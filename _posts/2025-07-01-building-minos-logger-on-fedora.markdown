### [Building Minos logger on Fedora](https://m0wdt.blogspot.com/2025/07/building-minos-logger-on-fedora.html)

I have been using Fedora linux for a while now I use The Qlog flatpak
 for general logging, it does have a contest mode but it cannot export 
to the .edi format that makes submitting VHF contest logs to the RSGBcc 
quite easy. 

On windows many operators use [Minos](https://minos.sourceforge.net/) which I think is a great VHF contest logger.

I could not find any packages on any distro for this logger but there are instructions on how to build on Ubuntu. 

Now I am only a beginner on linux so beware of following these instructions, it has not broken my system as far as I know but follow this at your own risk.

To build Minos on Fedora 42 KDE open the [builing for linux](https://sourceforge.net/p/minos/minos/ci/master/tree/Building%20Minos%20-%20Linux.txt#l57) instructions and follow along with the changes below.

Start at initial setup but skip the raspberrypi part.

If git isn't installed, you need to install it:

```
dnf install git
```

Go to your home directory and check out Minos

```
git clone git://git.code.sf.net/p/minos/minos Minos2
```

Then, so that you get the latest release rather than the "bleeding edge" source code

```
cd Minos2
git checkout Mqt_Release_2.7.x.x
```

Follow the instructions to make Hamlib.

Now this is where the process changes for Fedora.

The provided tools.sh is intended for debian based systems with their package names which are quite different. Below is the version of tools.sh that I used. I suggest you save this in the same directory with a different filename.  You will need to run the script with sudo.

```
#!bin/bash

#Install dependancies to build Minos2 2.7.1.0 logger on Fedora KDE edition
dnf -y install git
dnf -y install libtool #depends on automake

dnf -y install cmake
dnf -y install make

#build-essential on fedora is group development-tools
dnf -y install @development-tools
dnf -y install qtchooser
dnf -y install qt-creator
dnf -y install qt5-qtbase
dnf -y install qt5-qtbase-devel
dnf -y install qt5-qttools
dnf -y install qt5-qttools-devel
dnf -y install qt5-qtserialport
dnf -y install qt5-qtserialport-devel
dnf -y install qt5-qtcharts
dnf -y install qt5-qtcharts-devel
dnf -y install qt5-qtdeclarative
dnf -y install qt5-qtquickcontrols2
dnf -y install qt5-qtlocation
dnf -y install mesa-libGLU-devel
dnf -y install alsa-lib-devel
dnf -y install qt5-qtmultimedia-devel
```

Continue following the "Building Minos" instructions in the [builing for linux](https://sourceforge.net/p/minos/minos/ci/master/tree/Building%20Minos%20-%20Linux.txt#l57) document but before you run ./buildInstall.sh you need to edit line 31 
on this file and replace qmake with qmake-qt5 which should look like 
this

```
qmake-qt5 $QMAKEPARAM ../../mqt/mqt.pro
```

If successfull you should be asked if you would like to copy the runtime and configs, press y for each.
You can then start Minos with the following command:

```
~/runtime/Minos.sh &
```

I posted this as a record I can follow myself when I inevitably forget how I did it, hopefully  it wil help someone else too.

Good luck!

<sub>July 2025 - Initial post</sub>

<sub>Feb 2026 - Small edits and rebuilt again to confirm  this still works.</sub>
