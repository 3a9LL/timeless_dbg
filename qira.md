QIRA
=============
Installation on Debian/Ubuntu
------------------------------
```
wget -qO- https://github.com/BinaryAnalysisPlatform/qira/archive/v1.2.tar.gz | tar zx
cd qira-1.2
./install.sh
```

Installation Extras
--------------------
* ./fetchlibs.sh will fetch the libraries for i386, armhf, armel, aarch64, mips, mipsel, and ppc
* ./tracers/pin_build.sh will install the QIRA PIN plugin, allowing --pin to work

IDA plugin
---------------
Install the plugin in ~/qira/ida/bin after building. Or just copy ~/qira/ida/python/qira.py to IDA plugins.

Installation on Windows (experimental)
--------------------------------------
* Install git and python 2.7.9
* Upgrade pip
```
python -m pip install --upgrade pip
```
* Install [vcpython27](http://aka.ms/vcpython27)
* Clone
```
git clone https://github.com/BinaryAnalysisPlatform/qira.git
cd qira
```
* Extract header files from [zip](https://storage.googleapis.com/google-code-archive-downloads/v2/code.google.com/msinttypes/msinttypes-r26.zip) to ./qiradb/qiradb (inttype.h)
* Run
```
C:\Python27\Scripts\pip.exe install --upgrade html ^
   flask-socketio pillow pyelftools socketIO-client ^
   pydot ipaddr capstone-windows ./qiradb
```
* Install [gevent](https://pypi.python.org/pypi/gevent#downloads)
