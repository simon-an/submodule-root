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


### To remove a submodule you need to:

* Delete the relevant section from the .gitmodules file.
* Stage the .gitmodules changes git add .gitmodules
* Delete the relevant section from .git/config.
* Run git rm --cached submodule-2 (no trailing slash).
* Run rm -rf .git/modules/submodule-2 (no trailing slash).
* Commit git commit -m "Removed submodule-2 "
* Delete the now untracked submodule files rm -rf submodule-2