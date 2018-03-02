build-jack-fox
==============

An automation script for downloading, customizing and building (on Debian or a derivative distro) a version of the latest
Firefox browser with Jack audio (so you don't need to install PulseAudio, for example).

It also allows you to set a small list of additional locales to build, so you don't need to sit through building all of
them. Soon it will eliminate building and running tests too. These are for convenience only, as it seems Mozilla and Debian
won't likely compile Jack in by default anytime soon, so the tweaks are an attempt to keep the compile times down for the
sake of my poor laptop.

I will add proper documentation soon, but for now cd to the repo directory and run `./build-jack-fox --help` for a list of
optflags and varflags. Each flag can be specified equivalently in `build-jack-fox-conf.sh` to override the builtin defaults
(like `--enable-install` -> `install=1`, or `--jack-dev-pkg "libjack-dev"` -> `jack_dev_pkg=libjack-dev`). To run the
script without specifying the full-path, you can do e.g. `ln -s [github-repo-dir]/build-jack-fox /usr/local/bin/` and then
just do `build-jack-fox [flags] ...`.

For background and motivation for this script, see [my blogpost](http://blog.rowanthorpe.com/2017/12/17/firefox-without-pulseaudio-in-debian.html).

Authors
-------

Rowan Thorpe <rowan@rowanthorpe.com>

License
-------

GPLv3+ - see COPYING for details.

TODO
----

* use `die()` in more places instead of just letting `set -e` handle errors silently.
* remove compiling/running of tests for faster build
