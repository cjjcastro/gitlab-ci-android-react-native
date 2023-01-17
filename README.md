# gitlab-ci-android-react-native
This Docker image contains the Android SDK and most common packages necessary for building Android apps in a CI tool like GitLab CI. Make sure your CI environment's caching works as expected, this greatly improves the build time, especially if you use multiple build jobs.

A `.gitlab-ci.yml` with caching of your project's dependencies would look like this:

```
image: cjjcastro/gitlab-ci-android-react-native

stages:
- build

cache:
  key: ${CI_PROJECT_ID}
  paths:
  - android/.gradle/

build:
  stage: build
  script:
  - npm install
  - cd android
  - chmod +x ./gradlew
  - ./gradlew assembleRelease
  artifacts:
    paths:
    - android/app/build/outputs/apk/
```
