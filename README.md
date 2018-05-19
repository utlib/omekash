# `omekash`: A Command Line Tool for Omeka Classic 2.x

`omekash` allows you to easily provision, back up, and manage Omeka instances on a local development environment.

## Installation

Simply copy `omekash` to `/opt`. Make sure that its execute permission is enabled.

## Command verbs

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

## Configurations

- `rootuser`: The name of the root user in MySQL. Required for setting up new instances. Default: `root`
- `rootpass`: The password of the root user in MySQL. Required for setting up new instances. Default: `root`
- `httproot`: The path to the root directory from which Apache serves. Default: `/var/www/html`
- `wwwuser`: The user name that Apache runs as. Default: `www-data`
- `wwwgroup`: The group name that Apache runs as. Default: `www-data`
- `origdir`: The default path to find existing Omeka instances in. Default: `${httproot}/omeka-${origslug}`
- `origuser`: The default database user from existing Omeka instances. Default: `omeka${origslug}`
- `origpass`: The default database password from existing Omeka instances. Default: `omeka${origslug}root1108`
- `targetdir`: The default path to put new Omeka instances in. Default: `${httproot}/omeka-${slug}`
- `dbuser`: The default database user to give to new Omeka instances. Default: `omeka${slug}`
- `dbpass`: The default database password to give to new Omeka instances. Default: `omeka${slug}root1108`
- `branch`: The default branch to clone from in Git-dependent commands. Default: `master`

To override default values, add a `omekash-config` file in the same directory as `omekash`. It should contain Bash shell code that sets one or more of the variables above. *Make sure that its execute permission is disabled so it does not appear on tab auto-complete.*

## Hooks

You can insert custom code into certain points of execution using hook files. They can be added as code fragment files in the same directory as `omekash`. When `omekash` runs, these files are sourced in at runtime, as though they were part of `omekash` itself. *Make sure that the execute permission on these files is disabled so that none of them appear on tab auto-complete.*

- If you want custom code to run before and/or after any command verb, you can add `omekash-before` and/or `omekash-after`.
- If you want custom code to run before and/or after a specific command verb, you can add `omekash-before-verb` and/or `omekash-after-verb` (replace `verb` with the actual verb used, e.g. `new` or `rm`).

If you wish to run `omekash` without triggering hooks, add a `--vanilla` parameter to your call.

Hooks run in the following order for any given command verb:

- Global before (`omekash-before`)
- Verb before (`omekash-before-verb`)
- Verb after (`omekash-after-verb`)
- Global after (`omekash-after`)
