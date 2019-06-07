# NPL Tutorials


## Introduction
Welcome to NPL Hands-On tutorial. 
To help you better understand NPL language and its powerful constructs we have developed NPL Tutorials. These tutorials are catogerized into two sets. 

### [NPL Titbits](https://github.com/nplang/NPL-Tutorials/blob/master/NPL-Titbits)
   These are simple and comprehensive examples to understand constructs in NPL language.
### [Basic Switch Forwarding](https://github.com/nplang/NPL-Example-Applications) 
   These are switch forwarding examples to make you experience a very simple Layer2 and Layer3 flows.
   
### How to get a Working Environment

To accelerate your experiernce on Hands-on tutorial, we prepared complete test environment in a virtual machine. 

Steps to use  Virtual Machiene. 
- Downlaod [VirtualBox](http://www.oracle.com/technetwork/server-storage/virtualbox/downloads/index.html)
- Import virtual appliance File VritualBox Manager [ova]link
- Power on  appliance after importing OVA file. Appliance is built using Ubuntu Linux 16.04
- You will be prompted for a password which is "npl"

### Quick Introduciton to Working Environment

#### Directory Structure

Each example is written as an individual application. All examples are sharing similar subdirectories as shown below. 
The major directories include:

- bm_tests
      It provides the testPkt.py for generating packets to test this example
- npl
      The example written in NPL language

``` 
npl@npl-VirtualBox:~/ncsc-1.3.3rc3/examples/npl_tidbits/constructs/bus$ tree
.
├── bm_tests
│   ├── corp_net
│   │   └── testPkt.py
│   └── sf_definition
│       └── bm_sfc.cpp
├── Makefile
├── npl
│   ├── base_helper.npl
│   ├── bus.npl
│   └── config.ini
└── README

4 directories, 7 files
npl@npl-VirtualBox:~/ncsc-1.3.3rc3/examples/npl_tidbits/constructs/bus$
````
#### NPL Build Enivronment
Steps to be followed
 ```
 
 sudo bash
   Password is “npl”
 cd ~/ncsc-1.3.3rc3
 source ./bin/setup.sh
 
 ```
Once the environment is ready, follow the below steps to build and run the NPL examples.

```

export NPL_EXAMPLES=/home/npl/ncsc-1.3.3rc3/examples/npl_tidbits/constructs
cd $NPL_EXAMPLES/<construct_name> 
make fe_nplsim
make nplsim_comp
make nplsim_run

```

```nplsim_run``` will open couple of xterm windows. ``` BMODEL``` and ```BMCLI```. BMODEL is a behavior simulated model and BMCLI is a "bheavior model CLI" which helps to populate table entries for verification. 

``` NOTE: Those two windows might be overlapped. If you don’t see all of them after “make nplsim_run”, please drag and move the window to get access to the windows underneath.```


