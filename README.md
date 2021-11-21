# DKMS bnx2x with 2.5G patches

Based on the Debian 5.10.0-9 kernel package (Linux kernel 5.10.70), and the work from JAMESMTL:
https://www.dslreports.com/forum/r32440802-
https://raw.githubusercontent.com/JAMESMTL/snippets/master/bnx2x/patches/bnx2x_warpcore+8727_2_5g_sgmii.patch

**Not tested with any other kernels**

## Other versions

Please see https://github.com/severnt/bnx2x-2_5g-dkms/branches for branches for other kernel versions.

## Additional Changes
Added a module option that can be set to disable SFP TX fault detection:

`disable_sfp_tx_fault_detection`

To use, add a file to /etc/modprobe.d with the contents:

`options bnx2x disable_sfp_tx_fault_detection=1`

## Why DKMS
This driver doesn't seem to change too often. Instead of grabbing the full source and rebuilding, this will automatically rebuild the driver every time the kernel is updated.

## How to use DKMS
```sh
sudo apt-get update
sudo apt-get install dkms
cd /usr/src
sudo git clone -b debian11-5.10 https://github.com/severnt/bnx2x-2_5g-dkms.git bnx2x-99.1.713.36-0
sudo dkms add bnx2x/99.1.713.36-0
sudo dkms install bnx2x/99.1.713.36-0 -k $(uname -r)
```
Then it should rebuild every time you update your kernel.
