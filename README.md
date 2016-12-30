# pyGARD - Python Generation of Axi Register Definitions

## Description
This script will generate AXI Slave register definitions with a descriptive YAML.


## Configuration
For generate different components with register definitions you can put a single file
in the generation folder and will be parsed automatically.

### Component
The component definition has following commands
Name: xxx					(based on this name all needed AXI file be generated from it)
Version: 01.01.4711			(we need this time format)
Width: 32					(defines the AXI register width)
Build: ""					(please note the quotes it's necessary at the moment, sorry for that)
RegisterDefinition			(here we do more magic, see next chapter)

### RegisterDefinition
Register_1 .... Register_N	(we need this for the description of slv register definitions, see next heading)

### Register_N
Name: RegisterNamePutHere	(this name will be used as an alias for you)
Documentation				(The flag isn't used at this time, but I plan to implement it as comment before alias definition)
Option						(see next heading)
Bits						(see after next heading)

### Option
read						(set True or False, if the register can be read)
write						(set True or False, if the register can be written)
clear_on_read				(set True or False, if the register will be cleared after reading)

### Bits
PutNameHere: N				(here you can specify a bit name as it will be used for alias name and the bit or vector you will assign)
PutNameHere: N-0

### Example
```vhdl
Component:
    Name: Test_XXX
    Version: 9.12.2016
    Width: 32
    Build : "00"
    RegisterDefinition:
        Register_1:
            Name: Interrupt
            Documentation: Text hier
            Option:
                read: True
                write: False
                clear_on_read: True
            Bits:
                IRQ1: 0
                IRQ2: 1
                IRQS: 6-2
                ENABLE: 7
                Undefined: 31-8
        Register_2:
            Name: Counter
            Documentation: Text hier
            Option:
                read: False
                write: True
                clear_on_read: False
            Bits:
                CNT1: 5-0
                CNT2: 12-6
                CNT3: 31-20
```

## To-Do
- implement Documentation
- make keynames case insensitive
- add more features (?)