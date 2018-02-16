# The `omekash` Command Line Tool

## Installation

Simply copy `omekash` to `/opt`.

## Configurations

## Commands

- `omeka new <name>`: Set up a new named Omeka instance. You will need 
to visit `http://127.0.0.1/omeka-<name>/install/install.php` to 
initialize its parameters.
  - `--branch <branch>`: Specify the branch to check out Omeka from. 
Default: `master`
  - `--repo <repository>`: Specify the repository to check out Omeka 
from. Default: `https://github.com/omeka/Omeka.git`
  - `--download <url>`: Use a download URL to a zip or tarball file 
instead of Git.
- `omeka rm <name>`: Remove the named Omeka instance.
- `omeka clone <oldname> <newname>`: Make an exact copy of the named 
Omeka instance.
- `omeka plug <name> <url>`: Download and add a plugin from the given 
URL to the named Omeka instance. The URL may be a Git repository, zip 
file or tarball file.
- `omeka unplug <name> <plugin-name>`: Directly remove a plugin from the 
named Omeka instance. * Warning: Make sure to uninstall the plugin 
first! *
- `omeka theme <name> <url>`: Download and add a theme from the given 
URL to the named Omeka instance. The URL may be a Git repository, zip 
file or tarball file.
- `omeka untheme <name> <theme-name>`: Directly remove a theme from the 
named Omeka instance. * Warning: Make sure that the theme is not 
currently used! *
