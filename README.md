# Assignmnet-10-
## Assignment #10 — Anti-Malware Detection using ClamAV

### Objective
Installed, configured, and operated ClamAV, an open-source antivirus engine, to perform system scans, detect malicious files, and manage malware threats on a local Linux system.

### Tools Used
- ClamAV (clamav, clamav-daemon)
- freshclam (virus signature database updater)
- clamscan (scanning engine)
- Kali Linux

### Process

**1. Installation**
Installed ClamAV and its daemon service on Kali Linux.

```bash
sudo apt update
sudo apt install clamav clamav-daemon -y
```

**2. Updating the Virus Signature Database**
Used freshclam to download and update the latest virus definitions before scanning.

```bash
sudo systemctl stop clamav-freshclam
sudo freshclam
```

Result: main.cvd and bytecode.cvd successfully updated to the latest available versions.

**3. Creating a Test Malware Sample (EICAR)**
Created a standard EICAR test file — a harmless string universally recognized by antivirus engines as a safe way to test detection capability.

```bash
mkdir ~/malware_test
cd ~/malware_test
echo 'X5O!P%@AP[4\PZX54(P^)7CC)7}$EICAR-STANDARD-ANTIVIRUS-TEST-FILE!$H+H*' > eicar.txt
```

**4. Scanning for Threats**
Performed a recursive directory scan using clamscan.

```bash
clamscan -r /home/kali/malware_test
```

Result:

**5. Quarantine / Removal**
Re-ran the scan with the --remove flag to automatically delete the detected threat.

```bash
clamscan -r --remove /home/kali/malware_test
```

Result:

Verified the directory was clean afterward:
```bash
ls ~/malware_test
```

### Key Takeaway
Antivirus engines like ClamAV are a critical layer of defense, but they are only as effective as their signature database. Regular updates (via freshclam) and scheduled scans are essential to maintaining a secure system posture.

### Best Practices
| Practice | Purpose |
|---|---|
| Regular signature updates (freshclam) | Ensures detection of newly identified threats |
| Scheduled scans | Catches malware before it can cause damage |
| Quarantine/removal policies | Prevents further execution of detected threats |
| Layered security | Antivirus should be paired with firewalls, monitoring, and safe user practices |

---

*This assignment was conducted strictly in a controlled, local, and safe lab environment for educational purposes only, as part of The Techzeen Cyber Security course under the guidance of instructor Farzeen Ali.*
