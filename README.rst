New version available
======================

This version (Fairbrix 0.3.27.78) is outdated and should no longer be used.

A new version is here: https://github.com/wiggi/fairbrix-0.8-coincontrol



Old readme for Fairbrix 0.3
============================

Fairbrix - a cryptocurrency optimized for CPU mining using scrypt as a proof of work scheme.
 - 5 minute block targets
 - 25 coins per block (constant forever)
 - 2016 blocks (1 week) to retarget difficulty
This version (Fairbrix 0.3.27) is based on on multicoin-QT.



ATTENTION!!!
DON'T FORGET TO PLACE fbx.conf into your APPDATA or default fairbrix folder (%APPDATA%\fairbrix on Win, ~/.fairbrix/ on Unixes)

The port and portsend value are 8591 by default. So you may want to open that port on your router.



Fairbrix 0.3.x known bugs:

- Linux: daemon being set to 1 seems to mess with Linux users on Ubuntu and some others. If getting segfaults use daemon=0.
- Windows qt-client: unresponsive while sending large transactions (can take several minutes)
- Windows qt-client: ignores newly available connections if already running
- Windows qt-client: not displaying UI after being minimized
  (it doesn't actually crash, double click on notification area symbol to "wake it up" again)
- normally hidden "change" part of transactions visible in transactions list
  after restoring old (>100 transactions/mined blocks) wallet backup

IMPORTANT! Windows users benefit from having both Daemon and Server set to 1 (far more responsive GUI)



Build instructions 
===================

Debian
-------

First, make sure that the required packages for Qt4 development of your
distribution are installed, for Debian and Ubuntu these are:

::

    apt-get install qt4-qmake libqt4-dev build-essential libboost-dev libboost-system-dev \
        libboost-filesystem-dev libboost-program-options-dev libboost-thread-dev \
        libssl-dev libdb++-dev

then execute the following:

::

    qmake
    make

Alternatively, install Qt Creator and open the `bitcoin-qt.pro` file.

An executable named `bitcoin-qt` will be built.


Windows
--------

Windows build instructions:

- Download the `QT Windows SDK`_ and install it. You don't need the Symbian stuff, just the desktop Qt.

- Download and extract the `dependencies archive`_  [#]_, or compile openssl, boost and dbcxx yourself.

- Copy the contents of the folder "deps" to "X:\QtSDK\mingw", replace X:\ with the location where you installed the Qt SDK. Make sure that the contents of "deps/include" end up in the current "include" directory and such.

- Open the .pro file in QT creator and build as normal (ctrl-B)

.. _`QT Windows SDK`: http://qt.nokia.com/downloads/sdk-windows-cpp
.. _`dependencies archive`: http://download.visucore.com/bitcoin/qtgui_deps_1.zip
.. [#] PGP signature: http://download.visucore.com/bitcoin/qtgui_deps_1.zip.sig (signed with RSA key ID `610945D0`_)
.. _`610945D0`: http://pgp.mit.edu:11371/pks/lookup?op=get&search=0x610945D0

Berkely DB version warning
==========================

A warning for people using the *static binary* version of Bitcoin on a Linux/UNIX-ish system (tl;dr: **Berkely DB databases are not forward compatible**).

The static binary version of Bitcoin is linked against libdb4.7 or libdb4.8 (see also `this Debian issue`_).

Now the nasty thing is that databases from 5.X are not compatible with 4.X. 

If the globally installed development package of Berkely DB installed on your system is 5.X, any source you
build yourself will be linked against that. The first time you run with a 5.X version the database will be upgraded, 
and 4.X cannot open the new format. This means that you cannot go back to the old statically linked version without
significant hassle!

.. _`this Debian issue`: http://bugs.debian.org/cgi-bin/bugreport.cgi?bug=621425
