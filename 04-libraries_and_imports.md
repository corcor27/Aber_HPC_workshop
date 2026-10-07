--
title: Practical Drafting Session
teaching: 45
exercises: 15
---

::::::::::::::::::::::::::::::::::::::: objectives

- Draft Core DMP Sections: Write concrete, funder-compliant responses for Data Collection, Ethics/Storage, and Long-Term Sharing.
- Formulate Format Conversion Rules: Identify proprietary file formats used in their current pipeline and define clear export pathways to open standards.
- Construct a Standardised README.txt: Build a project root folder documentation asset following metadata standards.



::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- Format Conversion Overhead: "How much automated scripting (e.g., Python, R, Bash) can you write into your analysis pipeline to automatically convert working files to open standards upon completion?"
- Cloud vs. On-Premises Backups: "Does your current backup setup fulfill all three components of the 3-2-1 strategy, or are you relying entirely on a single synchronized cloud folder?"
- Documentation Debt: "How long would it take to draft a complete README.txt for your current active project if you started right now?"

::::::::::::::::::::::::::::::::::::::::::::::::::


## Hands-On Drafting Exercises

Participants will open their preferred tool (DMPonline, DMPTool, or a local Word/Markdown template) and complete three focused drafting blocks.


### Exercise 1: Data Types, Formats & Volume (15 mins)

Prompt: Define the operational outputs of your current or upcoming project using the structured breakdown below.

!["Are we dealing with supervised or unsupervised
learning?"](fig/pillar_22.1.png){alt="Flow Diagram for determining supvervised vs unsupervised"}.

### Exercise 2: Ethics, Security & Backup (15 mins)

Prompt: Document your data protection measures, consent boundaries, and backup pipeline using the 3-2-1 strategy framework.

!["Are we dealing with supervised or unsupervised
learning?"](fig/pillar_22.1.png){alt="Flow Diagram for determining supvervised vs unsupervised"}.

### Exercise 3: Documentation Asset – Root README.txt (15 mins)

Prompt: Create a standardized, bare-bones README.txt template to accompany your dataset upon repository deposit.

========================================================================
DATASET README FILE
========================================================================

1. GENERAL INFORMATION
   - Title of Dataset: [ Insert Project Title ]
   - Principal Investigator / Author: [ Name, ORCID iD, Email ]
   - Date of Data Collection: [ YYYY-MM-DD to YYYY-MM-DD ]
   - Geographic Location / Context: [ Institution / Field Location ]
   - Funding Source / Grant Number: [ Funder Name, Grant ID ]

2. FILE & DIRECTORY STRUCTURE
   - /raw_data/          : Unprocessed files direct from acquisition equipment.
   - /processed_data/    : Anonymized, cleaned, and feature-engineered outputs (.csv).
   - /scripts/           : Code pipelines for processing and statistical evaluation.
   - /docs/              : Data dictionary, codebook, and metadata definitions.

3. DATA DICTIONARY & VARIABLES
   - Column A: sample_id   [ Unique participant identifier; string ]
   - Column B: scan_date   [ Date of scan acquisition; ISO 8601 YYYY-MM-DD ]
   - Column C: volume_mm3  [ Calculated lesion volume; numeric, float ]
   - Missing Values Code  : NA or -9999

4. LICENSING & ACCESS
   - Usage License       : Creative Commons Attribution 4.0 International (CC-BY 4.0)
   - Persistent Identifier: DOI: 10.xxxx/zenodo.xxxxxxx
========================================================================


:::::::::::::::::::::::::::::::::::::::: keypoints

- Draft as You Work: Never wait until the final month of a grant to write your DMP documentation assets.
- Automate Format Exports: Integrate export rules (.csv, .pdf, .tif) directly into your computing pipelines.
- Lock Down Identifiers: Pseudonymize early and verify that linkage keys are stored separately from raw analytical files.
- Standardize Metadata From Day 1: Using ISO standards (e.g., ISO 8601 for dates: YYYY-MM-DD) and clear missing value indicators (NA) prevents downstream analysis bugs.
::::::::::::::::::::::::::::::::::::::::::::::::::
