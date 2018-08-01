Isogeo.Help
============

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

### Circle CI

The project is tested, built and served on CircleCI: https://circleci.com/bb/isogeo/isogeo-help.

As specified in the CircleCI configuration (see: .circleci/config.yml):

- each commit triggers a deploy on QA (http://help.qa.isogeo.com/ = https://qaisogeohelp.z28.web.core.windows.net/)
- each tag triggers a deploy on PROD - not configured yet

It pushes built static website on a Static Website hosted on Azure Storage (GPv2). For more details on this kind of product, refer to these resources:

- [Blog: Static website hosting for Azure Storage now in public preview](https://azure.microsoft.com/en-us/blog/azure-storage-static-web-hosting-public-preview/)
- [Official documentation: Static website hosting in Azure Storage](https://docs.microsoft.com/fr-fr/azure/storage/blobs/storage-blob-static-website)

To upload built result, [rclone](https://rclone.org/azureblob/) is preferred to azure-cli because of more efficient and flexible. It's installed and used through go context in CircleCI. It needs some environment variables corresponding to the [storage account keys (example for QA)](https://portal.azure.com/#@mathieubeckerhotmail.onmicrosoft.com/resource/subscriptions/82885610-5841-4749-8d71-46f56b643ad2/resourceGroups/QA-isogeo/providers/Microsoft.Storage/storageAccounts/qaisogeohelp/keys) and set in the [CircleCI project settings](https://circleci.com/bb/isogeo/isogeo-help/edit#env-vars).

----

## Docker

First of all: build it.

```powershell
docker build --rm -f Dockerfile -t isogeo/gitbook-builder:latest .
```

### Serve as a website

```powershell
docker run --name isogeo-help -v $PWD/Help:/srv/gitbook --rm -it -d -p 4567:4567 isogeo/gitbook-builder:latest
# alternativately, you can use the live reload server
docker run --name isogeo-help -v $PWD/Help:/srv/gitbook --rm -it -d -p 4567:4567 -p 35729:35729 isogeo/gitbook-builder:latest
```

Then, open your favorite browser to http://localhost:4567.

To stop it : ```docker stop isogeo-help```

### Build static website

```powershell
docker run --rm -v $PWD/Help:/srv/gitbook -v $PWD/dist:/srv/html isogeo/gitbook-builder gitbook build . /srv/html
```

----

# Related resources

- [Document de travail initial](https://docs.google.com/a/isogeo.fr/document/d/1D39wXdfw0ueq9PViHike9qlAO26PSs6IoyAUgsvC3_Y/edit)
- [Dedicated folder on Google Drive](https://drive.google.com/drive/u/0/#folders/0B1LzWJagMM-PVFZpeU9jQjZRYUk)
- [Redmine project (bug tracking)](https://dev.isogeo.net/redmine/projects/help)
- [WYSIWYG Editor (desktop)](https://github.com/GitbookIO/editor)
- [GitBook official website](https://www.gitbook.com)
