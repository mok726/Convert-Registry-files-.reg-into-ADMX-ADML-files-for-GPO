﻿This script will read a v4 or v5 registry file and generate a Vista/W7 Policy file (ADMX) and it's corresponding interface file (ADML). 
 
 What it does
Reads a registry file (.reg) and creates the corresponding ADMX and ADML files that would allow to set the registry values detail led in the original .reg file.
in order to create the GUI definition required by the GPMC, it makes a few assumptions:
a) the "name" of the value is also used as the caption for all displays.
b) all dwords values are assigned a numeric textbox for data entry
c) all other value types are treated as strings and assigned a textbox for data entry.

Caveats
@ or (Default)
The tools will not handle correctly the "@" or unnamed valuename. This is the one that in the registry editor shows as (Default).
The reason for this is that I have not been able to find the correct way to define this in ADMX/L.

WORKAROUND: For now it's assigning the value to a "(Default)" value, but as you can see in the examples bellow, windows does not recognize this "(Default)" value as the real "(Default)" value.
I will need to find an existing ADMX that sets this kind of values and read it's XML in order to learn how it's done. OR maybe someone can let me know so I can correct the tool.

Hex, Hex(0) ...
This is another example of things that I was not able to learn from the ADMX files that I have available.
We have several cases of registry files that assing a value composed of several 2 char Hexadecimal values, but I have not find any ADMX file that applies this kind of settings to to policies.

WORKAROUND: For now, and until I can find the way to do it correctly, the script will make this hexadecimal values into a text.
I will need to find an existing ADMX that sets this kind of values and read it's XML in oder to learn how it's done. OR maybe someone can let me know so I can correct the tool.

HKU or HKEY_USERS
The ADMX definition allows you to set policies for Users (Current User, actually) and/or Computers, this does not include the HKU or the HKEY_USERS.

WORKAROUND: The script will treat any HKU policy as a HKCU (it will clean any named user defined as part of the HKU).


Usage:

CSCRIPT REG_2_ADMXL.vbs registry-file language [name]

registry-file is the name and path of the registry file to be converted.
language is the language and culture to be used, ie: en-US, sp-AR, etc.
name Display Name to show in the GPO. if omited "REG_2_ADMXL Generated Policy" will be used.


The output file will be named after the .REG file (if the input is myfile.REG, the output will be myfile.ADMX and myfile.ADML.
The ADMX output file will be saved in the same folder the input .REG file is located, while the ADML output file will be saved in a subfolder of the one the .REG file is located. The subfolder will be named after the language specified.
So, if the reg file is C:\myapp\myfile.reg and the lang is en-US, then the ADMX file will be as in C:\myAPP\myfile.ADMX and the ADML file will be saved as C:\myAPP\en-US\myfile.ADMX

 

 It's really quick and really simple to understand (I think).

 

If you want to read more details  visit http://mscosentino-en.blogspot.com/2010/02/convert-registry-file-to-admx-policy.html

 
