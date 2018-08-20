---
layout: base
title: Commands, daemons & assets
---

The entire syntax of a `snapcraft.yaml` with all available keys can be
reviewed in the [snapcraft.yaml syntax section](/build-snaps/syntax). Here we will
discuss the apps metadata in more detail.

## Declaring app commands

For every app you build in your snap, you can define which commands or
daemons are shipped. Declaring them in `snapcraft.yaml` will expose them in
the system. Starting with the **apps** keyword you specify each app and its
functionality. So, if there were two apps, one called *app1* and another
called *app2*, the extract would look like

```yaml
apps:
  app1:
    command: bin/app1
  app2:
    command: opt/bin/app2
    plugs:
      - network
```

So in the example, *app1* will declare its **command** to the relative path
`bin/app1`, while *app2* defines a
different **command** being `opt/bin/app2` and using the *network*
interface.

## Declaring daemons

Every app may build a binary that may need to be exposed in the system, with
that in mind, the way to expose a daemon is by using the **daemon**
keyword. So, if there were two services, one called *daemon1* and another
called *daemon2*, the extract would look like

```yaml
apps:
  daemon1:
    command: bin/app1
    daemon: simple
  daemon2:
    command: bin/app2 --start
    stop-command: bin/app2 --stop
    daemon: forking
```

So in the example, *daemon* will declare its start to the relative path
`bin/app1`, while *daemon2* defines a different start to `bin/app2`: it
declares an explicit stop mechanism.

Also note that *daemon1* is defined as a **simple** daemon, meaning that it
is expected that the command configured is the main process. Daemons like
*daemon2* which use **forking** have the configured command call fork() as
part of its start-up. The parent process is expected to exit when start-up is
complete and all communication channels are set up. The child continues to
run as the main daemon process. This is the behavior of traditional UNIX
daemons.

The `daemon` key values follow systemd service types (`forking`, `oneshot`, `notify` and `simple`). See the [apps and commands syntax](/build-snaps/syntax#apps-and-commands) for details on these types.

### Stopping daemons

To provide a clean way to stop a daemon, you can provide a `stop-command` with an additional `stop-timeout`. In case the `stop-command` does not successfully terminate the daemon in the timeout duration, it will be terminated with `SIGTERM` (and ultimately with `SIGKILL` if `SIGTERM` fails).

```yaml
apps:
  daemon1:
    command: bin/app1
    daemon: simple
    stop-command: bin/app1-stop
    stop-timeout: 10s
```

In this example, when snapd needs to stop `daemon1` (eg. if the user disables or removes the snap), `bin/app1-stop` will be executed.

See the [apps and commands syntax](/build-snaps/syntax#apps-and-commands) for details on how to automatically restart a daemon.

### Tutorial

To get a first experience with snapping a service, the ["Build a nodejs service" tutorial](https://tutorials.ubuntu.com/tutorial/build-a-nodejs-service?backURL=https://docs.snapcraft.io/build-snaps/metadata) will guide you through building, confining and general good practices to snap a simple web server.

## Using wrappers

It's customary to use within your app small wrappers that will launch the
real binaries. For instance, to select the binaries for the correct
architecture or to set runtime variables such as the application state
directory.

The typical wrapper is a small shell script that sets `PATH`,
`LD_LIBRARY_PATH` or other runtime specific environment variables.

For `PATH` to work properly, it's necessary not to hardcode any pathname in
your code. For instance, don’t rely on `/usr/bin/python` or on
`/usr/bin/java` but instead run `python` or `java`.

Snapcraft already generates a wrapper for each declared command, that adjusts symlinks to be relative and work for your snap. These wrappers are named after commands: `command-<command>.wrapper` and can be found in the `prime/` directory after a snapcraft build or in the  `/snap/<snap-name>/current/` directory after a snap install.

## Fixed assets

### Desktop files

You can declare a desktop file from your app within an `apps` entry using a path relative to the `prime` directory pointing to a desktop file, snapcraft will take care of the rest. If your project already has a desktop file, say in `/usr/share/applications/my-app.desktop` all you need to do is the following:

```yaml
apps:
    my-app:
        command: my-app
        desktop: usr/share/applications/my-app.desktop
```

Alternatively, you can create a `snap/gui/` directory at the root of your snapcraft project to host a desktop file:

    snap/gui/<app-name>.desktop
    snapcraft.yaml

Where `<app-name>` is the entry corresponding to `apps` in `snapcraft.yaml`.

### Package icons

To use an icon to represent your snap, just declare a PNG or SVG in
`snapcraft.yaml` through an `icon` entry with a path relative
to the icon inside the snap.


```yaml
icon: project/src/images/icon.png
```
