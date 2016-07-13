Build From Sources
-------------------
Ubuntu/Debian

    sudo apt-get install ccache cmake make g++-multilib gdb \
      pkg-config libz-dev realpath python-pexpect manpages-dev git zlib1g-dev

then
```
mkdir rr
cd rr
git clone https://github.com/mozilla/rr.git
mkdir obj
cd obj
```
Then to use `make` and the system default compiler to build:

    cmake rr
    make -j8
    make test

Or to use clang and Ninja to build (faster!):

    CC=clang CXX=clang++ cmake -G Ninja ../rr
    ninja-build
    ninja-build test

Or in Debian/Ubuntu
---------------------
```
cd /tmp
wget https://github.com/mozilla/rr/releases/download/4.3.0/rr-4.3.0-Linux-$(uname -m).deb
sudo dpkg -i rr-4.3.0-Linux-$(uname -m).deb
```

Hardware/software requirements
----------------------------------
Supported microarchitectures are Intel architectures newer than Merom and Penryn, i.e. Nehalem and beyond

`/proc/sys/kernel/perf_event_paranoid` must be &lt;= 1 for rr to work efficiently. Some distros set it to 2 or higher, in which case you either need to set it to 1 or use `rr record -n`, which is slow.
```
echo 'kernel.perf_event_paranoid = 1' | sudo tee -a /etc/sysctl.conf
sudo sysctl -p
```
On Ubuntu/Debian set governor to 'performance'
```
apt-get install cpufrequtils
sudo sed -i 's/^GOVERNOR=.*/GOVERNOR="performance"/' /etc/init.d/cpufrequtils
for ((i=0;i<$(nproc);i++)); do cpufreq-set -c $i -r -g performance; done
```
If you run rr in a virtual machine, **MAKE SURE VIRTUALIZATION OF PERF COUNTERS IS ENABLED**. The virtual machines that do work with rr and the settings required are listed below. If a virtual machine isn’t on this list, then it cannot be used with rr.

* VMWare Workstation 9 / Fusion 7: The default is for counter virtualization to be *disabled*. You have to enable it in the VM settings (ad
pandoc 1.17.1
* Qemu: On QEMU command line use
 `-cpu host`
* Libvirt/KVM: Specify CPU passthrough in domain XML definition:
 ```
 <cpu mode='host-passthrough'/>
 ```
* Digital Ocean: The only VPS provider known to work with RR.
