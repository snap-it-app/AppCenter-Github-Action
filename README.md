# App Center Github Action

This action run any App Center CLI command.

## Inputs

### `command`

**Required** The full command you want to use:
https://github.com/microsoft/appcenter-cli

### `token`

**Required** App Center token - you can get one from appcenter.ms/settings


```
name: Build, code quality, tests 

on: [push]

jobs:
  build:

    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v1
    - name: set up JDK 1.8
      uses: actions/setup-java@v1
      with:
        java-version: 1.8
    - name: build release 
      run: ./gradlew assembleRelease
    - name: upload artefact to App Center
      uses: joabalea/App-Center-action@v1.0.2
      with:
        command: appcenter distribute stores publish -s Beta -f app/build/outputs/apk/release/app-release-unsigned.apk -r releaseNote -a user/app
        token: ${{secrets.APP_CENTER_TOKEN}}
```
