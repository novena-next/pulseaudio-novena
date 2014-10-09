pulseaudio-novena
=================

Support files required to build a Debian package that adds support for Novena to Pulseaudio.

Building
------------

To build the package, run "git-buildpackage [tag]" where [tag] is a valid upstream tag,
such as v1.0.  You might also need to add -uc -us if building an unsigned package.  E.g.:

    git-buildpackage -us -uc --git-upstream-tag=v1.0


Installation
------------

To install, simply use dpkg to install the resulting .deb package.


Config Notes
-----

Debian ships a pulseaudio config file that enables ts, which in theory provides lower
power consumption.  For reasons we have not yet been able to determine, this is broken
on the i.MX6 audio codecs.  To workaround this, we set tsched=0 in default.pa.  In order
to ship this custom default.pa config file, we divert the existing default.pa.


Udev Notes
----------

PulseAudio supports adding udev variables to control which alsa profile is loaded.
In order to take advantage of this, we ship a custom udev rule.


Profile Notes
-------------

The audio codec chip used in Novena is an ES8328, which has two outputs: Output 1 and
Output 2.  The ruleset is required to allow headphone detection to work, so that
the speakers (Output 2) are muted when headphones are plugged in.
