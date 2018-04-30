# `omekash`: A Command Line Tool for Omeka Classic 2.x

`omekash` allows you to easily provision, back up, and manage Omeka instances on a local development environment. 

## Installation

Simply copy `omekash` to `/opt`. Make sure that its execute permission is enabled.

## Configurations

Several global configurations are available at the top of the `omekash` file.

- `rootuser`: The name of the root user in MySQL. Required for setting up new instances.
- `rootpassword`: The password of the root user in MySQL. Required for setting up new instances.
- `httproot`: The path to the root directory from which Apache serves.
- `wwwuser`: The user name that Apache runs as.
- `wwwgroup`: The group name that Apache runs as.

## Commands

- `omekash new <slug>`: Set up a new named Omeka instance. You will need to visit `http://<server root>/omeka-<slug>/install/install.php` to initialize its parameters.
  - `--branch <branch>`: Specify the branch to check out Omeka from. Default: `master`
  - `--repo <repository>`: Specify the repository to check out Omeka from. Default: `https://github.com/omeka/Omeka.git`
  - `--url <url>`: Use a download URL to a zip or tarball file instead of Git.
- `omekash rm <slug>`: Remove the named Omeka instance.
- `omekash clone <oldslug> <newslug>`: Make a copy of the named Omeka instance.
- `omekash plug <slug>`: Download and add a plugin to the named Omeka instance. You must provide either a `--repo` or `--url` parameter, but not both.
  - `--branch <branch>`: Specify the branch to check out the plugin from. Can only be used with `--repo`. Default: `master`
  - `--repo <repository>`: Specify the repository to check out the plugin from.
  - `--url <url>`: Specify the URL to a zip or tarball file to download the plugin from.
- `omekash unplug <slug> <plugin-name>`: Directly remove a plugin from the named Omeka instance. *Warning: Make sure to uninstall the plugin first!*
- `omekash theme <slug>`: Download and add a theme from the given URL to the named Omeka instance. You must provide either a `--repo` or `--url` parameter, but not both.
  - `--branch <branch>`: Specify the branch to check out the theme from. Can only be used with `--repo`. Default: `master`
  - `--repo <repository>`: Specify the repository to check out the theme from.
  - `--url <url>`: Specify the URL to a zip or tarball file to download the theme from. 
- `omekash untheme <slug> <theme-name>`: Directly remove a theme from the named Omeka instance. *Warning: Make sure that the theme is not currently used!*
- `omekash archive <zipname> <slug>`: Save the given Omeka instance and its associated database in the given zip file.
- `omekash restore <zipname> <slug>`: Restore the Omeka instance archived in the given zip file (can be a local path or a download URL) to the new name. The new instance can be accessed at `http://<server root>/omeka-<newslug>`.
