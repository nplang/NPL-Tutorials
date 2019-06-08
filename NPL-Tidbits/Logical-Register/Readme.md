# Logical Register Construct

The Logical Register construct is used to specify a one deep, multi-field entity.
``` logical_register ``` provides an interface to software to setup controls. Unlike logical table, a logical register has no lookup key. Fields can be initialized at compile time, or populated at run time.


## Logical Register Example 

We have created an couple examples to illustrate how to use NPL's ```logical_register``` construct.

### Example 1 (Ingress Packet Counter)
This example implements a simple ingress packet counter. A 32-bit packet counter is implemented as ```logical_register``` which is incremented for each ingress packet.

To execute this example, follow below steps

1. Make sure [build environment](https://github.com/nplang/NPL-Tutorials#npl-build-enivronment) was properly setup as described earlier
2. Once the environmental variables were setup execute below commands. 
````

export NPL_EXAMPLES=/home/npl/ncsc-1.3.3rc3/examples/npl_tidbits/constructs
cd $NPL_EXAMPLES/logical_register/reg_pkt_count
make fe_nplsim
make nplsim_comp
make nplsim_run

````

Now you will see two xterm windows one with name ```BMODEL``` and another with ```BMCLI```. You can now inject packet using below command  from original console widow where you compiled the NPL code. 

````
python bm_tests/corp_net/testPkt.py

````

The above testPkt.py injects 5 packets to port-0 of the Behavioral Model

On the BMODEL window you will see prints ```` ing_pkt_count```` getting incremented for each packet thats been sent. 


### Example 2  (TPID for parsing)

This NPL program implements simple configurable 'tag protocol identifier' (TPID) for parsing VLAN tagged packets. It supports four TPIDs. Multiple TPIDs can be selected for identifying tagged status of incoming packet. 

It implements this using registers:
tpid_enable: 4-bit value. Indicates valid tpid values.
tpid_values: 4 * 16-bit TPID values. (ex: 0x8100)

To execute this example, follow below steps

1. Make sure [build environment](https://github.com/nplang/NPL-Tutorials#npl-build-enivronment) was properly setup as described earlier
2. Once the environmental variables were setup execute below commands. 
````

export NPL_EXAMPLES=/home/npl/ncsc-1.3.3rc3/examples/npl_tidbits/constructs
cd $NPL_EXAMPLES/logical_register/reg_tpid
make fe_nplsim
make nplsim_comp
make nplsim_run

````

Now you will see two xterm windows one with name ```BMODEL``` and another with ```BMCLI```. You can now inject packet using below command  from original console widow where you compiled the NPL code. 

````
python bm_tests/corp_net/testPkt.py

````

The above testPkt.py sends  the following packet to port-0 of the Behavioral Model
````

Test - 1:
Ingress Packet : Send tagged packet with VID=1 through port-0 of BM.
Egress Packet : Tag status of the packet and vlan-id are printed on BM console.

Ingress Packet : Send untagged packet through port-0 of BM.
Egress Packet : Tag status of the packet is printed on BM console.

````
On the BMODEL window you will see prints that display ingress and egress packets.

You can experience complete NPL programs for this examples located at below location

````

$NPL_EXAMPLES/editor/logical_register/reg_pkt_count/npl/reg_pkt_count.npl
$NPL_EXAMPLES/editor/logical_register/reg_tpid/npl/reg_tpid.npl


````

## Next Tutorial 

Congratulations !!

You have experienced how ```Logical Register``` construct work. You can now move on to next example [Logical Table](https://github.com/nplang/NPL-Tutorials/blob/master/NPL-Tidbits/Logical-Table)
