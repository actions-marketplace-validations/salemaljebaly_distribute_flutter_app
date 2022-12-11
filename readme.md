
# [<img src="https://assets.testapp.io/logo/blue.svg" width="200" alt="TestApp.io"/>  <img width="120" src="https://docs.flutter.dev/assets/images/shared/brand/flutter/logo/flutter-lockup.png"/>](https://testapp.io/) Github Action

### Testappio is simple platfrom used for testing, sharing & feedback

The action from [TestApp action](https://github.com/testappio/github-action)

Action used for support flutter app instead of using for android and ios separately.

Now the action support android and the apk build  from flutter Framework

## Sample for build APK with Flutter
```
name: build android with flutter
on:
  push:
    branches:
      - deploy

jobs:
  export_android:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-java@v2
        with:
          distribution: 'zulu'
          java-version: "12.x"
      - uses: subosito/flutter-action@v2
        with:
          channel: stable
      - run: flutter clean
      - run: flutter pub get
      - run: flutter build apk --release

      - name: Upload APK to TestApp.io
        uses: testappio/github-action@v5
        with:
          api_token: ${{secrets.TESTAPPIO_API_TOKEN}} # generate from testapp.io
          app_id: ${{secrets.TESTAPPIO_APP_ID}} # APP_ID from testapp.io
          
          file: build/app/outputs/flutter-apk/app-release.apk
          release_notes: "Testing manual debug notes..."
          git_release_notes: true
          include_git_commit_id: false
          notify: true
```

If you want a debug version, replace the following:

`run: flutter build apk --debug`

`file: build/app/outputs/flutter-apk/app-debug.apk`


For more infomation visit [TestApp action](https://github.com/testappio/github-action)