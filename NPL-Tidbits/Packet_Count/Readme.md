# Packet Count Construct

Packet Counter Construct helps NPL program to implement packet Counting mechanism.

## Packet Count Example 

We have devenloped a simple example to count multicast packets. A counter will be incremented for every incoming packet with 40th bit set in destination mac-address.

To execute this example, follow below steps

1. Make sure [build environment](https://github.com/nplang/NPL-Tutorials#npl-build-enivronment) was properly setup as described earlier
2. Once the environmental variables were setup execute below commands. 
````

export NPL_EXAMPLES=/home/npl/ncsc-1.3.3rc4/examples/npl_tidbits/constructs
cd $NPL_EXAMPLES/packet_count
make fe_nplsim
make nplsim_comp
make nplsim_run

````

Now you will see two xterm windows one with name ```BMODEL``` and another with ```BMCLI```. 

You can now inject packet using below command from original console widow where you compiled the NPL code. 

````
python bm_tests/corp_net/testPkt.py

````

The above testPkt.py sends the following packets to port-0 of the Behavioral Model

````
Test - 1 :
Ingress Packet : Send a UC packet through port-0 of BM.
Observations on BMODEL window: BM window will not print out “Calling packet_count”

Test - 2 :
Input : Send a MC packet through port-0 of BM.
Observations on BMODEL window:: BM window print out “Calling packet_count”

````

You can experience complete NPL programs for this examples located at below location

````

$NPL_EXAMPLES/editor/packet_count/npl/packet_count.npl

````

## Next Tutorial 

Congratulations :+1:

You have experienced how ```Packet Count``` construct work. You can now move on to next example [Packet Drop](https://github.com/nplang/NPL-Tutorials/tree/master/NPL-Tidbits/Packet-Drop)
