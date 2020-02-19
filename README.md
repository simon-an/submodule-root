# submodule-root

```bash

git clone --recurse-submodules https://github.com/simon-an/submodule-root.git
git pull --recurse-submodules

git submodule init

git checkout master
// clone with --recurse-submodules
git submodule update 
// clone without --recurse-submodules
git submodule update --recursive --remote
git submodule status 
git submodule foreach "git branch -v"

git checkout develop
git submodule update --recursive --remote
git submodule status 
git submodule foreach "git branch -v"
```

### make sure the branch of the submodule is correct:

``` bash
git submodule foreach "git checkout <parent-branch>"
```

### new commit on the submodule:

```bash
echo this is a minor change >> README.md
git add README.md
git commit -m "change in submodule"
git push
```

### update the parent project branch

```bash
git add submodule-2
git commit -m "update submodule to include latest changes"
git push
```

### create release:

```bash
git checkout -b release-0.0.1
git submodule foreach "git checkout -b release-0.0.1"
git push -u origin release-0.0.1
git submodule foreach "git push -u origin release-0.0.1"
// bugfix commit to submodule
git add submodule-2
git commit -m "update submodule to release candidate"
git push

git checkout master
git submodule foreach "git checkout master"
git merge release-0.0.1
// submodule versioning might be too much effort, because commit sha as a reference is enough.
git submodule foreach "git merge release-0.0.1"
git push --recurse-submodules=on-demand

 git tag 0.0.1 -sam "this is a bugfix release bla bla"
 git submodule foreach git tag 0.0.1 -sam "this is a bugfix release bla bla"
 git submodule foreach git push origin 0.0.1
 git push origin 0.0.1 --recurse-submodules=on-demand

```

### merge back to develop

```bash
git submodule foreach git checkout develop
// merge tag or release branch
git submodule foreach git merge 0.0.1
git checkout develop
git add submodule-2
git merge 0.0.1
git commit -m "merge submodule release 0.0.1 to develop"
git push

// remove release branches:

git push origin --delete release-0.0.1
git submodule foreach git push origin --delete release-0.0.1
git branch -d release-0.0.1
git submodule foreach git branch -d release-0.0.1

```

### To remove a submodule you need to:

* Delete the relevant section from the .gitmodules file.
* Stage the .gitmodules changes git add .gitmodules
* Delete the relevant section from .git/config.
* Run git rm --cached submodule-2 (no trailing slash).
* Run rm -rf .git/modules/submodule-2 (no trailing slash).
* Commit git commit -m "Removed submodule-2 "
* Delete the now untracked submodule files rm -rf submodule-2
