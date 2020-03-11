# OpenCL Tutorials

Parallel Programming OpenCL tutorials running on Ubuntu16.04, Intel GPU and make. 


## Install instuctions for Ubuntu 16.04 on Intel HD series GPU:

```
#install generic user-end OpenCL APIs
sudo apt install ocl-icd-libopencl1 opencl-headers clinfo

#install Intel HD Graphics series GPU specific implementation of CL
add-apt-repository ppa:intel-opencl/intel-opencl
apt-get update
apt-get install intel-opencl-icd

#install helper libraries used in these tutorials
sudo apt install cimg-dev libcompute-dev

```

## Tips to find out how to do similar install on other systems:
```
To test if CL is already installed and working:
clinfo
	Numnber of processors: 0

To find graphics card/s make and model:
lspci | grep VGA
00:02.0 VGA compatible controller: Intel Corporation Device 591b (rev 04)

sudo lshw -C display
[sudo] password for charles: 
  *-display UNCLAIMED     
       description: Display controller
       product: Advanced Micro Devices, Inc. [AMD/ATI]
       vendor: Advanced Micro Devices, Inc. [AMD/ATI]
       physical id: 0
       bus info: pci@0000:01:00.0
       version: c0
       width: 64 bits
       clock: 33MHz
       capabilities: pm pciexpress msi bus_master cap_list
       configuration: latency=0
       resources: memory:a0000000-afffffff memory:b0000000-b01fffff ioport:e000(size=256) memory:ec400000-ec43ffff memory:ec440000-ec45ffff
  *-display
       description: VGA compatible controller
       product: Intel Corporation
       vendor: Intel Corporation
       physical id: 2
       bus info: pci@0000:00:02.0
       version: 04
       width: 64 bits
       clock: 33MHz
       capabilities: pciexpress msi pm vga_controller bus_master cap_list rom
       configuration: driver=i915 latency=0
       resources: iomemory:2f0-2ef irq:132 memory:eb000000-ebffffff memory:2fa0000000-2fafffffff ioport:f000(size=64) memory:c0000-dffff

Then look up the card on the net for CL compatability and power:
	Intel 591b part of the "HD Graphics 630" series. 
	591b is the version for mobile laptops etc.
	("HD Graphics 630" is part of "gen9" Intel GPUs)
	https://en.wikipedia.org/wiki/List_of_Intel_graphics_processing_units
		should run OpenCL 2.1 for Linux
		clock 350-1000MHz
		core config 192:24:3 (GT2)

If compatible, find and install an OpenCL runtime for the particular card:

	Intel OpenCL runtimes download:
		https://software.intel.com/en-us/articles/opencl-drivers
			"Intel® Graphics Technology Runtimes"  -- is for "HD Graphics series"
			-- Linux OS
		points to here to install:
		https://github.com/intel/compute-runtime/blob/master/documentation/Neo_in_distributions.md

	which says to do
		add-apt-repository ppa:intel-opencl/intel-opencl
		apt-get update
		apt-get install intel-opencl-icd
	then clinfo works.
```

## About OpenCL verions
The single file CL/cl2.hpp contains bindings for ALL of the 1.0, 1.2 and 2.0 APIs.

There are ways to specify which APIs will be used:  https://github.khronos.org/OpenCL-CLHPP/

CL1.2 ref card:  https://www.khronos.org/files/opencl-1-2-quick-reference-card.pdf

The tutorial base codes use OpenCL1.2 API, via the cl2.hpp emulation layer. (This hpp is provided on ubuntu by the opencl-headers package.)

Tutes 2 and 4 need the CImg and Boost.compute libraries to be installed.

```
