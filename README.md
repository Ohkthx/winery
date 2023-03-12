# Winery
Winery is a script for debugging **Wine** installations and discovering the required **Winetricks** packages. This process can be time consuming when the objective is to identify the <ins>**EXACT**</ins> packages required to get an application up and running without the bloat of unneeded packages. On the first start of **Winery**, a configuration file labled `settings.sh` is created that needs to be modified.

After your initial installation of an application inside of a WINE PREFIX. You can use the `./winery --winecfg` to launch **winecfg** tailored to the installation. After the user is satisfied with the configurations of the environment, `./winery --backup` is used to create a point that can be reverted to at any time. Proceed to use `./winery --winetricks some packages here` to install packages to support your application. 

TASTE TIME! When the user is ready to test the application to see if it works, execute `./winery --taste`. This has wine start the application in the proper environment utilizing any additional packages installed with `./winery --winetricks`. 

If the application fails to work, `./winery --restore` can be used to revert the whole environment back to last backup. This prevents the user having to remove the whole environment and reinstalling the application to try again.


## Options and Examples
```
usage: ./winery [--help] [--taste] [--backup] [--restore]

--help           Shows this message.
--taste          Test (taste) the product, start it to see if it works.
--winecfg        Starts winecfg in the proper environment.
--winetricks     Must be last flag, installs remaining arguments.

--backup         Create a backup of the WINE PREFIX.
--restore        Override current WINE PREFIX with a backup.

Examples:
  Test Application:  ./winery --taste
  Add Packages:      ./winery --winetricks corefonts dotnet48
  Launch WINECFG:    ./winery --winecfg
  Backup prefix:     ./winery --backup
  Restore prefix:    ./winery --restore

Report issues to:
  https://github.com/Ohkthx/winery
```

## Installation
```bash
# Obtaining winery with CURL
curl -O https://raw.githubusercontent.com/Ohkthx/winery/main/winery

# Obtaining winery with WGET
wget https://raw.githubusercontent.com/Ohkthx/winery/main/winery
```
