---
layout: base
title: 'snapcraft: command reference'
---

## General commands

<ul>
  <li style="margin-bottom: 0;"><a href="#help"><code>help</code></a></li>
  <li style="margin-bottom: 0;"><a href="#init"><code>init</code></a></li>
  <li style="margin-bottom: 0;"><a href="#list-plugins"><code>list-plugins</code></a></li>
</ul>


## Lifecycle commands

Calling snapcraft without a COMMAND will default to `snapcraft snap` and run the complete snapping lifecycle (pull -> build -> stage -> prime -> snap) for each part.

<ul>
  <li style="margin-bottom: 0;"><a href="#pull"><code>pull</code></a></li>
  <li style="margin-bottom: 0;"><a href="#build"><code>build</code></a></li>
  <li style="margin-bottom: 0;"><a href="#stage"><code>stage</code></a></li>
  <li style="margin-bottom: 0;"><a href="#prime"><code>prime</code></a></li>
  <li style="margin-bottom: 0;"><a href="#snap"><code>snap</code></a></li>
  <li style="margin-bottom: 0;"><a href="#pack"><code>pack</code></a></li>
  <li style="margin-bottom: 0;"><a href="#clean"><code>clean</code></a></li>
  <li style="margin-bottom: 0;"><a href="#cleanbuild"><code>cleanbuild</code></a></li>
</ul>


## Store commands

<ul>
  <li style="margin-bottom: 0;"><a href="#login"><code>login</code></a></li>
  <li style="margin-bottom: 0;"><a href="#logout"><code>logout</code></a></li>
  <li style="margin-bottom: 0;"><a href="#export-login"><code>export-login</code></a></li>
  <li style="margin-bottom: 0;"><a href="#whoami"><code>whoami</code></a></li>
  <li style="margin-bottom: 0;"><a href="#push"><code>push</code></a></li>
  <li style="margin-bottom: 0;"><a href="#release"><code>release</code></a></li>
  <li style="margin-bottom: 0;"><a href="#list-revisions"><code>list-revisions</code></a></li>
  <li style="margin-bottom: 0;"><a href="#status"><code>status</code></a></li>
  <li style="margin-bottom: 0;"><a href="#push-metadata"><code>push-metadata</code></a></li>
  <li style="margin-bottom: 0;"><a href="#close"><code>close</code></a></li>
  <li style="margin-bottom: 0;"><a href="#register"><code>register</code></a></li>
  <li style="margin-bottom: 0;"><a href="#list-registered"><code>list-registered</code></a></li>
  <li style="margin-bottom: 0;"><a href="#create-key"><code>create-key</code></a></li>
  <li style="margin-bottom: 0;"><a href="#register-key"><code>register-key</code></a></li>
  <li style="margin-bottom: 0;"><a href="#list-keys"><code>list-keys</code></a></li>
  <li style="margin-bottom: 0;"><a href="#sign-build"><code>sign-build</code></a></li>
</ul>


## Parts ecosystem commands

<ul>
  <li style="margin-bottom: 0;"><a href="#update"><code>update</code></a></li>
  <li style="margin-bottom: 0;"><a href="#search"><code>search</code></a></li>
  <li style="margin-bottom: 0;"><a href="#define"><code>define</code></a></li>
</ul>


## Command descriptions

### help

**Usage:** `snapcraft help [OPTIONS] <topic>`

Obtain help for a certain topic, plugin or command.

The <topic> can either be a plugin name or one of:

  - topics
  - plugins
  - sources

For example:

    snapcraft help cmake

Will return the `cmake` plugin help:

    The cmake plugin is useful for building cmake based parts.

    These are projects that have a CMakeLists.txt that drives the build.
    The plugin requires a CMakeLists.txt in the root of the source tree.
    ...


### init

**Usage:** `snapcraft init [OPTIONS]`

Initialize a snapcraft project.

For example:

    snapcraft init

Will initialize the project and return the location of your new `snapcraft.yaml`:

    Created snap/snapcraft.yaml.
    Edit the file to your liking or run `snapcraft` to get started


### list-plugins

**Usage:** `snapcraft list-plugins [OPTIONS]`

List the available plugins that handle different types of part. Note that this list does not include custom plugins contained in one's own source tree.

This command has an alias of `plugins`.

For example:

    snapcraft plugins

Will return the list of implemented plugins:

    ament      catkin-tools  dump    gulp     kernel  nil                python2  rust
    ant        cmake         go      jdk      make    nodejs             python3  scons
    autotools  copy          godeps  jhbuild  maven   plainbox-provider  qmake    tar-content
    catkin     dotnet        gradle  kbuild   meson   python             ruby     waf


### pull

**Usage:** `snapcraft pull [OPTIONS] [<part>...]`

Download or retrieve the source defined for a part. The default Ubuntu repositories will be used unless the `--enable-geoip` option is specified, in which case it will use the repositories geographically closest to you as determined by your IP address.

For example, to pull all parts:

    snapcraft pull

To pull only specific parts:

    snapcraft pull my-part1 my-part2


### build

**Usage:** `snapcraft build [OPTIONS] [<part>...]`

Build artifacts defined for a part. Systems capable of running parallel build jobs will do so unless the `--no-parallel-build` option is specified. It will also build for the host architecture unless the `--target-arch=<arch>` option is specified, in which case it will attempt to cross-compile a snap for that architecture (note that not all plugins support this).

For example, to build all parts:

    snapcraft build

To build only specific parts:

    snapcraft build my-part1 my-part2

To cross-compile all parts for armhf:

    snapcraft build --target-arch=armhf


### stage

**Usage:** `snapcraft stage [OPTIONS] [<part>...]`

Stage the part's built/installed artifacts into the common staging area.

For example, to stage all parts:

    snapcraft stage

To stage only specific parts:

    snapcraft stage my-part1 my-part2


### prime

**Usage:** `snapcraft prime [OPTIONS] [<part>...]`

Final copy and preparation for the snap.

For example, to prime all parts:

    snapcraft prime

To prime only specific parts:

    snapcraft prime my-part1 my-part2



### snap

**Usage:** `snapcraft snap [OPTIONS]`

Create a snap. The name of the snap will be `<snap name>_<architecture>.snap` unless the `--output` option is used. Note that if you want to snap a directory (as opposed to competing an entire lifecycle for all parts), you should use the [`pack`](#pack) command instead.

For example:

    snapcraft snap

To use a different name for the snap:

    snapcraft snap --output renamed-snap.snap


### pack

**Usage:** `snapcraft pack [OPTIONS] DIRECTORY`

Create a snap from a directory holding a valid snap, defined to be containing a valid `meta/snap.yaml`. The name of the snap will be `<snap name>_<architecture>.snap` unless the `--output` option is used.

For example:

    snapcraft pack my-snap-directory

To use a different name for the snap:

    snapcraft pack my-snap-directory --output renamed-snap.snap


### clean

**Usage:** `snapcraft clean [OPTIONS] [<part>...]`

Remove content - cleans downloads, builds or install artifacts. By default, all lifecycle steps of all parts are cleaned, unless part names are given and/or the `--step` option is used.

For example, to completely clean all parts and lifecycle steps:

    snapcraft clean

To clean only the back to the build step for all parts (leaving the pull step alone):

    snapcraft clean --step build

To clean only back to the build step for a specific part (leaving the pull step alone and not touching any other part):

    snapcraft clean --step build my-part


### cleanbuild

**Usage:** `snapcraft cleanbuild [OPTIONS]`

Create a snap using a clean environment managed by LXD. This requires a properly-setup LXD environment that can connect to external networks. Refer to the "Ubuntu Desktop and Ubuntu Server" section on [Linux Containers Getting Started Guide](https://linuxcontainers.org/lxd/getting-started-cli) to get started. If using a remote, prior setup is required which is described in the ["multiple hosts"](https://linuxcontainers.org/lxd/getting-started-cli/#multiple-hosts) section of that guide.

For example:

    snapcraft cleanbuild


### login

**Usage:** `snapcraft login [OPTIONS]`

Login with your Ubuntu One e-mail address and password. Note that it will prompt for login information unless one specifies the `--with` option. See the [`export-login`](#export-login) command for more details.

If you do not have an Ubuntu One account, you can create one at https://dashboard.snapcraft.io/openid/login

For example:

    snapcraft login

Output:

    Enter your Ubuntu One e-mail address and password.
    If you do not have an Ubuntu One account, you can create one at https://dashboard.snapcraft.io/openid/login
    Email: me@example.com
    Password:

    Login successful.

To login with a file containing an exported login:

    snapcraft login --with exported

Output:

    Login successful. You now have these capabilities:

    snaps:       No restriction
    channels:    No restriction
    permissions: ['package_upload', 'package_access', 'package_manage']
    expires:     2019-01-23T23:51:19.642295



### logout

**Usage:** `snapcraft logout`

Clear session credentials.

### export-login

**Usage:** `snapcraft export-login [OPTIONS] FILE`

Save login configuration for a store account in FILE. This file can then be used to log in to the given account with the specified permissions using `login --with FILE`. This is typically used to manage snaps from some sort of CI environment in a controlled manner. Note however that the exported login _is not encrypted_! Do not commit it to version control without encrypting it.

The exported login grants access to all snaps accessible from the account unless the `--snaps` option is used to limit it. It also grants access to all channels unless the `--channels` option is used to limit it. The login will grant access to all capabilities unless the `--acls` option is used to limit it. Finally, the login expires after one year, at which time a new login will need to be exported. An expiration shorter than a year can be requested with the `--expires` option.


For example, to limit access to the edge channel of any snap the account can access:

    snapcraft export-login --channels=edge exported

Or to limit access to only the edge channel of a single snap:

    snapcraft export-login --snaps=my-snap --channels=edge exported

To limit access to a single snap, but only until 2019:

    snapcraft export-login --expires="2019-01-01T00:00:00" exported


### whoami

**Usage:** `snapcraft whoami`

Prints information regarding the account that's currently logged in.

For example:

    snapcraft whoami
    email:        me@example.com
    developer-id: 4tAgWHFEL13m9l8mSiBtBDJnnSQ2v0c9


### push

**Usage:** `snapcraft push [OPTIONS] <snap-file>`

Push `<snap-file>` to the store. This operation will block until the store finishes processing the snap. Note that the snap must first be registered to your account, see the [`register`](#register) command for more information.

By default, this command will simply create a new revision in the store and run the automated checks; it won't be released into any channel. One may request the snap be released into one or more channels by specifying the `--release` option with a comma-separated list of channels.

For example, to push a snap without releasing it:

    snapcraft push my-snap_0.1_amd64.snap

To push a snap and release it to edge:

    snapcraft push --release edge my-snap_0.2_amd64.snap

To push a snap and release it to multiple channels:

    snapcraft push --release candidate,beta my-snap_0.3_amd64.snap


### release

**Usage:** `snapcraft release [OPTIONS] <snap-name> <revision> <channel>[,<channel>...]`

Release `<revision>` of `<snap-name>` to the selected store `<channel>`(s). `<revision>` must exist on the store; see the [`list-revisions`](#list-revisions) command to see available revisions.

The format for channels is `[<track>/]<risk>[/<branch>]` where

  - `<track>` is used to have long term release channels. It is implicitly set to `latest`. If this snap requires one, it can be created by request by having a conversation on https://forum.snapcraft.io under the *store* category
  - `<risk>` is mandatory and can be either `stable`, `candidate`, `beta` or `edge`
  - `<branch>` is optional and dynamically creates a channel that expires in a month

For example, to release revision 8 of `my-snap` into `stable`:

    snapcraft release my-snap 8 stable

To release revision 8 into a temporary branch:

    snapcraft release my-snap 8 stable/my-branch

To release revision 8 into the stable channel of the 12 track:

    snapcraft release my-snap 8 12/stable


### list-revisions

**Usage:** `snapcraft list-revisions [OPTIONS] <snap-name>`

Get the history in the store for `<snap-name>`. This command has an alias of `revisions`. It will show all revisions for all architectures unless the `--arch` option is used.

For example, to list all revisions of a specific snap:

    snapcraft list-revisions my-snap

To list all armhf revisions of a specific snap:

    snapcraft list-revisions --arch armhf my-snap


### status

**Usage:** `snapcraft status [OPTIONS] <snap-name>`

Get the status in the store for `<snap-name>`. This includes all tracks, risks, and branches, for all architectures (unless the `--arch` option is used).

For example, to get the status of everything for a specific snap:

    snapcraft status snapcraft
    Track    Arch    Channel    Version             Revision    Expires at
    latest   amd64   stable     2.35                794
                     candidate  ^                   ^
                     beta       2.38                1008
                     edge       2.38+git32.e993544  1043
             arm64   stable     2.35                796
                     candidate  ^                   ^
                     beta       2.38                1011
                     edge       2.38+git32.e993544  1045
             armhf   stable     2.35                795
                     candidate  ^                   ^
                     beta       2.38                1010
                     edge       2.38+git32.e993544  1046
             i386    stable     2.35                793
                     candidate  ^                   ^
                     beta       2.38                1009
                     edge       2.38+git32.e993544  1044

To get the status of only armhf:

    snapcraft status --arch armhf snapcraft
    Track    Arch    Channel    Version             Revision    Expires at
    latest   armhf   stable     2.35                795
                     candidate  ^                   ^
                     beta       2.38                1010
                     edge       2.38+git32.e993544  1046


### push-metadata

**Usage:** `snapcraft push-metadata [OPTIONS] <snap-file>`

Push metadata from `<snap-file>` to the store. This will error if the data in the store has diverged from the data in the snap unless the `--force` option is specified, in which case the data from the snap will overwrite the data in the store.

For example:

    snapcraft push-metadata my-snap_0.1_amd64.snap

To force the metadata in the snap to overwrite that in the store:

    snapcraft push-metadata --force my-snap_0.1_amd64.snap


### close

**Usage:** `snapcraft close [OPTIONS] <snap-name> <channel>[,<channel>...]`

Close `<channel>`(s) for `<snap-name>`. Closing a channel causes it to track the channel that follows it in the channel release chain. For example, closing the 'candidate' channel would make it track the 'stable' channel.

For example, to close the `beta` channel (thereby causing it to track the `candidate` channel):

    snapcraft close my-snap beta

To close the `beta` and `edge` channels (thereby causing both of them to track the `candidate` channel):

    snapcraft close my-snap beta edge


### register

**Usage:** `snapcraft register [OPTIONS] <snap-name>`

Register `<snap-name>` with the store. It will be registered to the account that is currently logged in. The snap will be registered publicly unless the `--private` option is specified.

For example:

    snapcraft register my-snap-name

To register a private snap:

    snapcraft register --private my-snap-name


### list-registered

**Usage:** `snapcraft list-registered`

List snap names registered to or shared with you. This command has an alias of `registered`.

For example:

    snapcraft list-registered

Will return all snap names you have access to:

    Name                          Since                 Visibility    Price    Notes
    my-snap1                      2016-06-22T15:46:17Z  public        -        -
    my-snap2                      2017-10-23T19:41:19Z  public        -        -


### create-key

**Usage:** `snapcraft create-key <key-name>`

Create a key to sign assertions. Note that the key must be registered via the [`register-key`](#register-key) command before the signature will be recognized by the store. See the [`sign-build`](#sign-build) command for an example of using this key.

For example:

    snapcraft create-key my-test-key


### register-key

**Usage:** `snapcraft register-key <key-name>`

Register the key named `<key-name>` with the store to sign assertions.

For example:

    snapcraft register-key my-test-key


### list-keys

**Usage:** `snapcraft list-keys`

List the keys available to sign assertions. This command has an alias of `keys`.

For example:

    snapcraft list-keys

Will return keys you have already generated:

````
    Name        SHA3-384 fingerprint
*   my-test-ey  Qjd2pj0EWLWkiiZ21HuFlhkSUqd3F3Df8Oj4x9UjeG0pFL0v321cLkQNr624hROy
````

### sign-build

**Usage:** `snapcraft sign-build [OPTIONS] <snap-file>`

Sign a built snap file and assert it using the developer's key. If there are multiple keys available, specify one using the `--key-name`option. The resulting assertion will be pushed to the store unless one specifies the `--local` option.

For example:

    snapcraft sign-build my-snap.snap

To use a specific key:

    snapcraft sign-build --key-name my-test-key my-snap.snap


### update

**Usage:** `snapcraft update`

Updates the parts listing from the cloud. Remote parts are listed and modifiable on the [wiki](https://wiki.ubuntu.com/snapcraft/parts).

For example:

    snapcraft update


### search

**Usage:** `snapcraft search [OPTIONS] <query>...`

Searches the remote parts cache for matching parts.

For example:

    snapcraft search go

Will return all matching parts:

    PART NAME  DESCRIPTION
    go         Go is an open source programming language that makes it easy to build simple,
    mongodb    A document-oriented database


### define

**Usage:** `snapcraft define [OPTIONS] <part>`

Shows the definition for the specified cloud part.

For example:

    snapcraft define go

Will return the definition for the `go` part:

    Maintainer: 'Leo Arias <leo.arias@canonical.com>'
    Description: Go is an open source programming language that makes it easy to build simple,
    reliable, and efficient software.
    This snapcraft part allows to build programs written in go.
    Usage:
      Add "after: [go]" to your part written in go. This will use the latest go
       from the master branch to compile your program.
      If you want to specify a go version, also add a go part with the version as
      the source-tag value. For example, to use go 1.7.5, use:
        parts:
          my-go-program:
            ...
            after: [go]
          go:
            source-tag: go1.7.5

    go:
      build: cd src && env GOROOT_BOOTSTRAP=$(go env GOROOT | tr -d '\n') ./make.bash
      build-packages:
      - golang-go
      - g++
      install: cp -R * $SNAPCRAFT_PART_INSTALL
      plugin: nil
      prime:
      - -*
      source: https://go.googlesource.com/go
      source-type: git
      stage:
      - bin
