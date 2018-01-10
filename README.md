# Disciple Tools Version Control
This repo hosts the public version control files necessary for triggering the remote updating of Disciple Tools.


## Steps for making a new release:
1. Update version number in `style.css` in the [Disciple Tools Theme](https://github.com/DiscipleTools/disciple-tools-theme) and commit changes to Github.
1. Create a new release in [Disciple Tools Theme](https://github.com/DiscipleTools/disciple-tools-theme) GitHub with the new version number and release description. The description must have a description section, a 'version required' line, and 'version tested up to' line. ([See  example](https://github.com/DiscipleTools/disciple-tools-version-control/blob/master/README.md#example-of-a-github-release-description))
1. Update the release notes page found in this repo inside [`docs/index.html`](https://github.com/DiscipleTools/disciple-tools-version-control/blob/master/docs/index.html). Find the "New Release Block" section inside the HTML and copy and paste a "New Release Block" section of code at the top of the existing list. Then add appropriate release notes. ([see example](https://github.com/DiscipleTools/disciple-tools-version-control#example-of-new-release-block-for-the-release-notes-indexhtml-page))
1. Download master .zip from [Disciple Tools Theme](https://github.com/DiscipleTools/disciple-tools-theme) Github repo, rename .zip to `disciple-tools-theme.zip`, and attach this zip file to the newly created version release.
1. Final Step (must be last), update `disciple-tools-theme-version-control.json`. This .json file needs updated in two places. ([see example](https://github.com/DiscipleTools/disciple-tools-version-control/blob/master/README.md#example-of-updating-the-disciple-tools-theme-version-controljson))

## Example of the style.css update:
```
/******************************************************************
Theme Name: Disciple Tools
Theme URI: http://disciple.tools
Description: Disciple Tools is a coalition management system for disciple making movements.
Author URI: https://github.com/DiscipleTools
GitHub Plugin URI: https://github.com/DiscipleTools/disciple-tools
Version: {UPDATE HERE]
Requires at least: 4.7.0
License: GPL-2.0 or later
License URI: https://www.gnu.org/licenses/gpl-2.0.html
Tags: Sass
******************************************************************/
```

## Example of a Github release description:
```
Description description description description description description description description description description description description description description. 

requires: 4.7.1
tested:  4.9.1
```


## Example of 'New Release Block' for the release notes index.html page:
```
  <!-- New Release Block -->
	<div class="release-block">
		<div class="version-number">
			<p><strong>v0.1.3</strong></p>
		</div>
		<div class="changed-items">
			<ul style="flex: 1 0 320px; margin-bottom: 0;">
				<li>First item changed.</li>
				<li>Second item changed.</li>
			</ul>
		</div>
	</div>
	<!-- End New Release Block -->
```


## Example of updating the disciple-tools-theme-version-control.json:
```
{
  "version": "{UPDATE HERE}",
  "details_url": "https://discipletools.github.io/disciple-tools-version-control/",
  "download_url": "https://github.com/DiscipleTools/disciple-tools-theme/releases/download/{UPDATE HERE}/disciple-tools-theme.zip"
}
```


## Mechanics of the updating system:
If a theme is hosted in the Wordpress directory, it has native access to the updating system inside the Wordpress software. But if the theme is not hosted inside the directory, and is therefore remotely hosted, then an additional system must be used to trigger and deliver updates to the native updating system inside the Wordpress software. This is what is required for Disciple Tools, because the requirements for hosting inside the Wordpress Directory to severly limit the implementation of the Disciple Tools system. (For example, not using custom tables for which Disciple Tools requires 6.)

The system for managing the remote update in Disciple Tools uses the library `plugin-update-checker`, which is found inside `disciple-tools-theme/dt-core/libraries/`.

This library is called from a class loaded in the `functions.php` file. 
```
if ( ! class_exists( 'Puc_v4_Factory' ) ) {
            require( get_template_directory() . '/dt-core/libraries/plugin-update-checker/plugin-update-checker.php' );
        }
        Puc_v4_Factory::buildUpdateChecker(
            'https://raw.githubusercontent.com/DiscipleTools/disciple-tools-version-control/master/disciple-tools-theme-version-control.json',
            __FILE__,
            'disciple-tools-theme'
        );
```
[link](https://github.com/DiscipleTools/disciple-tools-theme/blob/0a8ea1cef2d2b168b5021cbdc103066f4f448aaf/functions.php#L214)

When the Disciple_Tools class is loaded it checkes the .json url hosted here to see if there is a version update published. If there is, then the class downloads the .zip file hosted in the releases of Disciple-Tools-Theme and pulls the `disciple-tools-theme.zip` which should be prepared as part of the release.

This file is downloaded and goes through the native updating process built into the Wordpress software.

Fortunately, Github allows for raw hosting of .json files through its [RAW file view](https://raw.githubusercontent.com/DiscipleTools/disciple-tools-version-control/master/disciple-tools-plugin-version-control.json), which makes hosting this .json version file here a great option, even thought it could be hosted on any public server.
