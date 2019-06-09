# Logical Bus Construct

Logical bus construct is used to define collection of fields (variables).

## Bus Definition

Use a struct to define the fields and overlays that make up a logical bus.
Field ordering is maintained in the logical bus as defined in the struct.

## Bus Instantiation (bus)

The ````bus```` construct is used to declare a logical bus by instantiating a bus definition struct. Note that a bus may have overlay fields that can be individually referenced in the NPL program.

### Bus Example 

We have created an example that defines a bus, assigns values to the fields in bus in one function, and displays them in another function.

To execute this example, follow below steps

1. Make sure [build environment](https://github.com/nplang/NPL-Tutorials#npl-build-enivronment) was properly setup as described earlier
2. Once the environmental variables were setup execute below commands. 
````

export NPL_EXAMPLES=/home/npl/ncsc-1.3.3rc4/examples/npl_tidbits/constructs
cd $NPL_EXAMPLES/bus 
make fe_nplsim
make nplsim_comp
make nplsim_run

````

Now you will see two xterm windows one with name ```BMODEL``` and another with ```BMCLI```. You can now inject packet using below command  from original console widow where you compiled the NPL code. 

````
python bm_tests/corp_net/testPkt.py

````

On the BMODEL window you can see display of bus fields.

You can experience complete NPL program for this example which was located at below location

````

$NPL_EXAMPLES/bus/npl/bus.npl

````

## Next Tutorial 

Congratulations :+1:

You have experienced how ``` Logical bus ``` construct work. You can now move on to next example [Data Type and Parser](https://github.com/nplang/NPL-Tutorials/tree/master/NPL-Tidbits/Data-Types-Parser)
