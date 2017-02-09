# curl2me - A fast and simple pastie tool
--------------------------------------------

## Overview

* Operates via HTTP PUT
* Stores files using S3 or an S3 compatible API such as minio.io
* Fast and low resource consumption
* Stores metadata via LMDB

Inspired by fload from Frits Vlaanderen
https://github.com/frots/fload

## Usage 

### Uploading a file

```
$ curl -T /path/to/file https://endpoint/filename.ext

{
    "sha256sum": "c3ab8ff13720e8ad9047dd39466b3c8974e592c2fa383d4a3960714caef0c4f2",
    "filename": "filename.ext",
    "size": 34,
    "url": "https://endpoint/filename.ext",
    "deleteUrl": "https://endpoint/1f8fbf2b7eeee7b5787f2f436e9d1ff5303f0beb798c15f8754e9a7375960352"
    "mimeType": "text/plain",
    "remoteAddress": "8.8.8.8",
    "code": 0,
    "message": "New file created"
}
```

The output format can be changed by adding ?output=<output>

example:

```
$ curl -T /path/to/file https://endpoint/filename.ext?output=yaml
```

Passing an invalid output format results in a HTTP 400 error (Bad Request).

Supported output formats:

* json (default)
* yaml
* xml

You can also use stdin:

```
$ echo "something" | curl -T - https://endpoint/filename.ext
```

### Deleting a file

Deleting requires a HTTP DELETE to the returned "deleteUrl"

```
$ curl -X DELETE https://endpoint/1f8fbf2b7eeee7b5787f2f436e9d1ff5303f0beb798c15f8754e9a7375960352
```

## Compilation

Go 1.6+ is required to compile curl2me

To install the dependency's you will need gpm (https://github.com/pote/gpm)

then run:

```
$ gpm install
```

