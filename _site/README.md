# easyindex-cli  <!-- omit in toc -->

<p align="center">
  English •
  <a href="README-ja.md">日本語 (Japanese)</a>
</p>

`easyindex-cli` makes super easy to use Google Index API and IndexNow API!!

![Demo](demo.gif)

## index  <!-- omit in toc -->

- [preinstall](#preinstall)
- [required](#required)
- [install](#install)
- [Usage](#usage)
  - [Google](#google)
    - [quickstart](#quickstart)
    - [basic usage](#basic-usage)
    - [set quota](#set-quota)
    - [bulk request (updated \& deleted)](#bulk-request-updated--deleted)
  - [IndexNow](#indexnow)
    - [quickstart](#quickstart-1)
    - [basic usage](#basic-usage-1)
    - [set quota](#set-quota-1)
    - [use csv](#use-csv)
  - [Google \& IndexNow](#google--indexnow)
  - [Use as Golang package](#use-as-golang-package)
- [Parameters](#parameters)
  - [common](#common)
  - [Google indexing API](#google-indexing-api)
  - [IndexNow API](#indexnow-api)

## preinstall

- create Google service account
- create credential json file for Google Indexing API
- add your service account as a site owner on search console

ref. [Google Search Central](https://developers.google.com/search/apis/indexing-api/v3/prereqs)

## required

- Google service account
- credential json file for Google Indexing API

## install

Mac/Linux:

```sh
wget -O- https://github.com/usk81/easyindex-cli/releases/download/v{version}/easyindex-cli_{version}_{os}.tar.gz | tar xz
# e.g.
# mac M1 / version v1.0.1
# wget -O- https://github.com/usk81/easyindex-cli/releases/download/v1.0.1/easyindex-cli_1.0.1_darwin_amd64.tar.gz | tar xz
```

Windows (PowerShell):

```sh
iwr -outf easyindex-cli.tar.gz https://github.com/usk81/easyindex-cli/releases/download/v{version}/easyindex-cli_{version}_{os}.tar.gz
# e.g.
# 64bit / version v1.0.1
# iwr -outf easyindex-cli.tar.gz https://github.com/usk81/easyindex-cli/releases/download/v1.0.1/easyindex-cli_1.0.1_windows_amd64.tar.gz
```

## Usage

### Google

#### quickstart

updated:

```sh
# Mac / Linux:
easyindex-cli google publish updated -C (your credential json file path) https://example.com/foobar https://example.com/fizzbizz
 
# Windows:
easyindex-cli.exe google publish updated -C (your credential json file path) https://example.com/foobar https://example.com/fizzbizz
```

deleted:

```sh
# Mac / Linux:
easyindex-cli google publish deleted -C (your credential json file path) https://example.com/foobar https://example.com/fizzbizz
 
# Windows:
easyindex-cli.exe google publish deleted -C (your credential json file path) https://example.com/foobar https://example.com/fizzbizz
```

#### basic usage

> :smile:NOTE:  
>   You can omit specifying the credential file path by setting it in an environment variable (`EASYINDEX_CREDENTIAL_PATH`).

updated:

```sh
# Mac /Linux:
easyindex-cli google publish updated https://example.com/foobar https://example.com/fizzbizz

# Windows:
easyindex-cli.exe google publish updated https://example.com/foobar https://example.com/fizzbizz
```

deleted:

```sh
# Mac /Linux:
easyindex-cli google publish updated https://example.com/foobar https://example.com/fizzbizz

# Windows:
easyindex-cli.exe google publish updated https://example.com/foobar https://example.com/fizzbizz
```

#### set quota

> You can limit the number of requests.
>
> Please set based on the quota of Google Indexing API.

```sh
# Mac /Linux:
easyindex-cli google publish updated -l 200 https://example.com/foobar https://example.com/fizzbizz

# Windows:
easyindex-cli.exe google publish updated -l 200 https://example.com/foobar https://example.com/fizzbizz
```

#### bulk request (updated & deleted)

```sh
# Mac / Linux:
easyindex-cli google publish --csv index.csv
 
# Windows:
easyindex-cli.exe google publish --csv index.csv
```

CSV format:

e.g.

```csv
notification_type,url
URL_UPDATED,https://example.com/20da2710-e370-49e3-9ac8-c322007379a5
URL_DELETED,https://example.com/a949a013-9a11-492d-863f-45c3008ef43f
URL_UPDATED,https://example.com/f0e6e237-18f3-4857-88ea-c0dd1d26a5ce
```

### IndexNow

#### quickstart

```sh
# Mac / Linux:
easyindex-cli indexnow \
-H https://example.com \
-k 978c7955fdd547848fd3901ba4321e24 \
-f https://example.com/978c7955fdd547848fd3901ba4321e24.txt \
-e https://www.bing.com \
https://example.com/foobar https://example.com/fizzbizz
 
# Windows:
easyindex-cli.exe indexnow
-H https://example.com 
-k 978c7955fdd547848fd3901ba4321e24 
-f https://example.com/978c7955fdd547848fd3901ba4321e24.txt 
-e https://www.bing.com 
https://example.com/foobar https://example.com/fizzbizz
```

#### basic usage

> :smile:NOTE:  
>   You need to specify some required parameters with flags, but you can omit them by setting them all as environment variables.

```sh
# Mac / Linux:
easyindex-cli indexnow https://example.com/foobar https://example.com/fizzbizz
 
# Windows:
easyindex-cli.exe indexnow https://example.com/foobar https://example.com/fizzbizz
```

#### set quota

```sh
# Mac / Linux:
easyindex-cli indexnow -q 1000 https://example.com/foobar https://example.com/fizzbizz
 
# Windows:
easyindex-cli.exe indexnow -q 1000 https://example.com/foobar https://example.com/fizzbizz
```

#### use csv

```sh
# Mac / Linux:
easyindex-cli indexnow --csv index.csv
 
# Windows:
easyindex-cli.exe indexnow --csv index.csv
```

CSV format:

e.g.

```csv
url
https://example.com/20da2710-e370-49e3-9ac8-c322007379a5
https://example.com/a949a013-9a11-492d-863f-45c3008ef43f
https://example.com/f0e6e237-18f3-4857-88ea-c0dd1d26a5ce
```

### Google & IndexNow

> :smile:NOTE:  
>   You need to specify some required parameters with flags, but you can omit them by setting them all as environment variables.

```sh
# Mac / Linux:
easyindex-cli publish --csv index.csv
 
# Windows:
easyindex-cli.exe publish --csv index.csv
```

CSV format:

e.g.

```csv
notification_type,url
URL_UPDATED,https://example.com/20da2710-e370-49e3-9ac8-c322007379a5
URL_DELETED,https://example.com/a949a013-9a11-492d-863f-45c3008ef43f
URL_UPDATED,https://example.com/f0e6e237-18f3-4857-88ea-c0dd1d26a5ce
```

### Use as Golang package

ref. [core package](https://github.com/usk81/easyindex)

## Parameters

### common

| requred | environment variables | flag | flag-shorthand | default | description |
|---|---|---|---|---|---|
| :x: | - | help | h | - | Help about any command |
| :x: | - | csv | c | false | CSV file path to request |
| :x: | - | json | j | false | JSON file path to request |
| :x: | `EASYINDEX_DEBUG` | debug | d | false | output debug logs |
| :x: | `EASYINDEX_IGNORE_PRECHECK` | ignore-precheck | i | false | ignore pre-check |

### Google indexing API

| requred | environment variables | flag | flag-shorthand | default | description |
|---|---|---|---|---|---|
| :o: | `EASYINDEX_GOOGLE_CREDENTIALS_PATH` | google-credentials | C | credentials.json | Google credential file path |
| :o: | `EASYINDEX_GOOGLE_REQUEST_LIMIT` | google-limit | l | 200 | number of Google Index Publishing API Request limit |

### IndexNow API

| requred | environment variables | flag | flag-shorthand | default | description |
|---|---|---|---|---|---|
| :o: | `EASYINDEX_INDEXNOW_HOST` | indexnow-host | H | (empty) | your web site domain |
| :o: | `EASYINDEX_INDEXNOW_KEY` | indexnow-key | k | (empty) | IndexNow key |
| :o: | `EASYINDEX_INDEXNOW_KEY_LOCATION` | indexnow-keyfile | f | (empty) | IndexNow key file location |
| :x: | `EASYINDEX_INDEXNOW_REQUEST_LIMIT` | indexnow-limit | q | (empty) | number of IndexNow API Request limit |
| :o: | `EASYINDEX_INDEXNOW_SEARCH_ENGINE` | indexnow-searchengine | e | (empty) | IndexNow target search engine URL |
