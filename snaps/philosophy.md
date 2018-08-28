---
layout: base
title: Snapping philosophy
---

You are new to this world of snaps and want to know what is different from traditional packaging? How to architect your
application bundle and iterate from prototype to get your application working? This is the place for you!


## Relocatable code!

The main concept to snap your software is that your application needs to be relocatable. It’s a good practice to not
rely on hard coded paths like /etc and such, but to read your assets, configuration, hooks from subdirectories of your
application. A common way for application is to first read some local directories, via a relative path to your executable,
and then fallback to global ones.

This will have the net benefit as well to enable your application working from your development directory, enabling as
well testers to only download it from your VCS to test a new feature, without relying on any global installation. The
write-debug-fix cycle just became way easier!

Note that you can use environment variables as well to influence the paths your application is looking at. Then, just
ship a wrapper script that you point your snap commands to, which is setting those environment variables based on `$SNAP`,
`$SNAP_DATA`, and `$SNAP_USER_DATA` for instance to know where to read data and assets from and where to write to.

## Ship (and refer!) to your own dependencies

Another important concept of snaps is that you are in control of your dependencies. You won’t have anymore other updates
on the system breaking you as long as you ship everything you need, and update them at your own pace.

Generally speaking, your snap will only see libraries and 3rd party dependencies from your snap itself and the **core**
snap. Do not rely on this latter apart from some system library like access to the network, device nodes and such. Ship
all your dependencies as part of your snap (and so, don’t hardcode paths to look for them!). **Snapcraft** helps you by
creating a master wrapper script redirecting library loading directory under your snap folder before fallbacking to
system one. The wrapper content varies depending on the technology you are using (via overriding `PYTHONPATH`,
`LD_LIBRARY_PATH`, `GEM_HOME`, `PATH`…).

## Write data to user path

You can’t write data to every user-writable paths with snap. Your snap-related data are constrained and located in very
few of them. This is to enable the rollback mechanism to revert your data alongside the code version itself, ensuring
your data are always compatible with your code.

So, use `$SNAP_USER_DATA` for user data. If you have global configuration that should be readable by multiple users,
read and write to `$SNAP_DATA`. Remember that this last path is only writable by the root user though.

You can have your wrapper script using the same environment variable technique than described on the first stanza.
Another strategy is to unconditionally `cd` to `$SNAP_USER_DATA`.

## Common vs versioned path.
The previously mentioned paths are versioned. It means that for each new update of your snap, the content will be
copied to a new directory.

Some data are big assets that don’t really need to be versioned (even if you rollback, there is no configuration or data
format that will be specific to one version). For this, you can use `$SNAP_USER_COMMON` and `$SNAP_COMMON`, which are
similar in permission that their `*_DATA` counterpart.

However, as their names indicate, any change done there will be common to all versions of your snap (only one instance
of the data exists on disk), and such shouldn’t contain any version-specific info. We discourage the use of that
directory for configuration (which may change format from one version to the next one), data storage and even database
files, if you don’t plan to keep the schema backward-compatible.

The rule of thumb is to think: “if I revert to previous version of snap, will it be able to read all data in COMMON
directories?” If the answer is no, move some of those data to the versioned one. Do not worry, we have a great garbage
collection keeping only few working versions of your snap!

## Always start developing your snap in devmode

Proper confinement is challenging topic. Adding on that adjustment you have to make to ensure your code is relocatable,
while shipping all your dependencies on a read only system is calling for trouble!

This is for all those reasons you should always start developing your snap in devmode: ensure you define
`confinement: devmode` in your **snapcraft.yaml** stanza and install your package with `--devmode`. Iterate over it
while getting your application working. Once done, open the system logs (`/var/log/syslog`), and you may see some
**apparmor** and **seccomp** warnings with `ALLOWED` tags. Those mean that you have some confinement work to do, by
adding the right interfaces plugs to your snap declaration.

You can then try to install your package in non devmode, use the `snappy-debug.security` command (from **snappy-debug**
package) to confirm that you don’t have any `DENIALS` left, or get advice on what interfaces you may want to declare.
Go through this iterative mode to get your confined snap working.

## Don’t request too many permissions

Some interfaces autoconnect while the snaps are installed, some don’t. That means that the lesser plugs you are using,
the greater chance you have for people to install your snap. For interfaces that don’t autoconnect, try to make them
optional and have your code fallback to proper messages explaining why this feature is good to enable them, or why
it is required.
