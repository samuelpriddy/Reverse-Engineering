# 11/20/23 - Cruehead

## Files
[cruehead1.zip](https://github.com/samuelpriddy/Reverse-Engineering.github.io/files/13419266/cruehead1.zip)  

## Tools
[IDA Free](https://hex-rays.com/ida-free/)

## Overview
Crackme1.exe opens to a blank application  
![image](https://github.com/samuelpriddy/Reverse-Engineering.github.io/assets/111523310/61a121dc-3140-46ba-965c-39fb6a519ab6)  
Clicking Help, followed by Register, opens a new box. The registration fails unless a valid Serial value is entered.   
![image](https://github.com/samuelpriddy/Reverse-Engineering.github.io/assets/111523310/564497f9-6ad3-401c-ae95-4412d0cbce92)

## RE Process
1. Disassembled Crackme1.exe in IDA  
![image](https://github.com/samuelpriddy/Reverse-Engineering.github.io/assets/111523310/01fa2e5a-24e1-4f45-9f36-c65f7cce5299)

2. Open Strings viewer(shift + F12) and identify 'Great Work, mate!' as the target response
![image](https://github.com/samuelpriddy/Reverse-Engineering.github.io/assets/111523310/a7dfe2a3-6b3e-4a65-ba7b-96b4d8469488)

3. Follow the target response calls and identify sub_40134D as the target function, renamed to display_good_message  
   Crackme1.exe jumps to the display_good_message if eax == ebx, defined in lines 00401241 and 00401243
![image](https://github.com/samuelpriddy/Reverse-Engineering.github.io/assets/111523310/bb981c69-dd1e-43ee-a0fe-5d3104a53533)

5. 
