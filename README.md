# CWE Agent Assignment Reports (2025)

This repository contains **automatically generated reports** assigning **CWE categories** to **9,552 CVEs** using a hybrid RAG + LLM approach. It is designed to support CNAs, researchers, and security practitioners by offering **transparent, traceable, and human-readable CWE mapping reports**.

## Method Overview

This pipeline combines **retrieval-augmented generation (RAG)** with **LLM-based reasoning**:

* **CWE Content Retrieval**
  Both semantic and lexical search is used to shortlist relevant CWE entries from the [CWE List Version 4.17](https://cwe.mitre.org/data/published/cwe_v4.17.pdf), based on the description and extracted keyphrases, and reference content summary.

* **LLM-based Assignment**
  An LLM assigns the most appropriate CWE(s) using:

  * The CVE description
  * Extracted keyphrases [`cve_info/`](https://github.com/CyberSecAI/cve_info) following the [CVE Key Details Phrasing Guide](https://www.cve.org/Resources/General/Key-Details-Phrasing.pdf).
  * Summarized reference content  [`cve_info_refs/`](https://github.com/CyberSecAI/cve_info_refs/) from CVE “References to Advisories, Solutions, and Tools”
  * Retrieved CWE definitions from CWE List 4.17

For details, see [Vulnerability Root Cause Mapping with CWE](https://www.youtube.com/watch?v=TH1tGO15K24&list=PLBAUUhONOrO8iOYvs3pAbuzb-A07ZdT9C&index=2), Alec Summers, Chris Madden, FIRST VulnCon, May 2025



## 📄 How to Use

The repo contains a flat directory of CVEs e.g. https://github.com/CyberSecAI/cwe_agent_assign_reports_2025/blob/main/CVE-2024-10765/. This directory contains a list of files.
| File                                                                                                                                                                          | Description                                                           |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------- |
| [`CVE-2024-10019_report.md`](https://github.com/CyberSecAI/cwe_agent_assign_reports_2025/blob/main/CVE-2024-10019/CVE-2024-10019_report.md)                                   | **_report.md** is the output: intended for human review by CNA/researcher             |                    |
| [`CVE-2024-10765_analyzer_enhanced_input.md`](https://github.com/CyberSecAI/cwe_agent_assign_reports_2025/blob/main/CVE-2024-10765/CVE-2024-10765_analyzer_enhanced_input.md) | **_analyzer_enhanced_input.md** is the input for an LLM or human: includes keyphrases, references summary, and CWE shortlist |


---

---

## ⏱️ Processing Time


| Stage                | Time                 | Notes |
| -------------------- | -------------------- | --|
| Retrieval (Pre-LLM)  | 17 hours, 20 minutes | Creating the embeddings per CVE for semantic comparison is the longest operation|
| CWE Assignment (LLM) | *TBD*                | The LLM review of the input content, and the generation of the report, per CVE, is the longest operation|



---




## 📊 CWE Mapping Sets

These repositories contain **automatically generated reports** assigning **CWE categories** to CVEs in the Top25 subset for each year, where the subset is the CVEs where MITRE deemed the CWE mapping by CMAs should be corrected:
* [Top 25 - 2025 ](https://github.com/CyberSecAI/cwe_agent_assign_reports_2025)
* [Top 25 - 2023](https://github.com/CyberSecAI/cwe_agent_assign_reports_2023)
* [Top 25 - 2022](https://github.com/CyberSecAI/cwe_agent_assign_reports_2022)

The [Observed CVEs (CWE List)](https://github.com/CyberSecAI/cwe_agent_assign_reports_observed)  is the list of CVEs from the CWE List Observed Examples.

---

## 🛠️ Notes

* All reports are in **Markdown** format for easy processing by both humans and LLMs.
* The repo contains **all intermediate processing artifacts** for transparency—though not all are relevant to end users.
