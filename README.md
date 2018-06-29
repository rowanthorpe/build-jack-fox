build-jack-fox
==============

An automation script for downloading, customizing and building (on Debian or a derivative distro) a version of the latest
Firefox browser with Jack audio (so you don't need to install PulseAudio, for example).

As it seems Mozilla and Debian won't likely compile Jack in by default anytime soon, for the sake of hard-disk space usage,
compile-times, hardware longevity, and sanity you can also configure to tweak the following:

* set the list of locales to build so you don't need to build *all* of them
* prevent building and running tests

For background and motivation for this script, see
[my blogpost](https://blog.rowanthorpe.com/2017/12/17/firefox-without-pulseaudio-in-debian.html).

Installation (optional)
-----------------------

* If you want any flags hardcoded so you don't need to specify them every time, do:
  ```sh
  cd [repo-dir]
  cp build-jack-fox-conf.sh.template build-jack-fox-conf.sh
  ```
  and uncomment/edit them, for example:
  ```text
  --enable-install --> install=1
  ```
  ```text
  --jack-dev-pkg "libjack-dev" --> jack_dev_pkg=libjack-dev
  ```
* If you want to make the script available in your $PATH, do e.g.:
  ```sh
  ln -s [repo-dir]/build-jack-fox /usr/local/bin/
  ```
* NB: You will need at least about 15GB free on the partition housing the $srcdir (for the built files, and the copies
  made while packaging).

Invocation
----------

Do one of the following (the latter if you installed the script into your $PATH):

* `[repo-dir]/build-jack-fox [FLAGS]`
* `build-jack-fox [FLAGS]`

Documentation
-------------

I will add proper documentation at some point, but for now run `[path-to-repo]/build-jack-fox --help` for a list of
optflags and varflags.

Issues
------

* I was [pointed to an issue where version 59 audio fails](https://twitter.com/malkavianbilbao/status/974698569331625984)
  due to the sandbox blocking `bind()`. Apparently for v59 the only workaround is to set `security.sandbox.content.level=0`
  in `about:config` (which is not a good idea unless you really understand the consequences), but luckily due to an
  architectural change the issue doesn't affect v60 onwards
  ([confirmed OK](https://twitter.com/malkavianbilbao/status/997162915240316933) now that v60 is out in Debian Unstable).
  Personally, I just waited and jumped from version 58 to 60.

Authors
-------

Rowan Thorpe <rowan@rowanthorpe.com>

License
-------

GPLv3+ - see COPYING for details.

TODO
----

* "uninstall build-deps-package" step at end (opt-in)
* documentation
* use `die()` in more places instead of just letting `set -e` handle errors silently.
* add optional/configurable step to the install-phase, to mark the installed packages
  as "held" so they won't get auto-replaced by upstream newer versions
