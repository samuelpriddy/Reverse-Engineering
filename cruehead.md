# 11/20/23 - Cruehead

## Files/Links
[cruehead1.zip](https://github.com/samuelpriddy/Reverse-Engineering.github.io/files/13419266/cruehead1.zip)  
[Youtube Walkthrough](https://www.youtube.com/watch?v=Uo4fGnld4zk)

## Tools
[IDA Free](https://hex-rays.com/ida-free/)  
[Resource Hacker](https://www.angusj.com/resourcehacker/)


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

4. Find where eax and ebx are defined before the equality check
   - sub_40137E(renamed find_eax) with a String parameter
   - sub_4013D8(renamed find_ebx) with a byte parameter
     
5. Search for references(x key) to the String adn byte parameters; Both located in sub_401253
![image](https://github.com/samuelpriddy/Reverse-Engineering.github.io/assets/111523310/48fa79b5-7305-4b8b-9a32-7b7d98499450)

6. Both parameters are determined by GetDlgItemTextA calls, meaning the String and byte are the name and Serial inputted by the user  
   Following the user-inputted serial is a push from 3E9h, or 1001(h key)
![image](https://github.com/samuelpriddy/Reverse-Engineering.github.io/assets/111523310/91195d64-6881-46f4-b84a-3a74a340ccee)

7. Opening Crackme1.exe in Resource Hacker and opening the Dialog/DLG_REGIS folder confirms that the user inputted name box is 1000 and dialogue box is 1001
![image](https://github.com/samuelpriddy/Reverse-Engineering.github.io/assets/111523310/8da1df6d-a740-4803-b7f1-e10f95144dd2)

8. Going back to IDA, rename the String and byte to name and serial, respectively

9. Within the find_eax function, rename the argument to name
