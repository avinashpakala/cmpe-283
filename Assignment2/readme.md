


</br>

## Instrumentation Via Hyper-call (Add New CPUID Emulation Features in KVM)</br>

This assignment is to modify the CPUID emulation code in KVM to report back additional information when special CPUID leaf nodes are requested:</br>
   For CPUID leaf node %eax=0x4FFFFFFC:<br />
   Return the total number of exits (all types) in %eax <br />
   For CPUID leaf node %eax=0x4FFFFFFD:  <br />
   Return the high 32 bits of the total time spent processing all exits in %ebx <br />
   Return the low 32 bits of the total time spent processing all exits in %ecx<br />
  	%ebx and %ecx return values are measured in processor cycles, across all VCPUs<br />

At a high level, you will need to perform the following:<br />
  	Execute your assignment 1 environment<br />
  Then modify the kernel code with the assignment 2(s) functionality:<br />
  Now, Determine where to place the measurement code (for exit counts and # cycles)<br />
  Create new CPUID leaf 0x4FFFFFFD, 0x4FFFFFFC<br />
   Report back information as described above<br />


Instructions:<br />
•	In Google Cloud Platform, create a VM as done in assignment 1
•	Fork the Kernel code from GitHub: ` git clone https://github.com/torvalds/linux.git ` into personal repository
•	Clone the Kernel code from personal repository into GCP VM<br />
•	Kernel Code Compilation<br />
o	Install required pacakages: apt-get install build-essential kernel-package fakeroot libncurses5-dev libssl-dev ccache bison flex libelf-dev<br />
o	Check current os info: uname -a <br/>
•	Change .config file: cp -v /boot/{your kernel}./.config<br />

<img width="1206" alt="Screenshot 2022-12-05 at 10 08 05 PM" src="https://user-images.githubusercontent.com/61676560/205847814-2f66fc1b-7606-49e6-b432-63aa37723e87.png">


Build the kernel through the following commands:<br />
<!-- <img width="468" alt="image" src="">
 -->
    - sudo make -j 8 modules
    - sudo make -j 8
    - While compiling the kernel, an error may occur, to prevent please enter the below commands
        scripts/config --disable SYSTEM_TRUSTED_KEYS
        scripts/config --disable SYSTEM_REVOCATION_KEYS
    - sudo make -j 8 modules_install
    - sudo make -j 8 install
<br />
 


Reboot the system to update the kernel and check by using below commands
    - `sudo reboot`
    - `uname -a` 
    
Change the following files
   - *vmx.c*: 
   - *cpuid.c*: 
   </br>
Build the edited modules by running
    - `sudo make modules && sudo make modules_install`

Load the built modules:
   - `sudo rmmod kvm_intel`
   - `sudo rmmod kvm`
   - `sudo modprobe kvm`
   - `sudo modprobe kvm_intel`
  
For testing the functionality, an nested VM was created in the GCP VM. The steps to create an nested VM are as follows: </br>
    - Download the Ubuntu cloud image using below
    ```
    wget https://cloud-images.ubuntu.com/bionic/current/bionic-server-cloudimg-amd64.img
    ```
    </br>
    - Install required dependent packages 
    ```
    sudo apt update && sudo apt install qemu-kvm -y
    ```
    </br>
    -Move to the directory where .img file is downloaded. Change the password and login into the vm,by perform these following steps: </br>
    ```
      sudo apt-get install cloud-image-utils ``` </br>
      
      
      a) cat >user-data <<EOF
         #cloud-config
         password: testing
         chpasswd: { expire: False }
         ssh_pwauth: True
         EOF
        
      b) cloud-localds user-data.img user-data
  
  </br>
    - Now, to run this ubuntu image, execute this: </br>
    
    - `sudo qemu-system-x86_64 -enable-kvm -hda bionic-server-cloudimg-amd64.img -drive "file=user-data.img,format=raw" -m 512 -curses -nographic`
    

    - **username**: `ubuntu`
    - **password**: `testing`
    

205847814-2f66fc1b-7606-49e6-b432-63aa37723e87.png (2411×88)

If everything went well, you should be in the inner vm, once you are on the inner vm, we can run the test code to check for the exits.
</br>
Please find the screenshots below of the execution
 
Outputs:</br>
Inner VM screenshots </br>
 
<img width="327" alt="ubuntu1" src="https://user-images.githubusercontent.com/61676560/205847541-9a2bcb4c-b28b-456a-a603-7e504ed850d5.png">

<img width="500" alt="ubuntu1" src="https://github.com/avinashpakala/cmpe-283/blob/main/Assignment2/output.png">

## Team Contribution
 </br>
 Avinash :</br>
Kernel Creation </br>
Installation necessary kernel modules in the VM </br>
Research the assignments code and made reflections </br>
The code has been updated to reflect the changes that were discussed. </br>
README.md has been updated and documentation has been created.</br>

</br>
Vikas Tadepu :</br>
Created the kernel </br>
Reviewed the canvas lecture and understood the steps to be taken </br>
Did some research on CPUID instructions and CPU leaf nodes. </br>
Recognized where and what changes to make in order to complete the assignment </br>
Test files were created and compiled.</br>

</br>

 







