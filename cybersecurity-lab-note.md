# Cybersecurity Lab Setup: Ubuntu & Cowrie Honeypot

## Project Overview

This project documents the setup of a simple cybersecurity lab in a virtualized environment for hands-on security practice and experimentation.

The lab consists of two Ubuntu virtual machines running on **Oracle VM VirtualBox**:

* **Attacker Machine:** Ubuntu, used to simulate security testing activities.
* **Honeypot Machine:** Minimal Ubuntu server running **Cowrie**, used to capture and log unauthorized SSH/Telnet activity.

Both virtual machines are connected through a virtual network, allowing controlled interaction between the systems while keeping the lab environment isolated from external networks.

This project also documents the installation process, configuration steps, troubleshooting challenges, and solutions encountered during the setup.

---

# 1. Attacker Environment: Ubuntu

## Overview

The attacker machine was configured using Ubuntu within Oracle VM VirtualBox. It is used to simulate security testing activities and interact with the Cowrie honeypot in a controlled environment.

## Virtual Environment Setup

The following steps were completed:

* Installed **Oracle VM VirtualBox** on the host system.
* Verified that VirtualBox launched successfully.
* Created a new Ubuntu virtual machine.
* Allocated appropriate RAM, CPU, and storage resources.
* Downloaded the official Ubuntu ISO image.
* Mounted the ISO file to the virtual machine.
* Completed the Ubuntu installation.
* Booted successfully into the new Ubuntu environment.

## Troubleshooting: Cursor / Mouse Issue

### Issue

During interaction with the Ubuntu virtual machine, the mouse cursor occasionally disappeared or failed to respond correctly when clicking inside the VM window.

### Troubleshooting Attempts

Several configuration changes were attempted, including:

* Adjusting VirtualBox display and graphics settings.
* Reinstalling VirtualBox integration tools.
* Restarting the virtual machine.
* Reviewing input configuration settings.

### Resolution

The issue was related to the virtual machine's input/display configuration.

The following adjustments were made:

* Updated the VirtualBox system and display configuration.
* Ensured that the required integration tools were properly installed.

### Result

The mouse and cursor functionality was restored, allowing normal interaction with the Ubuntu virtual machine.

---

# 2. Honeypot Environment: Cowrie

## Overview

The second virtual machine was configured as a **Cowrie honeypot** running on a minimal Ubuntu installation.

Cowrie is designed to emulate SSH and Telnet services and record interactions with the honeypot. In this lab, it provides a controlled environment for observing login attempts and simulated attacker behavior.

## Server Setup

The honeypot environment was configured by:

* Creating a second virtual machine in Oracle VM VirtualBox.
* Installing a minimal Ubuntu operating system.
* Running the server without a graphical desktop environment.
* Allocating lightweight resources appropriate for a server.
* Connecting the honeypot and attacker machines to the same virtual network.

---

# 3. Installing Cowrie

## Step 1: Install Dependencies

Update the Ubuntu package list:

```bash
sudo apt update
```

Install the required dependencies:

```bash
sudo apt install git python3-venv libssl-dev libffi-dev build-essential authbind -y
```

If `sudo` is not available, install it with:

```bash
apt install sudo -y
```

### Network Troubleshooting

If the VM does not have internet connectivity during installation, temporarily configure the VirtualBox network adapter to use **NAT** so that the required packages can be downloaded.

After installation, the lab can be returned to an isolated networking configuration if required.

---

## Step 2: Clone the Cowrie Repository

Clone the Cowrie repository:

```bash
git clone https://github.com/cowrie/cowrie.git
```

Move into the Cowrie directory:

```bash
cd cowrie
```

---

## Step 3: Create a Python Virtual Environment

Create a Python virtual environment:

```bash
python3 -m venv cowrie-env
```

Activate the environment:

```bash
source cowrie-env/bin/activate
```

Upgrade `pip`:

```bash
pip install --upgrade pip
```

Install the required Python packages:

```bash
pip install -r requirements.txt
```

---

# 4. Configure Cowrie

Create the Cowrie configuration file from the provided template:

```bash
cp etc/cowrie.cfg.dist etc/cowrie.cfg
```

The configuration file can then be modified according to the requirements of the lab.

---

# 5. Troubleshooting Cowrie Startup

## Issue

When Cowrie was initially started, a **"file not found"** error was encountered even though the required files appeared to be present.

## Investigation

The issue was related to how Cowrie was installed and registered inside the Python virtual environment.

## Resolution

Cowrie was installed in editable mode using:

```bash
pip install -e .
```

The installation was then verified with:

```bash
which cowrie
```

This confirmed that the Cowrie executable was available within the active environment.

## Starting Cowrie

Cowrie can then be started with:

```bash
cowrie start
```

Its status can be checked with:

```bash
cowrie status
```

---

# 6. Tools & Technologies

| Component               | Technology                 |
| ----------------------- | -------------------------- |
| Hypervisor              | Oracle VM VirtualBox       |
| Attacker System         | Ubuntu                     |
| Honeypot System         | Ubuntu Minimal             |
| Honeypot                | Cowrie                     |
| Services Monitored      | SSH / Telnet               |
| Virtual Networking      | Internal Network / NAT     |
| Programming Environment | Python Virtual Environment |
| Version Control         | Git                        |

---

# 7. Lab Architecture

The basic lab structure consists of two virtual machines communicating through a controlled virtual network:

```text
                    VirtualBox Host
                          |
              -------------------------
              |                       |
       Attacker VM              Honeypot VM
         Ubuntu                    Ubuntu
            |                        |
            |                        |
            +---- Internal Network --+
                                     |
                                  Cowrie
                               SSH / Telnet
                                  Honeypot
```

The attacker machine interacts with the honeypot, while Cowrie records relevant interactions and authentication attempts.

---

# 8. Lab Capabilities

The completed lab can be used for controlled cybersecurity exercises such as:

* Simulating SSH authentication attempts.
* Observing honeypot interactions.
* Capturing login attempts through Cowrie.
* Reviewing Cowrie logs.
* Performing basic network discovery within the isolated lab.
* Identifying exposed services.
* Analyzing activity between the two virtual machines.

All testing should remain within the authorized lab environment.

---

# 9. Outcome

By completing this project, I was able to:

* Build an Ubuntu-based cybersecurity lab using VirtualBox.
* Configure an Ubuntu attacker environment.
* Deploy a minimal Ubuntu server as a honeypot.
* Install and configure Cowrie.
* Establish communication between the virtual machines.
* Troubleshoot virtualization, networking, and Cowrie installation issues.
* Verify that the Cowrie service could be started and monitored.
* Create an environment for practicing security monitoring and analyzing simulated attacker activity.

---

# 10. Key Learning

This project provided practical experience with:

* Virtual machine deployment.
* Linux server administration.
* Ubuntu command-line operations.
* Virtual networking.
* Python virtual environments.
* Git and GitHub repositories.
* Honeypot deployment.
* Security monitoring.
* Log analysis.
* Basic troubleshooting.

It also demonstrated how a controlled virtual lab can be used to safely practice cybersecurity concepts without testing against unauthorized systems.
