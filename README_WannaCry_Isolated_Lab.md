# WannaCry Ransomware Simulation --- Isolated Windows 7 Lab

> **Safety notice:** This repository documents an authorized, isolated
> virtual-machine lab for cybersecurity education. It does **not**
> distribute ransomware. Do not upload WannaCry, live malware samples,
> payloads, or infected VM images. Never reproduce this activity on
> systems or networks you do not own or have explicit permission to
> test.

## Project overview

This project records a home-lab exercise using Kali Linux as the testing
machine and Windows 7 as the target virtual machine. The goal was to
practise network discovery, service enumeration, vulnerability
assessment, and observation of ransomware impact in a controlled
environment.

**Important scope clarification:** Running a ransomware executable and
observing an encryption screen demonstrates execution and impact; by
itself, it does not prove that the executable exploited a particular
remote vulnerability. Keep the scan output and exact Metasploit module
details if you want to make a specific vulnerability claim.

## Lab environment

  Component           Role
  ------------------- --------------------------------------------------
  Kali Linux VM       Testing and assessment workstation
  Windows 7 VM        Intentionally vulnerable test target
  Oracle VirtualBox   Virtualization platform
  Network             Private lab network only; no third-party systems

Replace or add details only if you have verified them. Do not publish
your host machine's public IP, personal usernames, passwords, license
keys, or other sensitive information.

## What I did

1.  **Prepared the lab.** Started the Kali Linux and Windows 7 virtual
    machines in VirtualBox and used the Windows VM as the authorized
    target.
2.  **Checked network configuration.** Identified the machines' lab IP
    addresses so the assessment could be limited to the intended target.
3.  **Performed host discovery.** Used Nmap to identify reachable
    devices in the lab.
4.  **Enumerated services and assessed potential vulnerabilities.** Ran
    Nmap service/version and vulnerability checks against the Windows VM
    and reviewed the resulting output.
5.  **Reviewed the assessment results.** Used the findings to
    investigate which exposed service or vulnerability might be
    relevant. A finding should only be reported as confirmed when
    supported by the actual scan output and module documentation.
6.  **Observed ransomware impact in the isolated VM.** A file identified
    as `WannaCry.exe` was transferred to and executed on the Windows 7
    VM, after which a ransom-note screen and changes to the test
    environment were visible.
7.  **Recorded evidence.** Captured screenshots of the Windows VM and
    the Kali terminal for this report.

The public report intentionally omits executable malware, payload files,
and a copy-and-paste sequence for deploying ransomware. Screenshots and
written analysis are sufficient to demonstrate the learning outcomes.

## Technical accuracy: WannaCry and ports

WannaCry is known for spreading by exploiting a vulnerability in Windows
SMBv1 addressed by Microsoft security bulletin **MS17-010**. The
relevant SMB service is commonly associated with **TCP port 445**. **TCP
port 80 is normally HTTP**, not a printer port. Windows file and printer
sharing can involve SMB, while dedicated printing services commonly use
other ports.

Therefore, do not write that "port 80 for printing was the WannaCry
vulnerability" unless you have separate, reliable evidence for that
specific finding. A ransomware executable running successfully also does
not prove that an Nmap finding was exploitable or that a remote exploit
caused the execution. Review the original scan output, the exact module
name, and the Windows VM configuration before stating the root cause.

## Results and observations

-   Kali Linux and Windows 7 were running as separate virtual machines.
-   Network discovery and service/vulnerability enumeration were
    performed against the lab target.
-   The Windows VM displayed a ransom-note window after the test
    executable was run.
-   Screenshots were collected as evidence of the lab workflow and
    observed result.

**Evidence limitation:** A ransom note is evidence of observed
ransomware-like behaviour, but it is not enough on its own to establish
the binary's authenticity, the exact exploit path, the specific
vulnerability, or the full extent of file encryption. Avoid claiming
more than the evidence shows.

## Defensive lessons

1.  **Patch legacy systems.** Apply supported security updates and
    retire unsupported operating systems wherever possible.
2.  **Disable SMBv1 where it is not required.** Prefer modern, supported
    SMB configurations.
3.  **Restrict SMB exposure.** Do not expose TCP 445 to the public
    internet; filter unnecessary SMB traffic between network segments.
4.  **Maintain offline or immutable backups.** Test restoration
    procedures regularly.
5.  **Use endpoint protection and monitoring.** Investigate mass file
    modifications, suspicious process execution, unexpected SMB traffic,
    and ransom-note creation.
6.  **Prepare an incident-response procedure.** Isolate affected
    systems, preserve evidence, notify the responsible team, determine
    scope, and restore from known-good backups. Do not connect a
    suspected infected VM to a production network.
7.  **Use safe lab snapshots.** Take a clean VM snapshot before
    experiments and revert the VM afterward. Keep the lab network
    isolated from the host's sensitive files and other devices.

## Lab safety and cleanup

-   Keep vulnerable VMs on a host-only or otherwise isolated virtual
    network.
-   Disable shared folders, shared clipboard, drag-and-drop, and
    unnecessary host integration during malware exercises.
-   Do not bridge the vulnerable VM to a home, school, or workplace
    network.
-   Revert to a known-clean snapshot after the exercise; if the VM may
    be compromised, do not reuse it as a trusted machine.
-   Do not upload the ransomware executable, a malware archive, or the
    infected VM disk to GitHub.

## Suggested repository structure

``` text
wannacry-isolated-lab/
├── README.md
├── screenshots/
│   ├── lab-overview.png
│   └── observed-ransom-note.png
└── notes/
    └── defensive-lessons.md
```

Use only screenshots that you have reviewed for personal information.
The screenshots you supplied show a lab terminal and Windows desktop;
crop or blur any usernames, unrelated files, addresses, tokens, or other
details you do not want public. Keep the original malware binary out of
this repository.

## References

-   Microsoft Security Bulletin MS17-010:
    https://learn.microsoft.com/en-us/security-updates/securitybulletins/2017/ms17-010
-   Microsoft Security Intelligence --- WannaCry/WannaCrypt:
    https://www.microsoft.com/en-us/wdsi/threats/malware-encyclopedia-description?Name=Ransom%3AWin32%2FWannacrypt.A%21rsm
-   Nmap documentation for the MS17-010 detection script:
    https://nmap.org/nsedoc/scripts/smb-vuln-ms17-010.html
-   GitHub policy on active malware or exploits:
    https://docs.github.com/en/site-policy/acceptable-use-policies/github-active-malware-or-exploits

## Disclaimer

This is a learning exercise performed in a self-owned lab. It is not a
recommendation to deploy ransomware or test systems without
authorization. The report describes observations from the lab and should
not be interpreted as an independently verified forensic analysis of the
executable.
