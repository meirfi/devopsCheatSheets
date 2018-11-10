# Ubuntu - upgrade LTS OS


```bash

$ sudo apt update

$ sudo apt upgrade

# This makes sure your Ubuntu is up to date. Next, follow this up with:

$ sudo apt dist-upgrade
# This handles changing software dependencies with new versions of packages.
# I then follow this up with:

$ sudo apt-get autoremove
# This removes dependencies from uninstalled applications.
$ sudo apt install update-manager-core

# Finally:

$ sudo do-release-upgrade
```