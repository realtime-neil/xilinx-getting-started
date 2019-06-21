xilinx-getting-started
======================

This is what we're following: https://xilinx-wiki.atlassian.net/wiki/spaces/A/pages/18841738/Getting%2BStarted

This document references the Xilinx SDK version 2018.3 but will probably work
with other, later versions.

This document assumes the current working directory is the non-bare git
repository into which you've cloned out this project.

# Fetch Sources

https://xilinx-wiki.atlassian.net/wiki/spaces/A/pages/18842156/Fetch+Sources

The required sources are available as submodules in this repository. Cloning
out this repository implies that you have fetched all required sources. They
are repeated for convenience as follows:

> The following table gives an overview of the relevant repositories:
> Repository Name
> 	Content
> https://github.com/Xilinx/linux-xlnx.git
> 	The Linux kernel with Xilinx patches and drivers
> https://github.com/Xilinx/u-boot-xlnx.git
> 	The u-boot bootloader with Xilinx patches and drivers
> https://github.com/Xilinx/device-tree-xlnx.git
> 	Device Tree generator plugin for xsdk
> https://git.kernel.org/pub/scm/utils/dtc/dtc.git
> 	Device Tree compiler (required to build U-Boot)
> https://github.com/Xilinx/arm-trusted-firmware.git
> 	ARM Trusted Firmware (required for Zynq UltraScale+ MPSoC


# Build FSBL

https://xilinx-wiki.atlassian.net/wiki/spaces/A/pages/18841798/Build+FSBL

Use the shell script `build-fsbl` to generate the "First Stage Boot Loader"
into a lower directory:

    $ mkdir -vp fsbl
    $ ./build-fsbl -C fsbl ~/Downloads/zynq/zynq_linux.hdf

This script requires the xilinx tool `hsi`
in the `$PATH`. It also requires `gmake`. If you're missing `gmake` but have
`make`, then `build-fsbl` will create a temporary symlink for `gmake` to `make`
--- which `hsi` seems to swallow without incident.

# Build Device Tree Compiler (dtc)

https://xilinx-wiki.atlassian.net/wiki/spaces/A/pages/18841988/Build+Device+Tree+Compiler+dtc

This one is easy:

    $ make -C dtc

The tools that are built within that directory are required for later
steps. Xilinx would have you do...

    $ export PATH="${PWD}/dtc:${PATH}"

...but that's probably not necessary if you don't mind using longer paths in
your invocations.
