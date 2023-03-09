---
layout: default
permalink: /wsl
---

## [Home](/) >> WSL & Arch Linux

Set up a WSL development environment using [Arch Linux](https://www.archlinux.org/).

## Install WSL

### Enable Virtual Machine Platform

Ensure the "Virtual Machine Platform" optional component is enabled and that virtualization is enabled in the BIOS.

### Install WSL

Install the `Windows Subsystem for Linux` from the Microsoft Store, which is [now the default](https://devblogs.microsoft.com/commandline/the-windows-subsystem-for-linux-in-the-microsoft-store-is-now-generally-available-on-windows-10-and-11/).

> **Note**: You no longer should enable the "Windows Subsystem for Linux" optional component, or install the WSL kernel or WSLg MSI packages as they are no longer needed.
> Using the Store version of WSL allows you to [get updates to WSL much faster](https://devblogs.microsoft.com/commandline/a-preview-of-wsl-in-the-microsoft-store-is-now-available/) compared to when it was a Windows component. [WSLg](https://aka.ms/wslg) is also now bundled.

### Update WSL

To update to the latest version of WSL and WSLg, simply run `wsl --update` from an elevated command prompt or powershell.

    > wsl --update

## Install a distribution

WSL can be installed with Ubuntu as a default distribution (`wsl.exe --install`) or with a pre-defined distribution (`wsl.exe -l -o`) with the `-d` parameter.

It can also be used with any [custom Linux distribution](https://learn.microsoft.com/en-us/windows/wsl/build-custom-distro).
We will install [Arch Linux](https://archlinux.org/) as a custom [WSL distribution launcher]() package.

### Install Arch Linux

Download and extract the latest Online Installer `Arch_Online.zip` archive from the [ArchWSL](https://git.io/archwsl) project, for example in `C:\Linux\`.

Run the executable:

    PS C:\Linux > Arch.exe

You can check that the distribution has been installed and registered as default with WSL:

    > wsl.exe -l
    Windows Subsystem for Linux Distributions:
    Arch (Default)

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

> ## Uncomment to allow members of group wgeel to execute any command
> %wheel ALL=(ALL) ALL

Exit and set the default user of the Arch WSL instance:

    # exit
    > Arch.exe config --default-user <username>

### Configure WSL settings

Adjust [WSL config](https://learn.microsoft.com/en-us/windows/wsl/wsl-config) in `/etc/wsl.conf`:

> #
> # /etc/wsl.conf
> #
> # See https://docs.microsoft.com/en-us/windows/wsl/wsl-config
>
> # systemd support
> [boot]
> systemd=true
>
> # automount settings and options
> [automount]
> enabled = true
> mountFsTab = true
> root = /mnt/
> options = "metadata,umask=22,fmask=11"
>
> # network settings
> [network]
> generateHosts = true
> generateResolvConf = true
>
> # interop settings
> [interop]
> enabled = true
> appendWindowsPath = true

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

### Packages update

    $ sudo pacman -Sy archlinux-keyring
    $ sudo pacman -Su

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

The helper is now available to se
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

## Resources

### WSL

* [Windows Subsystem for Linux Documentation](https://learn.microsoft.com/en-us/windows/wsl/)
* [WSL Distro Launcher Reference Implementation](https://github.com/Microsoft/WSL-DistroLauncher)
* [Advanced settings configuration in WSL](https://learn.microsoft.com/en-us/windows/wsl/wsl-config)
* [Awesome WSL](https://github.com/sirredbeard/Awesome-WSL)

### Arch Linux

* [Arch Linux](https://www.archlinux.org/)
* [Arch Linux Wiki](https://wiki.archlinux.org/)
* [ArchWSL](https://git.io/archwsl)