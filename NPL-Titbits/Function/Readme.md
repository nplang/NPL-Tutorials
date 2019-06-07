# Funciton Construct

Function Construct enables NPL programmer to implement relative simple fixed decision processing logic. 
Supports actions and configuration without using match action tables. Functions can be nested within other functions
Inputs of a Funciton can be Global Bus, Packet Data Headers, Logical Registers. And the outout will be Bus field assignments.
A function can be associated with multiple buses and logic or arithmetic operations to  provide complex functionality


### Function Example 

We have created an example that illustrates how to use NPL's 'function' construct and provides sandbox for experiments. This NPL Program

 - Parse incoming packet
 - In a ``` function``` performa hash calculation by using packet's source & destination IP, source & destination TCP/UDP port and protocol in use
 - Assign the hash value to a bus field
 - Calculated hash value is printed on BM console
 
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
Sends a TCP packet with src_port = dst_port = 0.
Sends a UDP packet with src_port = 0x1234 and dst_port=0x5678 
Double check the output log from BMODEL window to see the calculated hash_value

````
On the BMODEL window you will see prints that display hash value changes done in  NPL program using ```function``` construct.

You can experience complete NPL program for this example which was located at below location

````

$NPL_EXAMPLES/editor/function/npl/fun_ip_hash_calc.npl

````

## Next Tutorial 

Congratulations !!
You have experienced how ```Function``` construct work. You can now move on to next example [Logical Register](https://github.com/nplang/NPL-Tutorials/blob/master/NPL-Titbits/Logical-Register)
