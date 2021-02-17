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
ls4w-create-vm -i win10_autoinstall.iso -h windows10.qcow2 --enable-graphics yes

# Start the VM
# Again, use graphics to see any errors.
ls4w-start-vm -h windows10.qcow2 --graphics yes
```

Command line options:
```sh
# Bootable iso. This should be the ISO created with the LS4W/WindowsIsoBuilder tool
-i|--iso)

# The amount of memory allocated to the VM. Default is 1G
-m|--memory)

# Enable or disable graphics. yes or no. Default is no
-g|--enable-graphics)

# Path to qcow2 image. 
-h|--hdd-image)

# Number of CPU cores to allocate
-i|--cores)

# The VM name
-n|--name)

# Path to OVMF_CODE.fd, default path is /usr/share/OVMF/OVMF_CODE_4M.fd
-o|--ovmf_code)

# Path to OVMF_VARS.fd, default path is /usr/share/OVMF/OVMF_VARS_4M.fd
-p|--ovmf_vars)
```

## Dependencies
This script will try to use the command qemu-system-x86_64. It also requires OVMF since it uses UEFI. It uses QXL for graphics.

### Debian

```sh
# List potentially incomplete, will need updated
ovmf qemu qemu-system-x86 spice-gtk
```
