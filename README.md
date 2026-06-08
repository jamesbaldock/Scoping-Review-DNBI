```markdown
# JLLS-Medical-Scoping-Review: Algorithmic Screening Pipeline for Military Grey Literature

This repository contains the programmatic screening pipeline used to isolate, standardize, and evaluate raw institutional records from the Joint Lessons Learned System (JLLS) for an academic scoping review. 

The pipeline strictly adheres to the **PRISMA-ScR (Preferred Reporting Items for Systematic Reviews and Meta-Analyses extension for Scoping Reviews)** guidelines, translating qualitative Population-Concept-Context (PCC) eligibility criteria into a reproducible, automated text-mining workflow.

---

## 📋 Project Overview

Traditional scoping reviews encounter immense publication bias when evaluating military and operational medicine due to the exclusion of grey literature. The Joint Lessons Learned Information System (JLLS) provides primary-source data, but database extracts are dense, heterogeneous, and lack a unified narrative field. 

This repository provides a two-phase Python screening framework designed to:
1. **Filter and Standardize:** Isolate health-related literature from a multi-domain database extract and computationally consolidate disparate text architectures into a single narrative column.
2. **Execute Algorithmic PCC Screening:** Categorize records using automated rule-based criteria targeting **Disease and Non-Battle Injuries (DNBI)** within the **Ukrainian Military** during the **Russo-Ukrainian Conflict (2020–Present)**.

---

## 🔍 Eligibility Criteria (PCC Framework)

The underlying rule-based algorithms are mapped directly from the review's core eligibility matrix:

| Criterion | Inclusion Criteria | Exclusion Criteria |
| :--- | :--- | :--- |
| **Population** | Ukrainian military service members (Active-duty, deployed, reserve component) | U.S. military service members, U.S. veterans, DoD civilians or contractors, Ukrainian civilians |
| **Concept** | Disease and Non-Battle Injuries (DNBI), public health, infection, hygiene, preventable illness | Traumatic combat injuries (e.g., blast, shrapnel, gunshot wounds), animal studies, biosurveillance/bioterrorism |
| **Context** | Russo-Ukrainian conflict occurring during or after 2020 | Prior or separate conflicts (e.g., Operation Enduring Freedom, Iron Swords, GWOT) |
| **Evidence Type** | Primary empirical data, technical reports, case studies, After Action Reports (AAR)*, Observation notes* | Protocols, literature reviews (systematic/narrative), editorial or news articles, dissertations, pre-2020 data |

*\*Note: Specific to JLLS module extractions.*

---

## ⚙️ Data Pipeline Architecture
[Raw Extract: 1,000 Rows] (export_01_Jun_2026_14-13-34.xlsx)
│
▼
┌─────────────────────────────────┐
│     Phase 1: Keyword Mining     │ ──► Discards 810 Non-Medical Records
└─────────────────────────────────┘
│
▼
[Medical Pool: 190 Rows] (Medical_Scoping_Review_Screening.xlsx)
│
▼
┌─────────────────────────────────┐
│     Phase 2: Automated PCC      │ ──► Discards 175 Out-of-Scope Rows
└─────────────────────────────────┘
│
├────────────────────────┐
▼                        ▼
[Potential Includes: 10 Rows]   [Manual Pending: 5 Rows]
│                        │
└───────────┬────────────┘
▼
┌─────────────────────────────────┐
│  Phase 3: Human-in-the-Loop     │ ──► Dual-Investigator Adjudication
└─────────────────────────────────┘
│
▼
[Final Systematic Corpus]

### File Tracking & Data Lifecycle
1. **`export_01_Jun_2026_14-13-34.xlsx`**: The raw, unedited source extraction spanning 7 database components (AAR, BIN, COL, COP, OBS, PVR, RES).
2. **`Medical_Scoping_Review_Screening.xlsx`**: The intermediate 190-row pool. Narrative descriptions (e.g., "Executive Summaries" from AAR sheets and "Observation/Discussion" blocks from OBS sheets) are computationally consolidated into a standardized `Main_Text` column.
3. **`Medical_Scoping_Review_PCC_Screened.xlsx`**: The fully audited database workbook featuring PRISMA-ScR tracking metadata: `Screening_Decision` (*INCLUDE / EXCLUDE / PENDING*), `Exclusion_Reason`, and `Reviewer_Notes` written programmatically.

---

## 🚀 How to Run the Scripts

You can run this pipeline locally or directly within **Google Colab**.

### Prerequisites
Ensure you have Python 3.x installed along with the required data-science libraries:
```bash
pip install pandas openpyxl

Steps for Google Colab Execution
Upload your raw export_01_Jun_2026_14-13-34.xlsx file using the folder icon in Colab's left sidebar.

Run the Phase 1 script to filter medical terms and build the consolidated narrative sheet.

Execute the Phase 2 script to apply the strict PCC rule matrix.

Refresh your sidebar and download Medical_Scoping_Review_PCC_Screened.xlsx to manually adjudicate rows marked PENDING (flagged due to mixed population contexts, such as U.S. advisors tracking Ukrainian casualties).

### 🛠️ How to Add This to Your GitHub Repository
1. On your local machine, download the generated `README.md` file from the link above.
2. If you are uploading via the GitHub web interface: open your repository page, click **Add file > Upload files**, drag and drop this `README.md` file, and commit changes.
3. If you prefer to make it directly on GitHub without downloading: click **Add file > Create new fi
