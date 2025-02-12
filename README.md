# Google drive download action

[![.github/workflows/test.yml](https://github.com/raeperd/google-drive-download-action/actions/workflows/test.yml/badge.svg)](https://github.com/raeperd/google-drive-download-action/actions/workflows/test.yml)
[![Quality Gate Status](https://sonarcloud.io/api/project_badges/measure?project=raeperd_google-drive-download-action&metric=alert_status)](https://sonarcloud.io/summary/new_code?id=raeperd_google-drive-download-action)
[![Maintainability Rating](https://sonarcloud.io/api/project_badges/measure?project=raeperd_google-drive-download-action&metric=sqale_rating)](https://sonarcloud.io/summary/new_code?id=raeperd_google-drive-download-action)
[![Lines of Code](https://sonarcloud.io/api/project_badges/measure?project=raeperd_google-drive-download-action&metric=ncloc)](https://sonarcloud.io/summary/new_code?id=raeperd_google-drive-download-action)
[![Code Smells](https://sonarcloud.io/api/project_badges/measure?project=raeperd_google-drive-download-action&metric=code_smells)](https://sonarcloud.io/summary/new_code?id=raeperd_google-drive-download-action)  
Github action for downloading google-drive files or folder using [Drives: list API](https://developers.google.com/drive/api/v3/reference/drives/list)

## Usage

```yaml
runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - uses: raeperd/raeperd/google-drive-download-action@v1.0
        with:
          clientId: ${{ secrets.CLIENT_ID }}
          clientSecret: ${{ secrets.CLIENT_SECRET }}
          redirectUri: ${{ secrets.REDIRECT_URI }}
          credential_json: ${{ secrets.CREDENTIAL_JSON }}
          q: "'1U-2NgagKTnqkIZrML52A2SsD9HDDeDN7' in parents"
          path: "./"
```

- `clientId` (required) 
  - Client id of oauth2 client application
- `clientSecret` (required)
  - Client secret of oauth2 client application
- `redirectUri` (required) 
  - Redirect uri of oauth2 client application
- `credential_json` (required)
  - credential.json value with refresh_token with scope `https://www.googleapis.com/auth/drive.readonly`
- `q` (required)
  - Query string to search for files and folders 
- `path` (optional)
  - Path to download files default to working directory
  - Default to `./`


## Getting Started
Before we start, we need Google Drive Application Project and `credential.json`

### Create Google Drive Application Project
1. [Create a Google Cloud project](https://developers.google.com/workspace/guides/create-project)
2. [Setup Google API Oauth2 prerequisites](https://developers.google.com/identity/protocols/oauth2/web-server#prerequisites)
   - After creating your credentials, download the `client_secret.json` file from the API Console.
3. [Enable the Google Drive API](https://developers.google.com/drive/api/v3/enable-drive-api)

### Create `credential.json`
- Create `credential.json` using [Node.js quickstart | Google Drive API](https://developers.google.com/drive/api/v3/quickstart/nodejs)  
- Or you can create `credential.json` using [ts-node - npm](https://www.npmjs.com/package/ts-node)
  1. Clone this repository, and install dependencies
  2. Move your `client_secret.json` file into repository directory with name `oauth.keys.json`
  3. ```shell
     ts-node write-credential.ts
     ```
  
❗❗ **NEVER INCLUDE YOUR CLIENT SECRET (`oauth.keys.json` and `credential.json`) IN VERSION CONTROL** ❗❗ 

### Setting up repository secret
To run this action, we need 4 repository secret parameter

1. clientId
2. clientSecret 
3. redirectUri 
4. credential_json

- First 3 parameters can be obtained by `client_secret.json` (or `oauth.keys.json`)
- credential_json is contents of file `credential.json` created by you
  - This value is parsed by action, using `JSON.parse()` function. 
  - Check out [/src/input.ts](./src/input.ts) for more detail

## How to debug google drive api query
Use [debug.ts](./debug.ts) file in this repo

1. Define constants `CLIENT_ID`, `CLIENT_SECRET`, `REDIRECT_URI`, `CREDENTIAL_JSON`
2. Define constants `query` inside `main()` function
3. Run `ts-node ./debug.ts` and checkout results

❗❗ **NEVER INCLUDE YOUR CHANGES OF `debug.ts` IN VERSION CONTROL ❗❗

# License 
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

# Contacts
raeperd117@gmail.com

