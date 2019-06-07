# Logical Bus Constructs

Logical bus constructs are used to define collection of fields (variables).

## Bus Definition

Use a struct to define the fields and overlays that make up a logical bus.
Field ordering is maintained in the logical bus as defined in the struct.

## Bus Instantiation (bus)

The ````bus```` construct is used to declare a logical bus by instantiating a bus definition struct. Note that a bus may have overlay fields that can be individually referenced in the NPL program.

### Bus Example 

We have created an example that defines a bus, assigns values to the fields in bus in one function, and displays them in another function.
