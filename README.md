# CWE Agent Assignment Reports (MITRE Top25 2025)

This repository contains **automatically generated reports** assigning **CWEs** to **9,552 CVEs** using a hybrid RAG + LLM approach. 

- It is designed to support CNAs, researchers, and security practitioners by offering **transparent, traceable, and human-readable CWE mapping reports**.
- For each CVE, it creates files 
  - **_analyzer_enhanced_input.md** (used as an input to an agent (human or LLM) to assign CWEs) e.g. [`CVE-2024-10019_analyzer_enhanced_input.md`](./cve/CVE-2024-10019/CVE-2024-10019_analyzer_enhanced_input.md) contains:
    - CVE Description
    -  [Extracted keyphrases](https://github.com/CyberSecAI/cve_info) following the [CVE Key Details Phrasing Guide](https://www.cve.org/Resources/General/Key-Details-Phrasing.pdf)
    - [Summarized reference content](https://github.com/CyberSecAI/cve_info_refs/) from CVE “References to Advisories, Solutions, and Tools” (if available; if the reference links allow crawling)
    - [Consensus CWE](https://github.com/CyberSecAI/cve_dedup) where ~~15% of CVE Descriptions are very similar to others and tend to have the same CWEs assigned (if available)
    - Shortlist of candidate CWEs based on Hybrid RAG
      - Both semantic and lexical search is used to shortlist relevant CWE entries from the [CWE List Version 4.17](https://cwe.mitre.org/data/published/cwe_v4.17.pdf), based on the description and extracted keyphrases, and reference content summary.
  - **_report.md** e.g. [`CVE-2024-10019_report.md`](./cve/CVE-2024-10019/CVE-2024-10019_report.md)
    - is the CWE assignment report created by the LLM

> [!TIP]
> For details on this approach, see [Vulnerability Root Cause Mapping with CWE](https://youtu.be/TH1tGO15K24?t=948), Alec Summers, Chris Madden, FIRST VulnCon, May 2025.


> [!TIP]
> **See [index of CVEs](./index.md) that lists all processed CVEs and links to their directory.**
 
> [!WARNING]  
> This repository contains **automatically generated reports** assigning **CWEs** to CVEs in the 2025 Top25 subset of CVEs where MITRE deemed the CWE mapping by CNAs should be corrected.
>
> There is no guarantee or validation that the CWEs assigned here are correct - but the information is useful for reference - especially the **_analyzer_enhanced_input.md** that gathers the information for CWE assignment by an agent (human or LLM).  
>
> Example: [CVE-2024-10019](./cve/CVE-2024-10019/CVE-2024-10019_report.md) assigns CWE-78: OS command injection because "OS command injection" is part of the CVE Description. A detailed analysis of the underlying reference https://huntr.com/bounties/3cf80890-2d8a-4fc7-8e0e-6d4bf648b3ea shows that the underlying rootcauses were path traversal, and the ability to specify arbitrary python code to run (including but not limited to OS commands) so technically not OS command injection.

> [!WARNING]  
> The report CWE "Relationship Analysis" diagram generation is in alpha state.

 ## Using LLMs for CWE Assignment
[LLMs can complement and fall short](https://youtu.be/TH1tGO15K24?t=2405) in CWE assignment.  

A [CWE CVE Benchmark](https://cwe-cve-benchmark.github.io/) is being developed as part of a MITRE community collaboration to improve CWE mappings solutions.




## Processing Time and Cost

| Stage                | 💲Cost       | ⏱️ Time                 | Notes                                                                                   |
| -------------------- | ------- | -------------------- | ---------------------------------------------------------------------------------------- |
| Retrieval (Pre-LLM)  | ~$10    | 17 hours, 20 minutes | Creating the embeddings per CVE for semantic comparison is the longest operation. [OpenAI text-embedding-3-small](https://platform.openai.com/docs/models/text-embedding-3-small) was used ($0.02 per 1M tokens)       |
| CWE Assignment (LLM) | ~$14    | 51 hours, 12 minutes | The LLM review of the input content, and the generation of the report, per CVE, is the longest operation. [Gemini 2.0 Flash](https://ai.google.dev/gemini-api/docs/pricing#gemini-2.0-flash) was used (input: $0.10, output: $0.40 per 1M tokens) |

The process ran 
- unattended (after 5 minute setup time to kickoff the process)
- on a basic computer (with no optimization) calling 3rd party LLMs via API

 
---




## 📊 CWE Mapping Sets

These repositories contain **automatically generated reports** assigning **CWEs** to CVEs in the Top25 subset for each year, where the subset is the CVEs where MITRE deemed the CWE mapping by CNAs should be corrected:
* [Top 25 - 2025 ](https://github.com/CyberSecAI/cwe_agent_assign_reports_2025)
* [Top 25 - 2023](https://github.com/CyberSecAI/cwe_agent_assign_reports_2023)
* [Top 25 - 2022](https://github.com/CyberSecAI/cwe_agent_assign_reports_2022)

The [Observed CVEs (CWE List)](https://github.com/CyberSecAI/cwe_agent_assign_reports_observed)  is the list of CVEs from the CWE List Observed Examples.

---

## 🛠️ Notes

* All reports are in **Markdown** format for easy processing by both humans and LLMs.
* The repo contains **all intermediate processing artifacts** for transparency—though not all are relevant to end users.
