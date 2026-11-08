
name: Build Accent Blue Drive

on:
  workflow_dispatch:

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - uses: actions/setup-java@v4
        with:
          distribution: temurin
          java-version: '17'

      - uses: gradle/actions/setup-gradle@v4
        with:
          gradle-version: '8.2'

      - name: Extract project
        run: |
          unzip -q ACCENT_BLUE_DRIVE_proyecto.zip
          test -f ACCENT_BLUE_DRIVE/app/build.gradle

      - name: Build APK
        run: gradle -p ACCENT_BLUE_DRIVE assembleDebug

      - uses: actions/upload-artifact@v4
        with:
          name: ACCENT_BLUE_DRIVE_APK
          path: ACCENT_BLUE_DRIVE/app/build/outputs/apk/debug/app-debug.apk
          
