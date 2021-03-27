# ClickHouse RPMs and SRPMs for RHEL8\CentOS8

**Unofficial** ClickHouse RPMs and SRPMs for RHEL 8 \ CentOS 8 \ Oracle Linux 8 \ Alma Linux 8 \ Rocky Linux 8 and other derivatives of RHEL 8.

Natively built on CentOS 8 from a SPEC file for x86_64 and aarch64. Uses the OS libraries when possible and safe to do so. Requires the EPEL repository.
The server RPM includes a systemd service (clickhouse-server). Just install and start using :-)

You can find the RPMs and the SRPMs here:

#### ClickHouse \*-stable repository: https://download.opensuse.org/repositories/home:/mastertheknife:/clickhouse-stable/CentOS_8/
#### ClickHouse \*-lts repository: https://download.opensuse.org/repositories/home:/mastertheknife:/clickhouse-lts/CentOS_8/

Please note that sometimes the LTS contains a newer version than the stable. For example, as of this writing, latest LTS is 21.3 and latest stable is 21.2.

I originally created these for my own use, but given the effort of creating it and maintaining it, its worth sharing :-)
The RPMs are built on OpenSUSE's excellent OBS (Open Build Service).
If you are interested in the OBS projects, they're here:
https://build.opensuse.org/package/show/home:mastertheknife:clickhouse-stable/ClickHouse
https://build.opensuse.org/package/show/home:mastertheknife:clickhouse-lts/ClickHouse

### If you want to build the RPMs yourself:

This currently requires CentOS Stream 8 to build, because of the newer cmake version.
Also requires dwz 0.14 or newer, because dwz 0.12 and 0.13 crash due to the large size of debuginfo. dwz 0.14 for EL8 can be found here:
https://download.opensuse.org/repositories/home:/mastertheknife/CentOS_8/

The source .tar.xz was created as follows:
```
git clone git@github.com:clickhouse/clickhouse.git --branch v21.2.5.5-stable --depth 1 clickhouse-21.2.5.5
cd clickhouse-21.2.5.5
git submodule update --init --recursive --depth=1
git rev-parse HEAD > src-git-head.txt
git submodule foreach --recursive git rev-parse HEAD > src-git-submodule-heads.txt
rm -rf .git
cd ..
XZ_OPT="-9 -e" tar cvJf clickhouse-21.2.5.5.tar.xz clickhouse-21.2.5.5
```