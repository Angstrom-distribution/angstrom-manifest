angstrom-manifest
=================

Ångström Repo manifest repository

These are the setup scripts for the Ångström buildsystem. If you want to (re)build packages or images for Ångström, this is the thing to use.
The Ångström buildsystem is using various components from the Yocto Project, most importantly the Openembedded buildsystem, the bitbake task executor and various application and BSP layers.

To configure the scripts and download the build metadata, do:

	$ mkdir ~/bin
	$ PATH=~/bin:$PATH

	$ curl http://commondatastorage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
	$ chmod a+x ~/bin/repo

Run repo init to bring down the latest version of Repo with all its most recent bug fixes. You must specify a URL for the manifest, which specifies where the various repositories included in the Android source will be placed within your working directory.

	$ repo init -u git://github.com/Angstrom-distribution/angstrom-manifest

To check out a branch other than "master", specify it with -b:

	$ repo init -u git://github.com/Angstrom-distribution/angstrom-manifest -b angstrom-v2015.12-yocto2.0

When prompted, configure Repo with your real name and email address.

A successful initialization will end with a message stating that Repo is initialized in your working directory. Your client directory should now contain a .repo directory where files such as the manifest will be kept.

To pull down the metadata sources to your working directory from the repositories as specified in the default manifest, run

	$ repo sync

When downloading from behind a proxy (which is common in some corporate environments), it might be necessary to explicitly specify the proxy that is then used by repo:

	$ export HTTP_PROXY=http://<proxy_user_id>:<proxy_password>@<proxy_server>:<proxy_port>
	$ export HTTPS_PROXY=http://<proxy_user_id>:<proxy_password>@<proxy_server>:<proxy_port>

More rarely, Linux clients experience connectivity issues, getting stuck in the middle of downloads (typically during "Receiving objects"). It has been reported that tweaking the settings of the TCP/IP stack and using non-parallel commands can improve the situation. You need root access to modify the TCP setting:

	$ sudo sysctl -w net.ipv4.tcp_window_scaling=0
	$ repo sync -j1


Setup Environment
-----------------
	$ . setup-environment

	$ MACHINE=<machine> bitbake <image>
	e.g. MACHINE=beaglebone bitbake systemd-image

Creating a local topic branch
-----------------------------

Setup will already create a branch called $USER/work
but if you need to create local branches for all repos which then can be done e.g.

	$ ~/bin/repo start myangstrom --all

Where 'myangstrom' is the name of branch you choose

Updating the sandbox
--------------------

Setup will do this as well but in between if you need to bring changes from upstream then
use following commands

	$ repo sync

Rease your local committed changes

	$ repo rebase


If you find any bugs please report them here

https://github.com/Angstrom-distribution/angstrom-manifest/issues

If you have questions or feedback, please subscribe to

http://lists.linuxtogo.org/cgi-bin/mailman/listinfo/angstrom-distro-devel

Ångström Distribution maintainers
---------------------------------

* Koen Kooi <mailto:koen@dominion.thruhere.net>
* Khem Raj  <mailto:raj.khem@gmail.com>
