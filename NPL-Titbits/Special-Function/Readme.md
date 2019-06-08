# Special Function Construct

The Special Function construct is used to define the interface to a target architecture IP block. The internal functionality of the IP block is not specified in the NPL. The interface definition of the IP block must be provided by target vendor using template methods. The NPL writer calls the IP block in the program by using the defined template methods and using appropriate arguments. The ```special_function``` is an extensible construct where target vendor can add custom methods.


## Special Function Example 
We have created an example to illutrate how to connect an IP block with the rest of the NPL logic functions. 'sf_timestamping' program uses 'special function' to connect LINUX C function to get the time-of-day information for every packet and print the timestamping value out on the BM console.

To execute this example, follow below steps

1. Make sure [build environment](https://github.com/nplang/NPL-Tutorials#npl-build-enivronment) was properly setup as described earlier
2. Once the environmental variables were setup execute below commands. 
````

export NPL_EXAMPLES=/home/npl/ncsc-1.3.3rc3/examples/npl_tidbits/constructs
cd $NPL_EXAMPLES/packet_trace
make fe_nplsim
make nplsim_comp
make nplsim_run

````

Now you will see two xterm windows one with name ```BMODEL``` and another with ```BMCLI```. 

You can now inject packet using below command  from original console widow where you compiled the NPL code. 

````
python bm_tests/corp_net/testPkt.py

````

The above testPkt.py sends 5  packets to port-0 of the Behavioral Model

````

Test - 1 :
Ingress Packet : Sends 5 packets with interval of 1 sec for each packet.
Observations on BMODEL Window : BM window prints out the timestamping of each packets based on the time of the system.


````

You can experience complete NPL programs for this example located at below location

````

$NPL_EXAMPLES/editor/special_function/npl/sf_timestamping.npl

````

## Next Tutorial 

Congratulations !!
You have experienced how ```special_function``` construct work. You can now move on to next example [Strength Construct](https://github.com/nplang/NPL-Tutorials/blob/master/NPL-Titbits/Strength)
