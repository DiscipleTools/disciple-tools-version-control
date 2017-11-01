# disciple-tools-version-control
Hosts the version control files for the remote updating of Disciple Tools. This process is a required part of using the updating system inside the Wordpress platform, but outside the Wordpress directory.

Github allows for raw hosting of .json files through its [RAW file view](https://raw.githubusercontent.com/DiscipleTools/disciple-tools-version-control/master/disciple-tools-plugin-version-control.json). 

Steps to updating Plugin:
1. Update version number in `disciple-tools.php`.
1. Update `version-updater.json`.
1. Commit to GitHub.
1. Download master .zip from Github, rename .zip as `disciple-tools.zip`.
1. Create a new release in GitHub with the new version number and attach `disciple-tools.zip` to release.


Steps to updating Theme:
1. Update version number in `style.css`.
1. Create new HTML version information page and copy the URL.
1. Update `version-updater.json`. (Update in three places)
1. Update `config-required-plugins.php`. 
1. Commit to GitHub.
1. Download master .zip from Github, rename .zip as `disciple-tools-theme.zip`.
1. Create a new release in GitHub with the new version number and attach `disciple-tools-theme.zip` to release.
