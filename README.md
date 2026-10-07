<!--
#
# Licensed to the Apache Software Foundation (ASF) under one
# or more contributor license agreements.  See the NOTICE file
# distributed with this work for additional information
# regarding copyright ownership.  The ASF licenses this file
# to you under the Apache License, Version 2.0 (the
# "License"); you may not use this file except in compliance
# with the License.  You may obtain a copy of the License at
#
# http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing,
# software distributed under the License is distributed on an
# "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
#  KIND, either express or implied.  See the License for the
# specific language governing permissions and limitations
# under the License.
#
-->

# Cordova Android — VoltBuilder fork

This is a fork of [apache/cordova-android](https://github.com/apache/cordova-android),
maintained by [VoltBuilder](https://volt.build) so that **cordova-android 9
projects can still be built**. It is free to use, by anyone, with or without a
VoltBuilder account. The licence is unchanged: Apache 2.0, same as upstream.

If you are starting a new project, you do not want this. Use
[upstream cordova-android](https://github.com/apache/cordova-android).

## Why this fork exists

Apache's last cordova-android 9 release was **9.1.0, in April 2021**. It resolves
some of its build dependencies through **JCenter / Bintray**, which JFrog shut
down. Those hosts no longer serve artifacts, so a stock cordova-android 9
project fails during dependency resolution — not because of anything in your
app, and not in a way you can fix from your own `config.xml`.

Plenty of working apps were pinned to 9.x and had no reason to move. Rather than
tell those projects they were out of luck, we patched the dependency resolution
and kept the version alive.

## What changed

Two commits on top of Apache's `9.1.0`, tagged **`9.1.1`**:

| Commit | What it does |
| --- | --- |
| `d0a0492` | Fixes a Java dependency resolution failure |
| `c5b2041` | Removes the dead Bintray repository from `framework/build.gradle` |

That is the entire delta. No features, no behaviour changes, no backports — if
your app built on cordova-android 9.1.0 in 2021, it should build on `9.1.1` now.

Branches and tags for every other cordova-android version are present because
this is a full fork, but **`9.1.1` is the only tag we maintain.** For anything
10.x and above, use upstream.

## Using it

Add this to your `config.xml`:

```xml
<engine name="android" spec="https://github.com/voltbuilder/cordova-android#9.1.1" />
```

Then build as usual:

```sh
cordova build android
```

**Requires JDK 8.** cordova-android 9 predates the newer toolchains and will not
compile on a modern default JDK.

On VoltBuilder this works out of the box — the build agent selects JDK 8
automatically when it sees this engine URL. See
[Building for Android 12 and Later](https://volt.build/docs/android_12/) for how
engine versions map to JDK versions.

## Before you use it: the Play Store will not take these builds

Apps built with cordova-android 9 target **Android SDK 29**. Google Play has
required a higher target SDK for several years, for new apps *and* for updates
to existing ones. This fork is useful if you are distributing outside the Play
Store — enterprise distribution, direct APK download, sideloading, kiosk and
device-management deployments — or if you need to reproduce an old build.

If your app ships through Google Play, you need cordova-android 11 or later, and
this fork will not help you get there.

## Support

This is maintained, not developed. We keep `9.1.1` building; we are not adding
to it.

- **Bugs in this fork** — open an issue here.
- **Bugs in cordova-android itself** — report them to
  [Apache](https://github.com/apache/cordova-android/issues). We are not the
  Cordova project and cannot fix upstream.
- **VoltBuilder build problems** — [support@volt.build](mailto:support@volt.build).

## What VoltBuilder is

[VoltBuilder](https://volt.build) compiles Cordova and Capacitor web projects
into signed Android and iOS apps in the cloud. No Mac required for iOS, no local
Android SDK, nothing to install — upload a zip, get a signed app. We support
cordova-android 9 through 15 and Capacitor, which is why keeping this version
alive was worth the trouble.

---

Everything below is Apache's original README for cordova-android, unchanged.

---

# Cordova Android

[![NPM](https://nodei.co/npm/cordova-android.png)](https://nodei.co/npm/cordova-android/)

[![Node CI](https://github.com/apache/cordova-android/workflows/Node%20CI/badge.svg?branch=master)](https://github.com/apache/cordova-android/actions?query=branch%3Amaster)
[![codecov.io](https://codecov.io/github/apache/cordova-android/coverage.svg?branch=master)](https://codecov.io/github/apache/cordova-android?branch=master)

Cordova Android is an Android application library that allows for Cordova-based projects to be built for the Android Platform. Cordova based applications are, at the core, applications written with web technology: HTML, CSS and JavaScript.

[Apache Cordova](https://cordova.apache.org) is a project of The Apache Software Foundation (ASF).

## Requires

- Java JDK 1.8
- Android SDK [http://developer.android.com](https://developer.android.com/)

## Cordova Android Developer Tools

We recommend using the [Cordova command-line tool](https://www.npmjs.com/package/cordova) to create projects and be able to easily install plugins.

However, the following scripts can be used instead:

    ./bin/create [path package activity] ... creates the ./example app or a cordova android project
    ./bin/check_reqs ....................... checks that your environment is set up for cordova-android development
    ./bin/update [path] .................... updates an existing cordova-android project to the version of the framework

These commands live in a generated Cordova Android project. Any interactions with the emulator require you to have an AVD defined.

    ./cordova/clean ........................ cleans the project
    ./cordova/build ........................ calls `clean` then compiles the project
    ./cordova/log   ........................ streams device or emulator logs to STDOUT
    ./cordova/run   ........................ calls `build` then deploys to a connected Android device. If no Android device is detected, will launch an emulator and deploy to it.
    ./cordova/version ...................... returns the cordova-android version of the current project

## Using Android Studio

1. Create a project
2. Import it via "Non-Android Studio Project"

## Running the Native Tests

The `test/` directory in this project contains an Android test project that can be used to run different kinds of native tests. Check out the [README contained therein](test/README.md) for more details!
