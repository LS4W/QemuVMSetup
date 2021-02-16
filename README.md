# QemuVMSetup
Uses the output iso from WindowsIsoBuilder to create a vm. An example of how you would use this is as follows:

```sh
# Generate autounattend with https://github.com/LS4W/WindowsAutoUnattendBuilder
WindowsBuilder > autounattend.xml

# Patch a windows 10 ISO with the generated autounattend using https://github.com/LS4W/WindowsIsoBuilder
# Again, note this ISO has to contain an install.wim
ls4w-build-iso Win10_20H2_V2_English_x64.iso autounattend.xml win10_autoinstall.iso

# Create a virtual HDD
ls4w-create-hdd windows10.qcow2 20G

# Create a VM with this HDD
# You can use the graphics flag to help debug. This will create a window to show the VM
ls4w-create-vm -i win10_autoinstall.iso -h windows10.qcow2 --graphics yes

# Start the VM
# Again, use graphics to see any errors.
ls4w-start-vm -h windows10.qcow2 --graphics yes
```
