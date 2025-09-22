# Network Reconnaissance with Nmap

## Objective

Discover devices and open ports on my local network to understand service exposure and potential risks.

## Steps Performed

1. **Installed Nmap**

   * Downloaded Nmap `.mpkg` installer and cleared macOS quarantine attributes (`xattr -r -d com.apple.quarantine`).
   * Verified installation with:

     ```bash
     nmap --version
     ```

2. **Identified Local IP and Subnet**

   * Ran:

     ```bash
     ifconfig
     ```
   * Found active interface `en0` with IP `********` and subnet mask `********` → `********`.

3. **Host Discovery (Ping Scan)**

   * Enumerated live hosts on the network:

     ```bash
     sudo nmap -sn ********
     ```
   * Detected 11 active devices (router, Apple devices, IoT devices, etc.).

4. **Port Scanning (TCP SYN Scan)**

   * Performed a stealth scan of all hosts:

     ```bash
     sudo nmap -sS 1********-oN ~/Desktop/scan_results.txt
     ```
   * Collected open ports (e.g., SSH, HTTP, MySQL, VNC, Kerberos, UPnP).

5. **Service Version Detection**

   * Identified running services:

     ```bash
     nmap -sV 192.168.0.0/24
     ```
   * Example findings:

     * Router (`**********`): SSH, DNS, HTTP config page, UPnP.
     * My Mac (`*********`): MySQL, VNC, RTSP/AirTunes, Kerberos, Microsoft-DS.
     * Other hosts: iPhones exposing `62078/tcp` (sync), IoT with UPnP.

6. **Saved Results**

   * Output saved in both normal text (`scan_results.txt`) and XML (`scan_results.xml`) formats.

## Outcome

* Learned to use **Nmap** for host discovery and open port detection.
* Understood which services/devices are active on my LAN.
* Identified potential risks from open ports like **MySQL (3306/tcp)**, **VNC (5900/tcp)**, and **UPnP (1900/tcp)**.
