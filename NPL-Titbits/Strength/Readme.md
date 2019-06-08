# Strength Resolution Construct

In the NPL paradigm, multiple tables may be looked up in parallel. When multiple tables assign the same object, a mechanism is needed to resolve which value to use. NPL uses a strength-based mechanism for resolution when a numerical comparison is sufficient to decide the winning object.

NPL provides constructs to associate strength values with table lookup results. Each lookup generates one strength profile. Strengths can be static (per table based) or dynamic (per entry based).


## Strength Resolution Construct Example 

We have created couple of examples to illustrate how to use NPL's 'Strength' constructs and provides sandbox for experiments.

### Example 1 (Strength Resolution for COS)
This example illustrates strength-based mechanism to decide a winning cos-value-assignment when multiple tables can assign cos-value. In the program there are three sources for cos assignment:
 - Pri_cos_mapping assigns cos values based on 802.1p value(vlan_priority)
 - Dscp_cos_mapping assigns cos values based on dscp value in IP header
  - Local_bus default cos assignment (no mapping from packet contents)

```strength_resolution``` construct resolves the winning object based on 'cos_strength_profile_table' and 'strength_index' provided by each of cos assignment sources.

To execute this example, follow below steps

1. Make sure [build environment](https://github.com/nplang/NPL-Tutorials#npl-build-enivronment) was properly setup as described earlier
2. Once the environmental variables were setup execute below commands. 
````

export NPL_EXAMPLES=/home/npl/ncsc-1.3.3rc3/examples/npl_tidbits/constructs
cd $NPL_EXAMPLES/strength/strength_cos 
make fe_nplsim
make nplsim_comp
make nplsim_run

````

Now you will see two xterm windows one with name ```BMODEL``` and another with ```BMCLI```. 

Before injecting packets into BMODEL ```pri_cos_mapping_table```, ```dscp_cos_mapping_table``` and ```cos_strength_profile_table``` has to be populated with entries for match action. BMCLI window should be used to populate these tables using below LT Commands.

````

rcload /home/npl/ncsc-1.3.3rc3/examples/npl_tidbits/constructs/strength/strength_cos/bm_tests/corp_net/tbl_cfg_cos.txt

````

You can now inject packet using below command  from original console widow where you compiled the NPL code. 

````
python bm_tests/corp_net/testPkt.py

````

The above testPkt.py sends the following packets to port-0 of the Behavioral Model
````

Test - 1:
Ingress Packet : Send a packet with pri = 0, dscp = 0 from port-0 to BM
Observations to made : 
Strength of pri_cos_mapping_table and dscp_cos_mapping_table are 0, while strength of local_bus.cos is 1
The winning object is local_bus.cos.
Print out the cos value along with egress packet in BM window

Test - 2:
Ingress Packet : Send a packet with pri = 3, dscp = 8 from port-0 to BM
Observations to made : 
Strength of pri_cos_mapping_table is 3, strength of dscp_cos_mapping_table is 1,  strength of local_bus.cos is 1. 
The winning object is pri_cos_mapping_table and final cos value is 3.
Print out the cos value along with egress packet in BM window

Test - 3:
Ingress Packet : Send a packet with pri = 3, dscp = 40 from port-0 to BM
Observations to made : 
Strength of pri_cos_mapping_table is 3, strength of dscp_cos_mapping_table is 5,  strength of local_bus.cos is 1. 
The winning object is dscp_cos_mapping_table and the final cos value is 5.
Print out the cos value along with egress packet in BM window

````
On the BMODEL window you will see prints that display ingress and egress packets based on strength resolution construct results.


### Example 2  (Strength Resolution for Vlan ID)

This example illustrates strength-based mechanism to decide a winning vlan-assignment when multiple tables can assign vlan for flow. In the program there are two sources for vlan assignment:
    - port_table: assigns vlan value based on port on which packet has ingressed.
    - vlan_protocol_table : assigns vlan value based on packet protocol.
```strength_resolution``` construct resolves the winning object based on 'vlan_strength_profile_table' and 'strength_index' provided by each source.

To execute this example, follow below steps

1. Make sure [build environment](https://github.com/nplang/NPL-Tutorials#npl-build-enivronment) was properly setup as described earlier
2. Once the environmental variables were setup execute below commands. 
````

export NPL_EXAMPLES=/home/npl/ncsc-1.3.3rc3/examples/npl_tidbits/constructs
cd $NPL_EXAMPLES/strength/strength_vid
make fe_nplsim
make nplsim_comp
make nplsim_run

````

Now you will see two xterm windows one with name ```BMODEL``` and another with ```BMCLI```. 

Before injecting packets into BMODEL ```port_table```, ```vlan_protocol_table``` and ```vlan_strength_profile_table``` has to be populated with entries for match action. BMCLI window should be used to populate these tables using below LT Commands.

````

rcload /home/npl/ncsc-1.3.3rc3/examples/npl_tidbits/constructs/strength/strength_vid/bm_tests/corp_net/tbl_cfg_vlan.txt

````

You can now inject packet using below command  from original console widow where you compiled the NPL code. 

````
python bm_tests/corp_net/testPkt.py

````

The above testPkt.py sends the following packets to port-0 of the Behavioral Model
````

Test - 1:
Ingress Packet : Send a tagged packet from port-0 to BM.
Observations to made : 
No vlan assignment is done for outer tagged packet
BM prints out the outer vid along with received packet from BM on port-1

Test - 2:
Ingress Packet : Send an untagged EtherII packet from port-0 to BM.
Observations to made : 
EtherII packets will not lookup vlan_protocol_table, vlan assignment is taken from port table
BM prints out the vid value 0xf alomg with received packet from BM on port-1

Test - 3:
Ingress Packet : Send an untagged LLC packet from port-0 to BM
Observations to made : 
LLC packets will lookup vlan_protocol_table and port_table, since  vlan_protocol_table gets higher strength, vid is assigned as 0x2
BM prints out the vid assignment value along with received packet from BM on port-1

Test - 4:
Ingress Packet : Send an untagged SNAP packet from port-0 to BM
Observations to made : 
SNAP packets will lookup vlan_protocol_table and port_table, since vlan_protocol_table gets higher strength, vid is assigned as 0x1
BM prints out the vid assignment value along with received packet from BM on port-1


````
On the BMODEL window you will see prints that display ingress and egress packets based on strength resolution construct results.



You can experience complete NPL programs for this examples located at below location

````

$NPL_EXAMPLES/strength/strength_cos/npl/strength_cos.npl
$NPL_EXAMPLES/strength/strength_vid/npl/strength_vid.npl


````

## Next Tutorial 

Congratulations !!
You have experienced how ```Editor``` construct work. You can now move on to next example [Function](https://github.com/nplang/NPL-Tutorials/blob/master/NPL-Titbits/Function)
