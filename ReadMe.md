Isogeo.Help
==============

# General information
Isogeo.Help is the project used to generate the online help for the Isogeo platform.

# Development

## Development build

For a lightweight build, run the following command from this directory: `build.bat /dev /nopause`. In case of success the resulting documentation artefacts can be found in the `tmp\obj\bin` folder. 

- Prerequisites:
  * [Git for Windows](https://git-for-windows.github.io/) 2.x
  * [node.js](http://nodejs.org/) 4.x
  * [npm](https://npmjs.org/) 4.x
    + [Upgrading on Windows](https://github.com/npm/npm/wiki/Troubleshooting#upgrading-on-windows)
  * [Grunt CLI](http://gruntjs.com/):
    + `npm install -g grunt-cli`
  * [rimraf](https://www.npmjs.com/package/rimraf):
    + `npm install -g rimraf`
  * [Calibre](http://calibre-ebook.com/download_windows64) 64bit 3.5.0

## CI build

To simulate the CI continuous build, run the following command from this directory: `build.bat /nopause`.

- Prerequisites (in addition to all of the above):
  * Microsoft Visual Studio 2015
  * [MSBuild.Community.Tasks 1.5.0](https://github.com/loresoft/msbuildtasks)

# Related resources

- [Document de travail initial](https://docs.google.com/a/isogeo.fr/document/d/1D39wXdfw0ueq9PViHike9qlAO26PSs6IoyAUgsvC3_Y/edit)
- [Dedicated folder on Google Drive](https://drive.google.com/drive/u/0/#folders/0B1LzWJagMM-PVFZpeU9jQjZRYUk)
- [Redmine project (bug tracking)](https://dev.isogeo.net/redmine/projects/help)
- [WYSIWYG Editor (desktop)](https://github.com/GitbookIO/editor)
- [GitBook official website](https://www.gitbook.com)