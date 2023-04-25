<p align="center">
    <a href="https://patreon.com/ohkthx" title="Donate to this project using Patreon">
        <img src="https://img.shields.io/badge/patreon-donate-red.svg?style=for-the-badge&color=f38ba8&label=PATREON&logo=patreon&logoColor=f38ba8&labelColor=11111b"
            alt="Patreon donate button"></a>
    <a href="https://ko-fi.com/G2G0J79MY" title="Donate to this project using Ko-fi">
        <img src="https://img.shields.io/badge/kofi-donate-ffffff.svg?style=for-the-badge&color=fab387&label=KOFI&logo=kofi&logoColor=fab387&labelColor=11111b"
            alt="Buy me a coffee! Ko-fi"></a>
<br>
    <a href="https://github.com/ohkthx/winery" title="Size of the repo!">
        <img src="https://img.shields.io/github/repo-size/ohkthx/winery?style=for-the-badge&color=cba6f7&label=SIZE&logo=codesandbox&logoColor=cba6f7&labelColor=11111b"
            alt="No data."></a>
</p>

# Winery
Winery is a cross-platform tool for debugging **Wine** installations and discovering the required **Winetricks** packages.

This process can be time consuming when the objective is to identify the <ins>**EXACT**</ins> packages required to get an application up and running without the bloat of unneeded packages. On the first start of **Winery**, a configuration file labled `settings.sh` is created that needs to be modified.

After your initial installation of an application inside of a WINE PREFIX. You can use the `./winery --winecfg` to launch **winecfg** tailored to the installation. After the user is satisfied with the configurations of the environment, `./winery --backup` is used to create a point that can be reverted to at any time. Proceed to use `./winery --winetricks some packages here` to install packages to support your application. 

TASTE TIME! When the user is ready to test the application to see if it works, execute `./winery --taste`. This has wine start the application in the proper environment utilizing any additional packages installed with `./winery --winetricks`. 

If the application fails to work, `./winery --restore` can be used to revert the whole environment back to last backup. This prevents the user having to remove the whole environment and reinstalling the application to try again.

## Installation
```bash
# Obtaining winery with CURL
curl -O https://raw.githubusercontent.com/Ohkthx/winery/main/winery

# Obtaining winery with WGET
wget https://raw.githubusercontent.com/Ohkthx/winery/main/winery
```

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

# Configuration

This configuration file is automatically created after the first run of Winery.

The WINEPREFIX variable is used by Wine to determine the root directory of the environment. For testing purposes, it is often easier to set a custom PREFIX so that the application is in an isolated environment. The user of this script does not need to set the WINEPREFIX directly, but instead modify the settings below.

In the example below. The WINEPREFIX will be `$HOME/.wine64_myapp` directory. The application that is being tested will be in `$HOME/.wine64_myapp/drive_c/Program\ Files/MyApp/MyApp.exe`

```
# Check for script updates.
AUTO_UPDATE_SCRIPT="true"

# WINEPREFIX_PARENT is the directory hosting the WINEPREFIX_DIR.
# WINEPREFIX_DIR is the directory hosting the Wine configuration.
# WINEPREFIX_ARCH is the architecture of the PREFIX this is often
#   set to either win32 or win64
WINEPREFIX_PARENT="$HOME"
WINEPREFIX_DIR=".wine64_myapp"
WINEPREFIX_ARCH="win32"
# NOTE: WINEPREFIX will be set to: WINEPREFIX_PARENT / WINEPREFIX_DIR

# PROGRAM_PARENT is the path starting from WINEPREFIX
# PROGRAM_EXE is the executable inside PROGRAM_PARENT to execute.
# PROGRAM_FLAGS are the command line arguments to pass to the executable.
PROGRAM_PARENT="drive_c/Program Files/MyApp"
PROGRAM_EXE="MyApp.exe"
PROGRAM_FLAGS="--debug"
# NOTE: The application being tasted will be...
#   WINEPREFIX / PROGRAM_PARENT / PROGRAM_EXE PROGRAM_FLAGS
```
