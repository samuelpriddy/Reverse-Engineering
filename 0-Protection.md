# 11/21/23 - 0 Protection

## Files/Links
[ch1.zip](http://challenge01.root-me.org/cracking/ch1/ch1.zip)  

## Tools

## Overview
ch1.bin is a simple terminal password program   
![image](https://github.com/samuelpriddy/Reverse-Engineering.github.io/assets/111523310/087f8ec0-6c84-4bb0-8962-b32887b28b5a)

## RE Process  
1. Search for the strings loaded into memory right before the password is asked for("strings ch1.bin | grep passe -B 4")  
   123456789 is likely the password    
![image](https://github.com/samuelpriddy/Reverse-Engineering.github.io/assets/111523310/af7fbe69-e1de-4f73-b789-1efaddf6c941)
