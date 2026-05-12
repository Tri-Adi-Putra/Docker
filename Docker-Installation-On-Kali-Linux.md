## Since Kali Linux is based on Debian, the installation process follows the Debian steps. Here is the guide:
## 1. System Preparation
Update your system and remove any old versions of Docker to avoid conflicts.
```
sudo apt update && sudo apt full-upgrade -y
sudo apt remove docker docker-engine docker.io containerd runc
```
## 2. Set Up Docker Repository
Install the necessary packages and add Docker’s official GPG key:
```
sudo apt install ca-certificates curl gnupg
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://docker.com | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg
# Add the repository (using 'trixie' or 'bookworm' depending on your Kali version)
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://docker.com trixie stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt update
```
## 3. Download & Install Docker Desktop

   1. Go to the [official Docker website](https://docs.docker.com/desktop/setup/install/linux/debian/) and download the latest DEB package.
   2. Install the package using the terminal (replace <version> with the actual filename):
   ```
   sudo apt install ./docker-desktop-<version>-amd64.deb
   ```
   
## 4. KVM Configuration (Crucial)
Docker Desktop on Linux runs within a Virtual Machine, so it requires KVM support.
```
sudo modprobe kvm
sudo modprobe kvm_intel  # For Intel processors
sudo modprobe kvm_amd    # For AMD processors
sudo usermod -aG kvm $USER
```
Note: You must logout and log back in for the group changes to take effect.
## 5. Launch Docker Desktop
Search for "Docker Desktop" in your Kali Linux application menu and launch it. Accept the service agreement to get started.
Quick Tips:

* If you only need the CLI version (no GUI), just run sudo apt install docker.io.
* To verify the installation, run docker version in your terminal.

Do you need help checking if hardware virtualization is enabled in your BIOS/UEFI settings?

