# Img.cartel-Analysis report

# Malware Analysis Report: `cartel.img`

## Submitted By

- **Name:** Miracle Ezenwa
- **Course:** Cybersecurity
- **Assignment:** Malware Analysis of `cartel.img`

---

# Task One: File Identification and Hash Analysis

## Objective

The purpose of this task is to identify the malware sample and document its basic forensic properties. Cryptographic hash values provide a unique fingerprint of the file, enabling analysts to verify its integrity and compare it against malware databases.

---

## File Information

| Property | Value |
|----------|-------|
| **File Name** | `cartel.img` |
| **MD5 Hash** | `80348c58eec4c328ef1f7709adc56a54` |
| **SHA-256 Hash** | `ce550424200a997c61b413941c8ef4df9619a2f96579674952294a176a32be65` |
| **File Size** | `248MB` |
| **File Type / Permissions** | `-rw-rw-r--` |
| **Architecture** | FAT `16-bit` |

---

## Why Malware Analysts Calculate File Hashes Before Investigation

Malware analysts calculate file hashes before beginning an investigation because hash values act as unique digital fingerprints of a file. Algorithms such as **MD5** and **SHA-256** generate unique identifiers that allow analysts to verify file integrity and confirm that the sample has not been modified during acquisition, transfer, or analysis.

Hash values also enable investigators to compare a malware sample against public malware repositories, antivirus databases, and threat intelligence platforms. If a matching hash already exists, analysts can quickly determine whether the file is a known threat and obtain additional intelligence about its behavior.

Furthermore, hash values make it easier for security professionals to share malware indicators without distributing the malicious file itself. This supports collaboration while preserving forensic integrity throughout the investigation.

# Static Malware Analysis Findings


## Analysis Summary

| Item | Possible Finding |
|------|-------------!*Suspicious Embedded Strings** | URLs or IP addresses, PowerShell commands, `cmd.exe`, `rundll32.exe`, `regsvr32.exe`, registry paths such as sorry,`Software\Microsoft\Windows\CurrentVersion\Run, Base64-encoded strings, mutex names, error messages, and references to Windows API functions. |
| **Suspicious Embedded Functions** | `CreateProcess()`, `WinExec()`, `ShellExecute()`, `VirtualAlloc()`, `WriteProcessMemory()`, `CreateRemoteThread()`, `InternetOpenUrl()`, `URLDownloadToFile()`, `WSAStartup()`, `RegSetValueEx()`, `OpenProcess()`, `CreateFile()`, `WriteFile()`, and `Sleep()`. These APIs are commonly associated with process execution, code injection, networking, persistence, and file manipulation. |

**Whether the sample is packed or not**
  The sample is not packed 43%

| **Compiler**  the sample is a Windows non-PE executable, analysis tools may identify compilers such as **Microsoft Visual C++**, **MinGW GCC**, **Delphi**, or **Borland**. Malware authors may remove or modify compiler information to hinder attribution. |
| **Version Information** | Malware often contains missing, empty, or falsified version information. Unlike legitimate software, fields such as **Company Name**, **Product Name**, **File Description**, and **File Version** may be absent or intentionally forged. |

---

# Interpretation of the Findings about what they reveal about malware.

## Suspicious Embedded Strings

Suspicious strings can reveal the malware's intended capabilities.command interpreters, registry paths, encoded data, file system locations, and network indicators,such as sorry. These strings may suggest that the malware is capable of executing commands, modifying the Windows Registry, storing files in hidden directories, or communicating with remote servers.

## Suspicious Embedded Functions

The presence of Windows API functions provides insight into the malware's behavior. Functions related to process creation, memory allocation, code injection, registry modification, networking, and file operations indicate capabilities such as downloading additional payloads, injecting malicious code into other processes, maintaining persistence, stealing information, or communicating with command-and-control (C2) servers.e.g charlie

## Compiler Information

Compiler metadata can help analysts determine the development environment used to build the malware. Identifying the compiler may assist in malware family attribution and provide clues about the author's development practices. However, sophisticated malware often removes or alters this information to evade analysis.

## Version Information

Version metadata is useful for determining whether an executable appears legitimate. Genuine software typically contains descriptive information such as the company name, product name, version number, and file description. Malware frequently omits or falsifies this metadata to impersonate legitimate applications or avoid detection.

## Behavioral Analysis Summary

| Category | Possible Findings |
|----------|-------------------|
| **Files Created** | The malware may create executable files in directories such as `%AppData%`, `%Temp%`, `%ProgramData%`, or `%SystemRoot%`. It may also generate DLL files, configuration files, log files, or copies of itself using deceptive filenames such as `svchost.exe` or `update.exe` to evade detection. |
| **Registry Changes** | Possible modifications include adding autorun entries under `HKCU\Software\Microsoft\Windows\CurrentVersion\Run` or `HKLM\Software\Microsoft\Windows\CurrentVersion\Run`, altering Windows Defender settings, modifying file associations, or creating registry keys to store malware configuration and maintain persistence. |
| **Network Processes and Activity** | The malware may perform DNS lookups, establish HTTP/HTTPS connections to command-and-control (C2) servers, download additional payloads, upload stolen data, beacon to remote IP addresses, open unusual network ports, or use encrypted outbound communications to conceal its activity. |
| **Persistence Mechanisms** | Persistence may be achieved through Scheduled Tasks, Windows Services, Startup folder shortcuts, `Run` and `RunOnce` registry keys, WMI event subscriptions, DLL hijacking, or modifications to critical system files. |
| **Child Processes** | The malware may launch legitimate Windows utilities such as `cmd.exe`, `powershell.exe`, `wscript.exe`, `cscript.exe`, `rundll32.exe`, or `regsvr32.exe`, or spawn additional malicious processes to execute payloads, bypass security controls, or evade detection. |

---

# Interpretation of the Findings

## Files Created

Malware commonly creates additional files to store its payloads, configuration data, logs, or temporary information. Using trusted directory locations and legitimate-looking filenames helps the malware blend in with normal system activity and avoid detection.

## Registry Changes

Registry modifications are often used to establish persistence so that the malware automatically executes when the system starts or a user logs in. Registry keys may also store configuration settings or disable security features to make removal more difficult.

## Network Processes and Activity

Network communication enables malware to receive commands from attackers, exfiltrate sensitive information, download additional malware components, and maintain communication with command-and-control (C2) infrastructure.

## Persistence Mechanisms

Persistence techniques ensure that the malware remains active even after a system reboot or user logoff. These mechanisms make the infection more resilient and increase the likelihood that attackers maintain long-term access to the compromised system.

## Child Processes

The creation of child processes allows malware to execute additional commands, launch scripts, inject code into legitimate applications, or perform malicious actions while attempting to evade security monitoring.

<img width="1306" height="1204" alt="file_00000000dad08243b0352d4d52a42f8b" src="https://github.com/user-attachments/assets/e9bcdd8b-859c-4433-b2db-23b3d9629502" />


---

