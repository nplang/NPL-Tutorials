# Packet Trace Construct

Packet Drop Construct helps NPL program to trace the packet for debugging and also to understand the resolution logic.

## Packet Trace Example 
This example is used to trace a packet (copy to cpu or other ports).
In this example, packets with IP_OPTION are traced by calling packet_trace() construct.


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

The above testPkt.py sends the following packets to port-0 of the Behavioral Model

````
Test - 1 :
Ingress Packet : Send a packet with ip options from port-0 to BM
Observations on BMODEL Window : BM window prints out packet_trace() construct is calling
Receive a packet from port-1

Test - 2 :
Ingress Packet : Send a normal packet With out ip options from port-0 to BM
Observations on BMODEL Window : Receive a packet from port-1

````

You can experience complete NPL programs for this example located at below location

````

$NPL_EXAMPLES/editor/packet_trace/npl/packet_trace.npl

````

## Next Tutorial 

Congratulations :+1:

You have just finished NPL Basic Examples. 

Please proceed to [Packet Forwarding Examples](https://github.com/nplang/NPL-Example-Applications)
