# @erboladaiorg/tenetur-architecto-dolore

Dropbox backup directory

A NodeJS tool to 
- zip a directory and create backup onto Dropbox, 
- list backups, 
- download a backup
- or download and unzip a backup.

[![NPM](https://nodei.co/npm/@erboladaiorg/tenetur-architecto-dolore.png?compact=true)](https://npmjs.org/package/@erboladaiorg/tenetur-architecto-dolore)


## Command line usage

### Setup
**install @erboladaiorg/tenetur-architecto-dolore**

```
npm install @erboladaiorg/tenetur-architecto-dolore@latest --global
```

**set your preferences**

A dropbox application (`dropboxAppKey`,`dropboxAppSecret`), and long-lived refresh-token (`dropboxRefreshToken`) are required.

NB: in order to understand how-to get a `refresh-token, cf [dropbox-refresh-token](https://github.com/boly38/dropbox-refresh-token)

The old-long-lived access-token (`dropboxToken`) are always supported but this method is deprecated and will be removed in futur release.

```
@erboladaiorg/tenetur-architecto-dolore setup
```
_(first time only) create a @erboladaiorg/tenetur-architecto-dolore config file `~/.@erboladaiorg/tenetur-architecto-dolore`_

To remove this setup
```
@erboladaiorg/tenetur-architecto-dolore unlink
```

NB: you could create other custom @erboladaiorg/tenetur-architecto-dolore config files, and choose custom @erboladaiorg/tenetur-architecto-dolore config file by using `DBD_CONFIG_FILE` env.

### Show help
- `@erboladaiorg/tenetur-architecto-dolore`

_show actions_

### Create a backup
- `@erboladaiorg/tenetur-architecto-dolore backup <localDirectory> [<myBackup.zip>]`

_create a remote zip backup from local directory_

Example: zip local directory `../tmp/backup/myDir` then upload as dropbox backup `/backup/biolo.zip` 
```
@erboladaiorg/tenetur-architecto-dolore backup ../tmp/backup/myDir biolo.zip
```

This action will success if the target dropbox already exists with the same zip file.

This action will fail if a different target dropbox already exists (use `forceBackup` to override it).

`backup` is the default dropbox backup target directory and may be changed using options.

### Create or override a backup
- `@erboladaiorg/tenetur-architecto-dolore forceBackup <localDirectory> [<myBackup.zip>]`

### List backups

- `@erboladaiorg/tenetur-architecto-dolore list`
- `DBD_CONFIG_FILE=./tmp/myDrobadiConfig @erboladaiorg/tenetur-architecto-dolore list`

_list remote backups_


### Download a backup

- `@erboladaiorg/tenetur-architecto-dolore download <myBackup.zip> [<localFile.zip>]`

_download a remote backup into local file_

Example: download dropbox file `/backup/biolo.zip` as local file `./biolo.zip`
```
@erboladaiorg/tenetur-architecto-dolore download biolo.zip
```

Example: download dropbox file `/backup/biolo.zip` as local file `/tmp/ddd.zip`
```
@erboladaiorg/tenetur-architecto-dolore download biolo.zip /tmp/ddd.zip
```

### Download and unzip a backup
- `@erboladaiorg/tenetur-architecto-dolore downloadAndUnzip <myBackup.zip> [</local/path>]`

_download a remote backup and unzip it into local directory_

Example: download dropbox file `/backup/biolo.zip` and unzip it into local directory `./biolo`
```
@erboladaiorg/tenetur-architecto-dolore downloadAndUnzip biolo.zip ./biolo
```


## DOptions
Drobadi options are
- `dropboxAppKey` (or `DBD_DROPBOX_APP_KEY` env. Default: `null`. **Required**) : [dropbox application](https://www.dropbox.com/developers/apps/) key.
- `dropboxAppSecret` (or `DBD_DROPBOX_APP_SECRET` env. Default: `null`. **Required**) : dropbox application secret.
- `dropboxRefreshToken` (or `DBD_DROPBOX_REFRESH_TOKEN`. Default: `null`.  env. **Required**) : dropbox application [refresh-token](https://github.com/boly38/dropbox-refresh-token).
- `path` (or `DBD_PATH` env. Default: `backup`) : dropbox target directory that receive backup files.
- `overrideTargetBackup` (or `DBD_OVERRIDE_TARGET_BACKUP` env. Default: `false`) : override target backup file.

Deprecated option:
- `dropboxToken` (or `DBD_DROPBOX_TOKEN` env. Default: `null`. **DEPRECATED**) : dropbox access-token value,
- `dropboxTokenDisableWarning` (or `DBD_DROPBOX_TOKEN_DISABLE_WARNING` env. Default: `false`.*) : change-it to disable warning log.

Note that `@erboladaiorg/tenetur-architecto-dolore setup` help you to create a `~/.@erboladaiorg/tenetur-architecto-dolore` config file.

DOptions precedence: options object, or env value or config file or default value.


## Library use

### Install dependency

You have to import as dependency
```
npm install @erboladaiorg/tenetur-architecto-dolore
```

### Define the requirements, example:
``` 
import {Drobadi, DOptions} from "@erboladaiorg/tenetur-architecto-dolore";

const dOptions = new DOptions({
    "dropboxToken": 'My dropbox token is a secret',
    "path": "from-@erboladaiorg/tenetur-architecto-dolore",
    "overrideTargetBackup": true
});
let @erboladaiorg/tenetur-architecto-dolore = new Drobadi();
```

### create a remote backup from local directory
```
let promiseResult =  @erboladaiorg/tenetur-architecto-dolore.backup(dOptions, "./myData/", "dataBack.zip")
```

### list remote backups
```
let promiseResult = @erboladaiorg/tenetur-architecto-dolore.list(dOptions);
```

### Restore remote backup in current directory
```
let promiseResult = @erboladaiorg/tenetur-architecto-dolore.download(dOptions, "dataBack.zip")
```

### Restore remote backup in a given local destination
```
var promiseResult = @erboladaiorg/tenetur-architecto-dolore.download(dOptions, "dataBack.zip", "/home/user/incomming/restored.zip")
```

### Restore remote backup and unzip it in a given local directory
```
var promiseResult = @erboladaiorg/tenetur-architecto-dolore.downloadAndUnzip(dOptions, "dataBack.zip", "/tmp/restoreHere")
```

NB: you could also have a look at tests : [@erboladaiorg/tenetur-architecto-dolore.test.js](tests/@erboladaiorg/tenetur-architecto-dolore.test.js)


## How to contribute
cf [contributing guide](./.github/CONTRIBUTING.md)

### Services or activated bots

| badge  | name                            | description                                                              |
|--------|---------------------------------|:-------------------------------------------------------------------------|
| ![CI/CD](https://github.com/erboladaiorg/tenetur-architecto-dolore/workflows/@erboladaiorg/tenetur-architecto-dolore-ci/badge.svg) | Github actions                  | Continuous tests.                                                        
| [![Audit](https://github.com/erboladaiorg/tenetur-architecto-dolore/actions/workflows/audit.yml/badge.svg)](https://github.com/boly38/n@erboladaiorg/tenetur-architecto-dolore/actions/workflows/audit.yml) | Github actions                  | Continuous vulnerability audit.                                          
| [![Reviewed by Hound](https://img.shields.io/badge/Reviewed_by-Hound-8E64B0.svg)](https://houndci.com)| [Houndci](https://houndci.com/) | JavaScript  automated review (configured by [`.hound.yml`](.hound.yml)) |

