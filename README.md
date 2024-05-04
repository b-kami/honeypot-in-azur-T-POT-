# honeypot-in-azur-T-POT

## Overview

This project aims to demonstrate the setup of a virtual machine (VM) on Microsoft Azure and the configuration of TPOT (Tree-based Pipeline Optimization Tool) for machine learning tasks. By following the instructions provided here, users can replicate the setup process and utilize TPOT for automated machine learning experimentation.

## Getting Started

To get started with setting up the VM and configuring TPOT, follow these steps:

### 1. Create a Virtual Machine on Azure

1. Sign in to the Azure portal at [portal.azure.com](https://portal.azure.com).
2. Navigate to the "Virtual machines" section and click on "Create".
3. Follow the prompts to select a VM size, operating system, networking settings, etc. Consider the requirements for running TPOT when selecting the VM specifications.
4. Ensure that you select **Debian 11** as the operating system for the VM.
5. Choose a VM size with at least **8GB of RAM** to meet the requirements for running TPOT.
6. Once the VM is provisioned, make note of the connection details (e.g., IP address, username, password) for accessing the VM.

### 2. Configure Network Security Rules

1. In the Azure portal, navigate to the "Networking" section of your VM and select the "Security group" associated with your VM's network interface.
2. Add the following network security rules:
   - **Rule 1: SSH Access**
     - Protocol: TCP
     - Port: 22
     - Source: `My IP` (This ensures that only your IP address is allowed to connect via SSH for initial configuration.)
   - **Rule 2: TPOT Management Access**
     - Protocol: TCP
     - Port: 64297
     - Source: `My IP` (This allows access to TPOT's management interface via NGINX reverse proxy.)
   - **Rule 3: Honeypot Access**
     - Protocol: TCP
     - Port: 0-64000
     - Source: `Any` (This rule allows connections from any IP address to access the honeypot for testing and statistical purposes.)

### 3. Install Git

1. SSH into your VM.
2. Install Git by running the following command:
    ```bash
    sudo apt-get install git
    ```

### 4. Install TPOT

1. Clone the TPOTCE (Community Edition) repository from GitHub to your VM:
    ```bash
    git clone https://github.com/telekom-security/tpotce
    ```
2. Navigate to the cloned repository directory:
    ```bash
    cd tpotce
    ```
3. Run the installer as non-root:
    ```bash
    ./install.sh
    ```

### 5. Configure and Use TPOT

1. Follow the TPOT documentation for usage instructions and examples: [TPOT documentation](https://epistasislab.github.io/tpot/).

## Additional Resources

- [Microsoft Azure Documentation](https://docs.microsoft.com/azure/)
- [TPOT Documentation](https://epistasislab.github.io/tpot/)
- [Azure Virtual Machines Overview](https://docs.microsoft.com/azure/virtual-machines/)
- [Azure VM Pricing](https://azure.microsoft.com/pricing/details/virtual-machines/)

**Note:** These instructions are tested on Debian 11 with a minimum of 8GB of RAM for running TPOT.

## License

[MIT License](LICENSE)
