---
layout: default
permalink: /wsl
---

## [Home](/) >> WSL & Arch Linux

Set up a WSL development environment using [Arch Linux](https://www.archlinux.org/).

* TOC
{:toc}

* * *

## Install WSL

### Enable Virtualization

Ensure that virtualization is enabled in the BIOS and that the `Windows Subsystem for Linux` optional component is enabled.

    > Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux

### Install WSL

Install the `Windows Subsystem for Linux` from the Microsoft Store, which is [now the default](https://devblogs.microsoft.com/commandline/the-windows-subsystem-for-linux-in-the-microsoft-store-is-now-generally-available-on-windows-10-and-11/).

> **Note**: You no longer should enable the "Windows Subsystem for Linux" optional component, or install the WSL kernel or WSLg MSI packages as they are no longer needed.
>
> Using the [Store version](https://aka.ms/wslstorepage) of WSL allows you to [get updates to WSL much faster](https://devblogs.microsoft.com/commandline/a-preview-of-wsl-in-the-microsoft-store-is-now-available/) compared to when it was a Windows component. [WSLg](https://aka.ms/wslg) is also now bundled.

### Update WSL

To update to the latest stable version of WSL and WSLg, simply run `wsl --update` from an elevated command prompt or powershell.

    > wsl --update

To update to the latest pre-release version, run instead:

    > wsl --update --pre-release

## Install a distribution

WSL can be installed with Ubuntu as a default distribution (`wsl.exe --install`) or with a pre-defined distribution (`wsl.exe -l -o`) with the `-d` parameter.

It can also be used with any [custom Linux distribution](https://learn.microsoft.com/en-us/windows/wsl/build-custom-distro).

### Install Arch Linux

Arch Linux provides an official WSL image as part of the [archlinux-wsl](https://gitlab.archlinux.org/archlinux/archlinux-wsl) project.

#### Automated installation

From a Windows system with WSL 2 installed, run:

    > wsl --install archlinux

You can then run Arch Linux in WSL via the `archlinux` application from the Start menu, or by running `wsl -d archlinux` in a Windows shell.

#### Manual installation

Download the latest Arch Linux `.wsl` image and double-click on it to start the installation, or run:

    > wsl --install --from-file C:\Users\Username\Downloads\archlinux.wsl

You can check that the distribution has been installed and registered as default with WSL:

    > wsl.exe -l
    Windows Subsystem for Linux Distributions:
    archlinux (Default)

You can launch WSL from the added Windows Terminal entry.

## Configuration

After the installation, you have access to a root shell.

    [root@HOSTNAME]#

### Setting the root password

Set the root password:

    # passwd
    New password:
    Retype new password:
    passwd: password updated successfully

### Add the default user

Please see [Sudo](https://wiki.archlinux.org/title/Sudo#Example_entries) and [User and groups](https://wiki.archlinux.org/title/Users_and_groups) pages.

Add user:

    # useradd -m -G wheel -s /bin/bash <username>

Set default user password:

    # passwd <username>
    New password:
    Retype new password:
    passwd: password updated successfully

Adjust default user sudo permissions in `/etc/sudoers` using `visudo`.

    # export EDITOR=vim
    # visudo /etc/sudoers

```
## Uncomment to allow members of group wheel to execute any command
%wheel ALL=(ALL) ALL
```

To set a different default user than `root`, append the following to `/etc/wsl.conf`:

```
[user]
default=username
```

> **Note**: Make sure to give your `root` user a password before you close your session. If you find yourself 'locked out', invoke `> wsl -u root` from a CMD window on the Windows host.

The change will apply at the next session. To terminate your current session:

    > wsl --terminate archlinux

You can also set the default user with:

    > wsl --manage archlinux --set-default-user <username>

### Configure WSL settings

Set [advanced settings configuration](https://learn.microsoft.com/en-us/windows/wsl/wsl-config).

#### Global settings

Adjust global configuration file in `C:\Users\<Username>\.wslconfig`:

```
# Settings apply across all Linux distros running on WSL 2
[wsl2]
memory=24GB
processors=20

[experimental]
autoMemoryReclaim=gradual
sparseVhd=true
```

#### Local settings

Adjust local configuration file in `/etc/wsl.conf`:

```
#
# /etc/wsl.conf
#
# See https://docs.microsoft.com/en-us/windows/wsl/wsl-config

# systemd support
[boot]
systemd=true

# automount settings and options
[automount]
enabled = true
mountFsTab = true
root = /mnt/
options = "metadata,umask=22,fmask=11"

# network settings
[network]
generateHosts = true
generateResolvConf = true

# interop settings
[interop]
enabled = true
appendWindowsPath = true
```

### Configure the package manager

Initialize and configure the [pacman](https://wiki.archlinux.org/title/Pacman) package manager.

#### Package manager options

Enable the `VerbosePkgLists` option to have a nicer display.

    $ sudo vim /etc/pacman.conf

#### Select a mirror

Select a packages [mirror](https://wiki.archlinux.org/title/Mirrors) close to your location.

    $ sudo vim /etc/pacman.d/mirrorlist

#### Initialize keyring

Initialize the keyring of the `pacman` package manager:

    $ sudo pacman-key --init
    $ sudo pacman-key --populate

#### Packages update

    $ sudo pacman -Sy archlinux-keyring
    $ sudo pacman -Su

## Post-installation

### Install Zsh

Bash is the default command-line shell, but [Zsh](https://wiki.archlinux.org/title/Zsh) is a good
alternative due to its improved interactive experience, richer scripting capabilities, extensibility.

    $ sudo pacman -S zsh

Make it the [default shell](https://wiki.archlinux.org/title/Command-line_shell#Changing_your_default_shell):

    $ chsh -s /bin/zsh

### Install Neovim

    $ sudo pacman -S neovim

Set neovim as default editor

In `~/.zshrc`, set the default editor:

```
# editor
export EDITOR=nvim
export VISUAL=nvim
export SUDO_EDITOR=nvim
export SYSTEMD_EDITOR=nvim
export GIT_EDITOR=nvim
```

In `/etc/sudoers`, set the default editor for `sudo`:

```
Defaults editor=/usr/bin/nvim
```

### Install an AUR helper

Install an [AUR helper](https://wiki.archlinux.org/title/AUR_helpers) to easily access the [Arch User Repository](https://wiki.archlinux.org/title/Arch_User_Repository).
We will use [auracle](https://aur.archlinux.org/packages/auracle-git) to semi-automate the process.

#### Build and install auracle

Ensure `base-devel` is installed:

    $ sudo pacman -S base-devel

Install `git`:

    $ sudo pacman -S git

Clone the `auracle-git` package:

    $ cd ~
    $ mkdir aur && cd aur
    $ git clone https://aur.archlinux.org/auracle-git.git

Build and install the package:

    $ cd auracle-git
    $ makepkg -si

The helper is now available to search and download packages.

#### Check for AUR update

To check for outdated packages, run:

    $ auracle outdated
    fakeroot-tcp 1.25.3-2 -> 1.31-1

As an example, a newer version of the `fakeroot-tcp` package is available.

#### Update AUR packages

To update packages:

    $ auracle update
    $ cd fakeroot-tcp/
    $ makepkg -si

### Enable system clipboard

Enable system clipboard with WSLg and Wayland:

    $ sudo pacman -S wl-clipboard

Enable WSLg communication socket for the user:

    $ sudo umount --quiet /tmp/.X11-unix
    $ sudo rm -rf /tmp/.X11-unix
    $ sudo ln -s /mnt/wslg/.X11-unix /tmp/.X11-unix
    $ sudo ln -s /mnt/wslg/runtime-dir/wayland-0* /run/user/1000/

### Open URLs in the Windows host browser

Install `xdg-utils` to enable opening links in your Windows host browser:

    $ sudo pacman -S xdg-utils

In `~/.zshrc`, set the browser environment variable:

```
export BROWSER="pwsh.exe /C start"
```

### GPU acceleration

To enable GPU video accelerated rendering in WSL, install the following packages:

    $ sudo pacman -S mesa vulkan-dzn vulkan-icd-loader

In `~/.zshrc`, set the driver environment variables:

```
export GALLIUM_DRIVER=d3d12
export LIBVA_DRIVER_NAME=d3d12
```

## Troubleshooting

Known issues and resolution.

### Set systemd time synchronization

To avoid time desynchronization after waking up from sleep, enable the time synchronization daemon.

Ensure systemd is enabled at boot in `/etc/wsl.conf`:

```
[boot]
systemd=true
```

Adjust systemd config to enable time synchronization:

    $ sudo systemctl edit systemd-timesyncd

Override the setting by adding these 2 lines:

```
### Editing /etc/systemd/system/systemd-timesyncd.service.d/override.conf

[Unit]
ConditionVirtualization=

### Line below this comment will be discarded
```

Enable and start the service:

    $ sudo systemctl enable systemd-timesyncd
    $ sudo systemctl start systemd-timesyncd

Check the status with:

    $ timedatectl status
    $ timedatectl timesync-status

### Fix libcuda symbolic link

Running `sudo pacman -Syu` results in a warning:

    /sbin/ldconfig.real: /usr/lib/wsl/lib/libcuda.so.1 is not a symbolic link

Replace the duplicated files with symlinks:

    $ cd /usr/lib/wsl/lib
    $ sudo rm libcuda.so libcuda.so.1
    $ sudo ln -s libcuda.so.1.1 libcuda.so.1
    $ sudo ln -s libcuda.so.1 libcuda.so
    $ sudo ldconfig

### Release allocation of disk space

WSL does not release disk space back to the host OS automatically.

Ensure `sparseVhd=true` is set in your global `.wslconfig` (see [Global settings](#global-settings) above). This automatically shrinks the WSL virtual hard disk (VHD) as you use it.

You can also manually compact the VHD from an elevated PowerShell prompt:

    > wsl --shutdown
    > Optimize-VHD -Path "C:\Users\<Username>\AppData\Local\Packages\...\LocalState\ext4.vhdx" -Mode Full

### User session errors or early crashes

If you encounter user session errors at startup or unexpected crashes, enable session lingering for your user:

    # loginctl enable-linger <username>

This helps ensure the systemd user session starts correctly and populates `/run/user/$UID`.

### Recover from catastrophic failure

Running `wsl` results in an error:

    > wsl.exe
    Catastrophic failure
    Error code: Wsl/Service/CreateInstance/E_UNEXPECTED

Mount the `.vhdx` image file on another distro:

    > wsl -d <working distro> --mount --vhd <path to image>\<image name>.vhdx --bare

Inside the working system, use `lsblk` to find the device and mount the device:

    $ sudo mount /dev/sdc /mnt

Repair the distro or retrieve files, then unmount the device:

    $ umount /mnt

On Windows, umount the image:

    > wsl --unmount <path to image>\<image name>.vhdx

## Resources

### WSL

* [Windows Subsystem for Linux Documentation](https://learn.microsoft.com/en-us/windows/wsl/)
* [Build a Custom Linux Distribution for WSL](https://learn.microsoft.com/en-us/windows/wsl/build-custom-distro)
* [Advanced settings configuration in WSL](https://learn.microsoft.com/en-us/windows/wsl/wsl-config)
* [Awesome WSL](https://github.com/sirredbeard/Awesome-WSL)

### Arch Linux

* [Arch Linux](https://www.archlinux.org/)
* [Install Arch Linux on WSL](https://wiki.archlinux.org/title/Install_Arch_Linux_on_WSL)
