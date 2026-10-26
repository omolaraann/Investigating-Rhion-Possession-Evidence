# 🦏 Investigating Rhion Possession Evidence

### Digital Forensics Investigation | USB Storage Forensics | Network Traffic Analysis | Evidence Recovery

---

## 🔎 Project Overview

This project documents a digital forensics investigation conducted as part of the **SBT-DF204 Digital Forensics case study**. The investigation focuses on examining a supplied USB storage image and associated network traffic artefacts to identify, recover, analyse, and document digital evidence relevant to the case.

The investigation combines file-system examination, evidence hashing, data carving, string analysis, HTTP request analysis, FTP activity review, and Telnet session analysis. The work demonstrates how different sources of digital evidence can be examined and correlated to develop a structured account of potentially relevant activity.

The project includes the original case archive, extracted forensic artefacts, analysis outputs, recovered-file metadata, network investigation results, and evidence integrity records. A detailed written report and supporting screenshots can be added to the `report/` and `investigation/screenshots/` directories as the documentation is finalised.

> **Investigation principle:** Findings should be supported by observable artefacts, documented analysis steps, and verifiable evidence. An artefact that suggests an action does not automatically prove that the action was completed or that a particular person performed it.

## 🎯 Investigation Objectives

The investigation was designed to:

- 🔍 Examine the supplied forensic evidence and identify relevant digital artefacts.
- 💾 Inspect the USB storage image and establish the file-system context of the available data.
- 🧾 Calculate and document cryptographic hashes to support evidence integrity and reproducibility.
- 🗂️ Examine allocated files and identify potentially relevant file-system contents.
- 🧩 Analyse unallocated data for remnants of deleted or otherwise unallocated content.
- 🖼️ Identify and recover GIF files through file carving, then document the resulting artefacts.
- 🌐 Examine network traffic for HTTP requests, file-transfer activity, and interactive remote-session data.
- 📡 Investigate FTP activity, including file-transfer commands and associated session artefacts.
- 💻 Examine Telnet streams for readable session data and authentication-related activity.
- 🔗 Correlate findings from storage and network artefacts where the available evidence supports a relationship.
- 📝 Document the tools, commands, observations, limitations, and findings in a reproducible investigation structure.

## 🧰 Tools and Technologies

The investigation uses a combination of command-line utilities and network-analysis techniques in a Linux forensic environment.

| Tool or technique | Purpose |
|---|---|
| 🐉 Kali Linux | Investigation environment for forensic analysis and command-line examination |
| 🔐 SHA-256 hashing | Evidence integrity verification and identification of forensic artefacts |
| 🗃️ File-system examination | Inspection of the USB image and its available file-system contents |
| 🧵 String analysis | Extraction and examination of readable text from files and unallocated data |
| 🪓 Foremost | File carving to identify and recover files from data signatures |
| 🖼️ GIF structural analysis | Examination of recovered GIF artefacts and their technical characteristics |
| 🌐 Wireshark / TShark analysis | Examination of network traffic, protocol conversations, and reconstructed streams |
| 📡 HTTP analysis | Identification and examination of HTTP requests and responses |
| 📂 FTP analysis | Review of file-transfer commands and related session data |
| 🖥️ Telnet analysis | Examination of interactive session streams and readable protocol data |
| 🧾 Git and GitHub | Version control and documentation of the investigation project |
| 📦 Git LFS | Storage of large forensic binary files when required and supported by repository quotas |

*The table identifies the tools and techniques used or documented for this investigation. Individual report sections should identify the exact tool version and command used wherever that information is available.*

## 🗂️ Repository Structure

The repository is organised to separate source evidence, extracted artefacts, analysis outputs, notes, screenshots, and formal reporting.

```text
Investigating-Rhion-Possession-Evidence/
│
├── 📄 README.md
├── 📑 Investigating Rhion Possession Evidence.pdf
│
├── 📁 evidence/
│   ├── 📁 original/
│   │   └── DFRWS2005-RODEO.zip
│   │
│   └── 📁 working/
│       └── 📁 DFRWS2005-RODEO/
│           ├── RHINOUSB.dd
│           ├── rhino.log
│           ├── rhino2.log
│           └── rhino3.log
│
├── 📁 investigation/
│   ├── 📁 notes/
│   │   └── extracted_evidence_hashes.txt
│   │
│   ├── 📁 output/
│   │   ├── 📄 gumbo1.txt
│   │   ├── 📄 gumbo2.txt
│   │   ├── 📄 usb_file_listing.txt
│   │   │
│   │   ├── 📁 carving/
│   │   │   └── 📁 foremost_gif/
│   │   │       ├── audit.txt
│   │   │       └── 📁 gif/
│   │   │           ├── 00106320.gif
│   │   │           └── 00106344.gif
│   │   │
│   │   ├── 📁 giftext/
│   │   │   ├── 00106320_giftext.txt
│   │   │   ├── 00106320_identify_errors.txt
│   │   │   ├── 00106344_giftext.txt
│   │   │   └── 00106344_identify_errors.txt
│   │   │
│   │   ├── 📁 network/
│   │   │   ├── ftp_data_summary.txt
│   │   │   ├── ftp_selected_streams.txt
│   │   │   ├── rhino_http_requests.txt
│   │   │   ├── rhino2_http_requests.txt
│   │   │   ├── rhino3_http_requests.txt
│   │   │   ├── telnet_ftp_summary.txt
│   │   │   ├── telnet_interactive_data.txt
│   │   │   └── telnet_streams.txt
│   │   │
│   │   └── 📁 unallocated/
│   │       ├── unallocated_strings.txt
│   │       └── usb_unallocated.bin
│   │
│   ├── 📁 screenshots/
│   └── 📁 timeline/
│
└── 📁 report/
```

*This is a representation of the intended project structure. The repository contents may change as the report, screenshots, and additional documentation are added.*

## 💾 Evidence Acquisition and Integrity

The investigation is based on the supplied `DFRWS2005-RODEO` evidence archive and its extracted contents.

The original archive and working artefacts are kept in separate directories to distinguish the supplied evidence from the files used during examination.

### 🔐 Evidence integrity

Cryptographic hashes are documented in:

`investigation/notes/extracted_evidence_hashes.txt`

The hash records provide a means of identifying files and checking whether their contents have changed. Where an original evidence hash is available, it should be compared with the hash of the corresponding working copy before relying on the copy for further examination.

### 📦 Evidence handling principles

- Preserve the original evidence and avoid modifying it during analysis.
- Conduct examination using working copies where possible.
- Record hashes for original and derived artefacts.
- Document the commands and tools used to generate investigation outputs.
- Keep recovered files distinguishable from original evidence.
- Record any transformation, extraction, redaction, or other modification performed on a publication copy.
- Avoid treating an extracted or recovered file as an original source artefact without documenting its origin.

## 🗃️ USB Storage and File-System Examination

The USB storage image, `RHINOUSB.dd`, was examined to understand its file-system contents and identify artefacts relevant to the case.

The available outputs include:

- `investigation/output/usb_file_listing.txt` — a record of the identified file listing.
- `investigation/output/gumbo1.txt` and `gumbo2.txt` — extracted text artefacts identified during the examination.
- `investigation/notes/extracted_evidence_hashes.txt` — recorded evidence hashes.

The file listing and extracted text outputs provide supporting material for describing the observed file-system contents. Interpretations should be tied to the actual output and should distinguish between file presence, file content, and conclusions about how or why a file came to be present.

## 🧩 Unallocated-Space Analysis and File Carving

Unallocated data was examined for remnants of files that were not represented as ordinary allocated files in the examined file-system context.

The relevant outputs are stored under:

`investigation/output/unallocated/`

and

`investigation/output/carving/foremost_gif/`

### 🪓 File carving

Foremost was used to identify and recover GIF-format artefacts based on file signatures. The recovered files are recorded as:

- `00106320.gif`
- `00106344.gif`

The carving audit file documents the recovery output:

`investigation/output/carving/foremost_gif/audit.txt`

Text-based examination outputs for the recovered files are stored in:

`investigation/output/giftext/`

These files support the documentation of the carving and subsequent technical examination. File carving can recover content without restoring the original filename, directory path, or complete file-system metadata. Therefore, a recovered file's original name, ownership, creation time, and relationship to a user should not be asserted unless independently supported by additional evidence.

## 🌐 Network Traffic Investigation

The investigation also examines three network-analysis logs associated with the case:

- `rhino.log`
- `rhino2.log`
- `rhino3.log`

Protocol-specific outputs are organised under:

`investigation/output/network/`

The investigation focuses on HTTP activity, FTP file transfers, and Telnet interactive sessions. These protocols can reveal information about requests, responses, transferred filenames, and readable session content, depending on what was captured.

### 🌍 HTTP analysis

The HTTP request outputs are:

- `rhino_http_requests.txt`
- `rhino2_http_requests.txt`
- `rhino3_http_requests.txt`

These outputs are used to examine observed web requests and related HTTP activity. The analysis includes a reported HTTP response associated with a file named `rhino.exe`. The response and any executable-file indicators should be documented as observations from the captured traffic.

The presence of an executable download does not, on its own, establish that the file was executed, that it was malicious, or that a particular endpoint was compromised. Those conclusions require corroborating evidence.

### 📂 FTP analysis

FTP-related analysis outputs include:

- `ftp_data_summary.txt`
- `ftp_selected_streams.txt`
- `telnet_ftp_summary.txt`

The recorded analysis includes FTP `STOR` activity associated with filenames such as `rhino1.jpg`, `rhino3.jpg`, and `contraband.zip`.

The outputs should be used to distinguish observed transfer commands from assumptions about the contents or purpose of transferred files. Where a filename appears in a protocol stream, that filename alone does not establish the contents of the transferred object.

### 🖥️ Telnet session analysis

The Telnet-related outputs include:

- `telnet_interactive_data.txt`
- `telnet_streams.txt`
- `telnet_ftp_summary.txt`

These files contain extracted or reconstructed session data for examination. Telnet does not encrypt its traffic by default, so captured sessions may contain readable commands, prompts, and authentication-related content.

Authentication material should be handled carefully when publishing analysis outputs. Any redaction made to a publication copy should be documented, and the original forensic artefact should remain unchanged in the evidence-preservation workflow.

## 🔗 Correlation of Findings

A key aspect of the investigation is to consider the storage and network evidence together, rather than treating each output in isolation.

Potential lines of correlation include:

- 🔍 Comparing filenames found in network traffic with files identified during storage examination.
- 🧩 Examining whether recovered artefacts are consistent with other documented findings.
- 🌐 Comparing activity across the available network logs.
- 🕒 Developing a timeline when reliable timestamps and supporting artefacts are available.
- 🔐 Using hashes to identify identical files or distinguish different versions of an artefact.

Correlation should be based on specific, documented evidence. Similar filenames, file types, or subject matter can suggest a relationship, but do not independently prove that two artefacts are the same file or that they originated from the same action.

## 📌 Key Observations

The available investigation outputs support the following areas of examination:

- 💾 **USB evidence:** A disk image and associated file-system examination outputs were available for analysis.
- 🗂️ **Allocated content:** Text artefacts were extracted and documented.
- 🧩 **Unallocated content:** Unallocated data was examined, and GIF-format artefacts were recovered through file carving.
- 🌐 **HTTP activity:** HTTP request outputs were generated for the available network logs.
- 📂 **FTP activity:** FTP-related outputs document file-transfer activity and associated session information.
- 🖥️ **Telnet activity:** Interactive session data was extracted for examination.
- 🔐 **Integrity records:** Hash values were recorded to support evidence identification and integrity checks.

These are summary observations of the investigation scope and available outputs. The final report should provide the detailed supporting artefacts, relevant timestamps, commands, and interpretation for each substantive finding.

## ⚠️ Limitations and Considerations

The conclusions of a digital forensics investigation depend on the completeness, integrity, and context of the available evidence.

- 📦 **Evidence scope:** Conclusions are limited to the supplied archive, disk image, network logs, and derived artefacts examined.
- 🧩 **Recovery limitations:** File carving may recover partial content and may not preserve original file-system metadata.
- 🌐 **Network visibility:** A capture may omit traffic, contain incomplete sessions, or lack context available from the original endpoint.
- 🔐 **Protocol limitations:** Readable protocol data can expose commands and authentication-related material, but interpretation still requires session context.
- 🧾 **Attribution:** An IP address, filename, account string, or command does not independently identify the human responsible for an activity.
- 🦠 **Malware conclusions:** A filename or executable signature alone is insufficient to establish maliciousness or successful execution.
- 🕒 **Timeline accuracy:** Any event chronology should account for the source and reliability of timestamps and possible differences between systems.
- 📑 **Documentation completeness:** Detailed conclusions, screenshots, tool versions, and command outputs should be included in the final report where available.

## 🛡️ Evidence Preservation and Responsible Publication

This repository is intended to document a forensic investigation and its supporting analysis. Evidence integrity and responsible handling remain important when publishing the project.

- 🔒 Preserve original evidence and retain its recorded hashes.
- 🧾 Clearly distinguish original files from derived analysis outputs.
- 🧹 Document any redaction applied to a publication copy.
- 🔑 Avoid exposing real credentials, access tokens, personal information, or other secrets in documentation.
- 📦 Confirm that source evidence may be redistributed before publishing it publicly.
- 🖼️ Review recovered files and their contents before making them publicly accessible.
- 📚 Credit the original dataset or source where appropriate and include applicable licence information.

A public repository is not a substitute for a controlled evidence store. If the evidence contains sensitive material, access and redistribution should be considered separately from the integrity of the local forensic originals.

## 📁 Project Documentation

The following locations are intended for supporting materials:

| Location | Contents |
|---|---|
| `report/` | Formal investigation report, findings, conclusions, and recommendations |
| `investigation/screenshots/` | Screenshots illustrating commands, tool outputs, and analysis steps |
| `investigation/notes/` | Hashes and supporting investigation notes |
| `investigation/output/` | Extracted, reconstructed, and analysed artefacts |
| `evidence/original/` | Supplied source evidence |
| `evidence/working/` | Working copies used during examination |

Additional documentation can be added as the investigation report and screenshots are finalised.

## 🧠 Skills Demonstrated

This project provides practical evidence of work involving:

- 🔍 Digital evidence examination and documentation.
- 🔐 Cryptographic hashing and evidence integrity.
- 💾 USB storage and file-system analysis.
- 🧩 Unallocated-space analysis and file carving.
- 🧵 String extraction and artefact examination.
- 🌐 HTTP request and response analysis.
- 📂 FTP protocol and file-transfer analysis.
- 🖥️ Telnet stream examination.
- 🔗 Evidence correlation and cautious interpretation.
- 📝 Forensic reporting and reproducible investigation workflows.
- 🐙 Git-based version control and technical portfolio documentation.

## 🏁 Conclusion

The case study brings together storage forensics, unallocated-space examination, file carving, and network protocol analysis in a single documented investigation. By organising the source evidence, derived artefacts, hashes, and analysis outputs into a structured repository, the project supports transparent review and reproducibility.

The strength of any final conclusion depends on the supporting evidence and the limits of the examination. Findings should therefore be reported with appropriate context, clearly separated from assumptions, and supported by the relevant artefacts.

---

### 👩🏽‍💻 About This Project

**Project:** Investigating Rhion Possession Evidence  
**Domain:** Digital Forensics and Incident Investigation  
**Case Study:** SBT-DF204  
**Environment:** Kali Linux  
**Repository:** [Investigating Rhion Possession Evidence](https://
