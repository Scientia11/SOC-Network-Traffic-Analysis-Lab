## 📌 Overview

This report documents the analysis of a packet capture (**PCAP**) file from a compromised host using `tcpdump`. The goal was to identify indicators of compromise (IOCs) and determine whether malicious activity occurred.

---

## 🚨 Indicators of Compromise (IOCs)

### 1. Suspicious File Download

* A **GET request** was observed from the internal host:

  ```
  10.0.0.1.68 → 103.232.55.148
  ```
* The request downloaded an executable file:

  ```
  /.audiodg.exe
  ```
* ⚠️ **Suspicion:**

  * The filename includes a **leading dot (`.audiodg.exe`)**, which is an unusual naming convention often used to evade detection or mimic legitimate files.

---

### 2. Masquerading as Legitimate System File

* The file name **audiodg.exe** resembles a legitimate Windows process:

  * *Windows Audio Device Graph Isolation* (`audiodg.exe`)
* ⚠️ **Suspicion:**

  * The file was **not downloaded from an official Microsoft source**
  * Indicates **possible masquerading attack**

---

### 3. Malicious External IP

* The destination IP:

  ```
  103.232.55.148
  ```
* IP lookup results:

  * Geolocation: Viet Nam
  * No affiliation with Microsoft
* ⚠️ **Suspicion:**

  * External, untrusted source unrelated to legitimate software distribution

---

### 4. Suspicious URL Structure

* The GET request contained encoded query parameters
* After decoding:

  * The URL used a **raw IP address instead of a domain name**
  * Communication occurred over **unencrypted HTTP**
* ⚠️ **Suspicion:**

  * Use of IP-based URLs and HTTP is common in **malware delivery infrastructure**

---

### 5. VirusTotal Detection

* The decoded URL was analyzed using **VirusTotal**
* Results:

  * Flagged as malicious by **6 security vendors**
* ⚠️ **Suspicion:**

  * Confirms known malicious indicators

---

### 6. Executable Signature in Packet Data

* ASCII output from captured packets revealed the string:

  ```
  "This program cannot be run in DOS mode"
  ```
* ⚠️ **Analysis:**

  * This string is commonly found in **Windows PE (Portable Executable)** files
  * Confirms that the downloaded file is an executable binary

---

## 🧠 Analysis Summary

The observed network activity strongly indicates a **malicious payload delivery attempt**:

* Unauthorized executable download
* Use of deceptive file naming
* Delivery from an untrusted external IP
* Suspicious URL encoding techniques
* Confirmation from threat intelligence sources
* Presence of executable file signatures in packet data

---

## ⚠️ Conclusion

Based on the analysis:

> The file `/.audiodg.exe` is **malicious** and was likely delivered to compromise the host system.

This activity represents a **potential malware infection vector**, and immediate remediation actions are recommended.

---

## 🛡️ Recommended Actions

* Isolate the affected host from the network
* Block the IP: `103.232.55.148`
* Perform full system malware scan
* Check for persistence mechanisms
* Monitor for further suspicious traffic

