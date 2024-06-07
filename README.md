# WSL2 Internals

![WSL2](/images/wsl2.png)


1. `wsl.exe` talks to [Lxss Manager Service](#lxss-manager-service). So `wsl.exe` is the client, like in comparison to Docker the `docker` client. 
2. [Lxss Manager Service](#lxss-manager-service), is in comparison to Docker agin like `dockerd`. And it manages the WSL2 [Distributions](#distributions), which is really just containers running on a [Managed Linux VM](#managed-linux-vm). It uses the [Host Compute System](#host-compute-system-hcs) service to manage the life cycle of the [Managed Linux VM](#managed-linux-vm). And it sets up all resources which is later used by the VM, like [WSL2 Networking](), Hyper-V sockets and the VHD-format [Hyper-V Filesystem](). 
3. [Host Compute System](#host-compute-system-hcs) is the host virtualization technology, and it's only used to handle the life cycle of the [Managed Linux VM](#managed-linux-vm) which is empheral, meaing that a new instance is always set up when started. So it's stateless and fully managed by [Managed Linux VM](#managed-linux-vm).
4. When the [Lxss Manager Service](#lxss-manager-service) has a [Managed Linux VM](#managed-linux-vm) to work with, it manages the [Distributions](#distributions) on the [Managed Linux VM](#managed-linux-vm). And sets up the `PID 1` `init executable`, provides it with a filesystem and uses `namespaces` to create the container. The `init executable` starts up the [9P Protocol Service](#9p-protocol-service), which is a remote filesystem protocol which `Windows Explorer` uses in order to access the [Distributions](#distributions) filesystem from Windows.


# 9P Protocol Service

# Distributions

# Host Compute System (HCS)
hcsdiag

# Managed Linux VM
CBL Mariner
wsl --debug-shell
wsl --system

# Lxss Manager Service
C:\Windows\System32\lxss

# Windows Sandbox


wsl.exe -> Lxss Manager Service (what distributions are installed, running etc) -> Host Compute Service (Virtualization Technology, host network, host VM)


# Integrations

## Plan 9 Linux -> Windows
A worker VM acts as a 9P protocol server (Plan 9) for Windows files. Runs on Windows host. And make Windows files and binaries accessible from Linux.

## Plan 9 Windows -> Linux
Inside a WSL2 distribution, a 9P protocol server is running. Which makes Linux files (and binaries?) accessible from Explorer in Windows.


# Init


# wslpath

# /etc/wsl.conf

# $WSLENV
Share environment variables between Linux and Windows


# Background Taks support