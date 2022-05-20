# Intel® Platform Monitoring Technology Backports

This repo holds backports of the pmt driver.

The driver is provided as a DKMS module targeting distinct
versions of various distros. Each backport is on a topic 
branch. Current support status is documented on the topic branch.

## Dependencies
This driver is part of a collection of kernel mode drivers 
that together enable support for Intel graphics. The backports 
collection within https://github.com/intel-gpu includes:

  - [i915](https://github.com/intel-gpu/intel-gpu-i915-backports) - The main graphics driver (includes a compatible DRM subsystem and dmabuf if necessary).
  - [cse](https://github.com/intel-gpu/intel-gpu-cse-backports) - Converged Security Engine
  - [pmt](https://github.com/intel-gpu/intel-gpu-pmt-backports) - Intel Platform Telemetry
  - [firmware](https://github.com/intel-gpu/intel-gpu-firmware) - Contains firmware required by i915.

Each project is tagged consistently so when pulling these repos pull the same tag.

## How to generate the DKMS module

### RHEL

#### Install dependencies:

Install packages

```
sudo dnf install \
   git \
   kernel-headers \
   make \
   rpm-build
```

Install dkms subsystem support:

```
git clone https://github.com/dell/dkms dkms
cd dkms
make install-redhat
```

#### Build and install dkms package
```
BUILD_VERSION=1 make -f Makefile.dkms dkmsrpm-pkg
```

The rpm package will be placed in $HOME/rpmbuild/RPMS/x86_64.
For example:

```
/home/user/rpmbuild/RPMS/x86_64/intel-platform-pmt-dkms-*.x86_64.rpm
```

To install, run:

```
cp $HOME/rpmbuild/RPMS/x86_64/*.rpm .
sudo dnf install intel-platform-pmt-dkms*.rpm
```
