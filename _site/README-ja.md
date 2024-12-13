# easyindex-cli  <!-- omit in toc -->

<p align="center">
  <a href="README.md">English</a> •
  日本語 (Japanese)
</p>

`easyindex-cli`は、Google Index APIやIndexNow APIをとても簡単に取り扱えるようにします。

![Demo](demo.gif)

## インデックス  <!-- omit in toc -->

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

## インストールの前に...

- Googleサービスアカウントを作成する
- Google Indexing API用のクレデンシャルJSONファイルを用意する 
- サーチコンソールでサービスアカウントをサイトオーナーとして追加する

参照. [Google Search Central](https://developers.google.com/search/apis/indexing-api/v3/prereqs)

## 必須要件

- Googleサービスアカウント
- Google Indexing API用のクレデンシャルJSON

## インストール

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

## 使い方

### Google

#### クイックスタート

更新したページの送信:

```sh
# Mac / Linux:
easyindex-cli google publish updated -C (your credential json file path) https://example.com/foobar https://example.com/fizzbizz
 
# Windows:
easyindex-cli.exe google publish updated -C (your credential json file path) https://example.com/foobar https://example.com/fizzbizz
```

削除したページの送信:

```sh
# Mac / Linux:
easyindex-cli google publish deleted -C (your credential json file path) https://example.com/foobar https://example.com/fizzbizz
 
# Windows:
easyindex-cli.exe google publish deleted -C (your credential json file path) https://example.com/foobar https://example.com/fizzbizz
```

#### 基本的な使い方

> :smile:NOTE:  
>   環境変数 (`EASYINDEX_CREDENTIAL_PATH`) にクレデンシャルファイルのファイパスを設定しておけば省略することができます。

更新したページの送信:

```sh
# Mac /Linux:
easyindex-cli google publish updated https://example.com/foobar https://example.com/fizzbizz

# Windows:
easyindex-cli.exe google publish updated https://example.com/foobar https://example.com/fizzbizz
```

削除したページの送信:

```sh
# Mac /Linux:
easyindex-cli google publish updated https://example.com/foobar https://example.com/fizzbizz

# Windows:
easyindex-cli.exe google publish updated https://example.com/foobar https://example.com/fizzbizz
```

#### 制限回数の設定

> リクエスト回数の制限を設定できます。
>
>  Google Indexing APIで割り当てられた制限値を設定してください。

```sh
# Mac /Linux:
easyindex-cli google publish updated -l 200 https://example.com/foobar https://example.com/fizzbizz

# Windows:
easyindex-cli.exe google publish updated -l 200 https://example.com/foobar https://example.com/fizzbizz
```

#### 一括リクエスト (更新したページの送信 と 削除したページの送信)

```sh
# Mac / Linux:
easyindex-cli google publish --csv index.csv
 
# Windows:
easyindex-cli.exe google publish --csv index.csv
```

CSVの形式:

例.)

```csv
notification_type,url
URL_UPDATED,https://example.com/20da2710-e370-49e3-9ac8-c322007379a5
URL_DELETED,https://example.com/a949a013-9a11-492d-863f-45c3008ef43f
URL_UPDATED,https://example.com/f0e6e237-18f3-4857-88ea-c0dd1d26a5ce
```

### IndexNow

#### クイックスタート

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
>   いくつかの必須パラメータをフラグで指定する必要がありますが、それらはすべて環境変数で設定することができます。


```sh
# Mac / Linux:
easyindex-cli indexnow https://example.com/foobar https://example.com/fizzbizz
 
# Windows:
easyindex-cli.exe indexnow https://example.com/foobar https://example.com/fizzbizz
```

#### 制限回数の設定

```sh
# Mac / Linux:
easyindex-cli indexnow -q 1000 https://example.com/foobar https://example.com/fizzbizz
 
# Windows:
easyindex-cli.exe indexnow -q 1000 https://example.com/foobar https://example.com/fizzbizz
```

#### CSVによるリクエスト

```sh
# Mac / Linux:
easyindex-cli indexnow --csv index.csv
 
# Windows:
easyindex-cli.exe indexnow --csv index.csv
```

CSVの形式:

例.)

```csv
url
https://example.com/20da2710-e370-49e3-9ac8-c322007379a5
https://example.com/a949a013-9a11-492d-863f-45c3008ef43f
https://example.com/f0e6e237-18f3-4857-88ea-c0dd1d26a5ce
```

### Google & IndexNow

> :smile:NOTE:  
>   いくつかの必須パラメータをフラグで指定する必要がありますが、それらはすべて環境変数で設定することができます。

```sh
# Mac / Linux:
easyindex-cli publish --csv index.csv
 
# Windows:
easyindex-cli.exe publish --csv index.csv
```

CSVの形式:

例.)

```csv
notification_type,url
URL_UPDATED,https://example.com/20da2710-e370-49e3-9ac8-c322007379a5
URL_DELETED,https://example.com/a949a013-9a11-492d-863f-45c3008ef43f
URL_UPDATED,https://example.com/f0e6e237-18f3-4857-88ea-c0dd1d26a5ce
```

### Golangパッケージとして使用する

ref. [コアパッケージ](https://github.com/usk81/easyindex)

## パラメータ

### 共通

| 必須 | 環境変数 | フラグ | フラグ（短縮） | デフォルト値 | 説明 |
|---|---|---|---|---|---|
| :x: | - | help | h | - | コマンドヘルプ |
| :x: | - | csv | c | false | CSVファイルパス |
| :x: | - | json | j | false | JSONファイルパス |
| :x: | `EASYINDEX_DEBUG` | debug | d | false | デバッグログの出力 |
| :x: | `EASYINDEX_IGNORE_PRECHECK` | ignore-precheck | i | false | プレチェックを行わない |

### Google indexing API

| 必須 | 環境変数 | フラグ | フラグ（短縮） | デフォルト値 | 説明 |
|---|---|---|---|---|---|
| :o: | `EASYINDEX_GOOGLE_CREDENTIALS_PATH` | google-credentials | C | credentials.json | Googleのクレデンシャルファイルのパス |
| :o: | `EASYINDEX_GOOGLE_REQUEST_LIMIT` | google-limit | l | 200 | Google Index Publishing APIのリクエスト制限回数 |

### IndexNow API

| 必須 | 環境変数 | フラグ | フラグ（短縮） | デフォルト値 | 説明 |
|---|---|---|---|---|---|
| :o: | `EASYINDEX_INDEXNOW_HOST` | indexnow-host | H | (empty) | サイトのドメイン |
| :o: | `EASYINDEX_INDEXNOW_KEY` | indexnow-key | k | (empty) | IndexNowのkey |
| :o: | `EASYINDEX_INDEXNOW_KEY_LOCATION` | indexnow-keyfile | f | (empty) | IndexNowのkey-location |
| :x: | `EASYINDEX_INDEXNOW_REQUEST_LIMIT` | indexnow-limit | q | (empty) | IndexNow APIのリクエスト制限回数 |
| :o: | `EASYINDEX_INDEXNOW_SEARCH_ENGINE` | indexnow-searchengine | e | (empty) | IndexNow APIをリクエストする検索エンジンのURL |
