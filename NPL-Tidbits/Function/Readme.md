# Function Construct

Functions are used in NPL, to describe generic packet processing, to process results of parser, logical tables, special_function and other constructs. Functions are imperative constructs, which can do data transformation and support application modularity. Multiple other NPL constructs can be invoked inside functions.

Function allow conditional statements, assignment statements and complex operations for data transformation of the logical buses. Functions can access and update logical bus data. Functions can be nested within other functions.

Here are a few scenarios where function could be used. Functions can be used to implement flexible decision logic. For example, decode lookup results to determine whether a packet is unicast or multicast.  Function can be used to extract packet data. Function can be used to invoke logical table lookups, special functions.

Function can also be used to specify application modularity. For such usage, function may have logical table lookups, strength resolve, special function calls, dynamic table calls etc. It is suggested to maintain separate NPL functions for modularity and packet processing.


### Function Example 

We have created an example that illustrates how to use NPL's ```function``` construct and provides sandbox for experiments. This NPL Program

 - Parse incoming packet
 - In a ``` function``` perform a hash calculation by using packet's source & destination IP, source & destination TCP/UDP port and protocol in use
 - Assign the hash value to a bus field
 - Calculated hash value is printed on BM console
 
To execute this example, follow below steps

1. Make sure [build environment](https://github.com/nplang/NPL-Tutorials#npl-build-enivronment) was properly setup as described earlier
2. Once the environmental variables were setup execute below commands. 
````

export NPL_EXAMPLES=/home/npl/ncsc-1.3.3rc4/examples/npl_tidbits/constructs
cd $NPL_EXAMPLES/function 
make fe_nplsim
make nplsim_comp
make nplsim_run

````

Now you will see two xterm windows one with name ```BMODEL``` and another with ```BMCLI```. You can now inject packet using below command from original console widow where you compiled the NPL code. 

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

You have experienced how ```Function``` construct work. You can now move on to next example [Logical Register](https://github.com/nplang/NPL-Tutorials/blob/master/NPL-Tidbits/Logical-Register)
