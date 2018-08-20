---
layout: base
title: Build and publish snaps from Git
---

You can build and publish snaps of commits to your Git repository so that other developers or early adopters can try the latest changes to your application.

This is an entirely automated process. Once set up, you should not need to touch it again.

## Using Travis

Extending your [Travis CI](https://travis-ci.org/) configuration to build and publish snaps on branch commits is easy. Run `snapcraft enable-ci travis` and you will be guided through the process.

Note that you should already have the following:
- The [Travis command line client](https://github.com/travis-ci/travis.rb#installation) installed.
- A [`.travis.yml`](https://docs.travis-ci.com/user/getting-started/) file in your project directory.
- Travis [enabled for your repository](https://travis-ci.org/profile/) and configured to "build pushes."

Travis does not currently allow open-source projects on [non-x86 architectures](https://docs.travis-ci.com/user/ci-environment/#Virtualization-environments), or builds that take longer than [50 minutes](https://docs.travis-ci.com/user/customizing-the-build#Build-Timeouts). 

- Tutorial: [Continuous snap delivery from Travis CI](https://tutorials.ubuntu.com/tutorial/continuous-snap-delivery-from-travis-ci?backURL=https://docs.snapcraft.io/build-snaps/ci-integration)

## Using CircleCI

- Tutorial: [Continuous snap delivery from CircleCI](https://tutorials.ubuntu.com/tutorial/continuous-snap-delivery-from-circle-ci?backURL=https://docs.snapcraft.io/build-snaps/ci-integration)

## Using Launchpad

Launchpad has no restrictions on build time, and can build for these architectures:
 - AMD x86-64 (amd64)
 - ARM ARMv8 (arm64)
 - ARM ARMv7 Hard Float (armhf)
 - Intel x86 (i386)
 - PowerPC64 Little-Endian (ppc64el)
 - IBM System z (s390x)

First, create an account on Launchpad and a project to host the build:
1. Fill in the form for a [new account](https://launchpad.net/+login)
1. Log in, and fill in the form on the [project registration](https://launchpad.net/projects/+new) page

Once registered, you can find your project listed under [your account](https://launchpad.net/~/+related-projects).

Now, configure the project to point at your existing Git repository:

1. From your project's main page, follow the "Code" link under "Configuration options"
1. Select "Git" under "Version control system"
1. Select "Import a Git repository hosted somewhere else" under "Link or import an existing repository"
1. In a new tab or window, go to your GitHub repository page and click the button for "Clone or download"
1. Select "Use HTTPS" and then click the "copy to clickboard" button
1. Back on the Launchpad page, paste the text from GitHub in the "Git repository URL" box and click the "update" button

Launchpad will now schedule an import of your GitHub repo. This will only take a few minutes. Grab a coffee, refresh the page, and you should see each of your branches listed.

Finally, tell Launchpad to build and publish snaps for this repository:

1. Under the "Branches" heading, click on the branch you would like to publish snaps for
1. In a new tab or window, go to the [snap name registration page](https://dashboard.snapcraft.io/dev/snaps/register-name/), signing in with the account you created at Launchpad
1. Type the name of your application in the "Snap name" field, then click on the "Register and proceed to upload" button
1. Close this tab and return to the branch page on Launchpad
1. Under the "Related snap packages" heading, click "Create snap package"
1. In the "Name" field, enter a name for the Launchpad snap recipe (if in doubt, use the same name you used on the snap name registration page)
1. Under "Processors", select any hardware architectures you wish to build snaps for
1. Check the box for "Automatically build when branch changes"
1. Check the box for "Automatically upload to store"
1. Enter the name of your application in the "Registered store package name" field
1. Under "Store channels" select "Edge"
1. Click "Create snap package"

Congratulations, you're all set. Four times a day Launchpad will check to see if any new commits have been pushed to your GitHub repository and will both build and publish snaps of them to the [edge channel](/reference/channels).

Your system can then automatically refresh this snap to the latest version, up to four times a day. To set that up, run `snap install --edge <snap name>`.
