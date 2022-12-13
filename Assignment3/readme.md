### Assignment 3


## Instrumentation Via Hyper-call (Add New CPUID Emulation Features in KVM)</br>


Instructions
 - Start from the previous environment used for the Assignment 2 
 - Modify the cpuid.c, vmx.c and cpuid.h as per the requirement and SDM 
 - Once Modified, Use the similar steps used in assignment 2, to rebuild the kernel 
 - Once Kernel is built do a reboot and launch the inner vm and run the test cases from inside. 
 Output should be like below
## Outer VM
![image](https://github.com/avinashpakala/cmpe-283/blob/main/Assignment3/output.png)

## Inner VM 
![image](https://github.com/avinashpakala/cmpe-283/blob/main/Assignment3/image2.png)
<br>
![image](https://github.com/avinashpakala/cmpe-283/blob/main/Assignment3/image3.png)



 
A3 Questions:

# Does the number of exits increase at a stable rate?
  * No, certain exits grow, while others stay the same. The ones that rise have varying increment ratios depending on the kind of exit.

# Are there more exits performed during certain VM operations?
  * Yes the exits are more for certain VM operations like  EXIT_REASON_MSR_READ(31), EXIT_REASON_IO_INSTRUCTION(30),  EXIT_REASON_CPUID(10) etc.

# Approximately how many exits does a full VM boot entail?
    * It contains approximately 833121 exits with total 12385262220 cycle times.
    
# Of the exit types defined in the SDM, which are the most frequent? Least?
  * The most common exit reason is EXIT REASON EPT VIOLATION(48), while the least common exit reason is EXIT REASON DR ACCESS(29).
  * Additionally, the biggest increment over time is for EXIT REASON MSR READ(31), whereas the lowest increment is for EXIT REASON EPT VIOLATION(48).

# Team Contribution.

</br>
Avinash :</br>
Created the kernel </br>
In the VM,  installed the necessary kernel modules. </br>
Comprehended and researched the assignment's code. </br>
The code has been updated to reflect the changes that were discussed. </br>
Test files were created and compiled.</br>

</br>
Vikas :</br>
Created the kernel </br>
Reviewed the canvas lecture and understood the steps to be taken </br>
Did some research on CPUID instructions and CPU leaf nodes. </br>
Recognized where and what changes to make in order to complete the assignment </br>
README.md has been updated and documentation has been created.</br>

</br>
</br>


