# munki-custom-installer
Customize the Repo and Manifest into the Munki installer

## Why custom installers for Munki?
My organization has many different admins who work with Macs. Some of them only
have a few and desire to use management tools without the need to stand up
their own tools.

### Why not use defaults?
While this can be done server side using the default settings for munki (repo url =
http://munki/repo and manifest = site_default) to install the proper repo url
and manifest, I wanted something a little more straight forward for these
admins and not have to mess with DNS records and computers accidentally going
to the wrong manifest.

## Usage
-r  --repo      munki repo url (SoftwareRepoURL)
-s  --source    source to original munki package
-m  --manifest  name of the default manifest or path to the directory containing multiple manifests
-o  --output    directory to output packages to (defaults to current)
-h  --help      show this help text

## How it works
I'm definitely open to better ways of doing this, but currently the script
expands the given munki installer and adds two lines to the preinstall script
of the munkitools_app installer.
```
sudo defaults write /Library/Preferences/ManagedInstalls.plist ClientIdentifier $manifest
sudo defaults write /Library/Preferences/ManagedInstalls.plist SoftwareRepoURL $repo
```
It would be great to move this to its own
installer, but for now this works. It's only really meant for the initial
enrollment of a machine into munki.
