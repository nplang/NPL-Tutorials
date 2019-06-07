# Editor Construct

Editor constructs are defined to
 - Add a new header using ```add_header``` construct
 - Delete a header from the packet using ```delete_header ``` construct
 - Modify header fields using ``` replace_header_field ``` construct
 - Create Checksum using ``` create_checksum ``` construct
 - Update packet Length using ``` update_packet_length ``` construct


## Editor Example 

We have created an couple examples to illustrate how to use NPL's 'editor' constructs and provides sandbox for experiments.

### Example 1 (L2 Tag Manipulation)
This example shows how to parse the incoming packet and edit Layer-2 headers. This NPL Program 
 - Parse incoming packet
 - Check for number of VLAN tags present in incoming packet
 - If incoming packet is double-tagged (or) single-outer-tagged then deletes outer tag from outgoing packet
 - If incoming packet is untagged (or) single-inner-tagged then adds outer tag to outgoing packet
 - Additionally, ethertype field in L2 header is modified

To execute this example, follow below steps

1. Make sure [build environment](https://github.com/nplang/NPL-Tutorials#npl-build-enivronment) was properly setup as described earlier
2. Once the environmental variables were setup execute below commands. 
````

export NPL_EXAMPLES=/home/npl/ncsc-1.3.3rc3/examples/npl_tidbits/constructs
cd $NPL_EXAMPLES/editor/editor_l2_tag 
make fe_nplsim
make nplsim_comp
make nplsim_run

````

Now you will see two xterm windows one with name ```BMODEL``` and another with ```BMCLI```. You can now inject packet using below command  from original console widow where you compiled the NPL code. 

````
python bm_tests/corp_net/testPkt.py

````

The above testPkt.py sends the following packets to port-0 of the Behavioral Model
````

Test - 1:
Ingress Packet : Send untagged packet from port-0
Egress Packet: Received packet is outer tagged, outer tpid is 0x8100

Test - 2:
Ingress Packet : Send single outer tagged packet from port-0
Egress Packet : Received packet is untagged 

Test - 3:
Ingress Packet : Send single inner tagged packet from port-0
Egress Packet : Received packet is double tagged, outer tpid is 0x8100, inner tpid is 0x9100

Test - 4:
Ingress Packet : Send double tagged packet from port-0
Egress Packet : Received packet is single inner tagged, tpid is 0x9100

````
On the BMODEL window you will see prints that display ingress and egress packets based on editor function changes in  NPL program.


### Example 2  (VxLAN Encapsulation & Decapsulation)

This program illustrates how to use NPL's ```editor``` constructs and provides sandbox for experiments. This NPL Program
 - Parse incoming packet
 - Checks for vxlan header in incoming packet
 - If incoming packet has vxlan header, deletes vxlan header from outgoing packet
 - If incoming packet does not have vxlan header then adds vxlan header to outgoing packet

To execute this example, follow below steps

1. Make sure [build environment](https://github.com/nplang/NPL-Tutorials#npl-build-enivronment) was properly setup as described earlier
2. Once the environmental variables were setup execute below commands. 
````

export NPL_EXAMPLES=/home/npl/ncsc-1.3.3rc3/examples/npl_tidbits/constructs
cd $NPL_EXAMPLES/editor/editor_vxlan
make fe_nplsim
make nplsim_comp
make nplsim_run

````

Now you will see two xterm windows one with name ```BMODEL``` and another with ```BMCLI```. You can now inject packet using below command  from original console widow where you compiled the NPL code. 

````
python bm_tests/corp_net/testPkt.py

````

The above testPkt.py sends the following packets to port-0 of the Behavioral Model
````

Test - 1:
Ingress Packet : Send a non-VXLAN packet from port-0
Egress Packet : Received packet is a VXLAN packet, VXLAN header is added
Test - 2:
Ingress Packet : Sends a VXLAN packet from port-0
Egress Packet : Received packet is a non-VXLAN packet, VXLAN header is removed

````
On the BMODEL window you will see prints that display ingress and egress packets based on editor function changes in  NPL program.



You can experience complete NPL programs for this examples located at below location

````

$NPL_EXAMPLES/editor/editor_l2_tag/npl/editor_l2_tag.npl
$NPL_EXAMPLES/editor/editor_vxlan/npl/editor_vxlan.npl


````

## Next Tutorial 

Congratulations !!
You have experienced how ```Editor``` construct work. You can now move on to next example [Function](https://github.com/nplang/NPL-Tutorials/blob/master/NPL-Titbits/Bus/Function)
