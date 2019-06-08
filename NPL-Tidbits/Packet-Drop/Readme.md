# Packet Drop Construct

Packet Drop Construct helps NPL program to implement packet Drop mechanism.

## Packet Drop Example 

We have implemented a simple 'packet_drop' program which validates mac-address. The program checks if incoming packet's source-mac-address (or) destination-mac-address are zero. If one of the values is zero then packet will be dropped.


To execute this example, follow below steps

1. Make sure [build environment](https://github.com/nplang/NPL-Tutorials#npl-build-enivronment) was properly setup as described earlier
2. Once the environmental variables were setup execute below commands. 
````

export NPL_EXAMPLES=/home/npl/ncsc-1.3.3rc3/examples/npl_tidbits/constructs
cd $NPL_EXAMPLES/packet_drop
make fe_nplsim
make nplsim_comp
make nplsim_run

````

Now you will see two xterm windows one with name ```BMODEL``` and another with ```BMCLI```. 

You can now inject packet using below command  from original console widow where you compiled the NPL code. 

````
python bm_tests/corp_net/testPkt.py

````

The above testPkt.py sends the following packets to port-0 of the Behavioral Model

````
Test - 1 :
Ingress Packet : Send a normal packet through port-0 of BM
Observations on BMODEL window: Egress Packet will be shown on console

Test - 2 :
Ingress Packet : : Send a MAC_SA=0 packet through port-0 of BM
Observations on BMODEL window : packet drop and drop_vector set to 1

Test - 3 :
Input : Send a MAC_DA=0 packet through port-0 of BM.
Observations on BMODEL window : packet drop and drop_vector set to 2

````

You can experience complete NPL programs for this example located at below location

````

$NPL_EXAMPLES/editor/packet_drop/npl/packet_drop.npl

````

## Next Tutorial 

Congratulations !!

You have experienced how ```packet_drop``` construct work. You can now move on to next example [Packet Trace](https://github.com/nplang/NPL-Tutorials/blob/master/NPL-Tidbits/Packet-Trace)
