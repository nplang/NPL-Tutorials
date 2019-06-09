# Logical Table Construct

The logical table constructs are used to define a match action table with keys, fields, key_construct, fields_assign, table type minsize and maxsize. Logical tables also have a built-in lookup() method. It allows NPL Programmer to define a data structure which control-plane or data-plane can modify. NPL Programmer can specify key and policy fields to be stored in the logical_table. NPL Programmer can also specify key construction mechanisms using logical bus fields. Finally logical_table allows NPL Programmer to specify fields_assign method to handle fields. 

## Logical Table Example 

We have created an NPL application to demonstrate & provide sandbox to experiment with ```logical_table``` construct.

Logical-Table type used in this example is Index type named as VLAN_TABLE. This table is indexed using vlan_id of packet & determines the ports that incoming packet can be forwarded.

To execute this example, follow below steps

1. Make sure [build environment](https://github.com/nplang/NPL-Tutorials#npl-build-enivronment) was properly setup as described earlier
2. Once the environmental variables were setup execute below commands. 
````

export NPL_EXAMPLES=/home/npl/ncsc-1.3.3rc4/examples/npl_tidbits/constructs
cd $NPL_EXAMPLES/logical_table
make fe_nplsim
make nplsim_comp
make nplsim_run

````

Now you will see two xterm windows one with name ```BMODEL``` and another with ```BMCLI```. 

Before injecting packets into ``` BMODEL``` VLAN_TABLE has to be populated with entries for match action. ```BMCLI``` window should be used to populate VLAN_TABLE using below ```LT``` Commands

````

Entry#1 vlan_table[entry-2].vlan_membership_bitmap = {ports-0,2}
Commnand to be used : (bmcli.0> lt vlan_table insert _INDEX=2 vlan_membership_bitmap=0x5)

Entry #2 vlan_table[entry-3].vlan_membership_bitmap = {ports-0,3}
Commnand to be used :(bmcli.0> lt vlan_table insert _INDEX=3 vlan_membership_bitmap=0x9)

````
You can either use above individual commands directly to get an experience of LT commands OR we have added these CLI commands in a text file which you can invoke using below command from BMCLI window
````
rcload /home/npl/ncsc-1.3.3rc4/examples/npl_tidbits/constructs/logical_table/bm_tests/corp_net/configuration.txt

````

You can now inject packet using below command  from original console widow where you compiled the NPL code. 

````
python bm_tests/corp_net/testPkt.py

````

The above testPkt.py sends the following packets to port-0 of the Behavioral Model

````

Send vlan-2 packet from port-0 and check packet received back on port-2.
Send vlan-3 packet from port-0 and check packet received back on port-3.

````

On the BMODEL window you will see prints that display ingress and egress packets.

You can experience complete NPL programs for this examples located at below location

````

$NPL_EXAMPLES/editor/logical_table/npl/logical_tbl.npl

````

## Next Tutorial 

Congratulations :+1:

You have experienced how ```Logical Table``` construct work. You can now move on to next example [Special Function](https://github.com/nplang/NPL-Tutorials/tree/master/NPL-Tidbits/Special_Function)
