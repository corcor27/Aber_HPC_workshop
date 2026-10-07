---
title: Walkthrough of DMP Components
teaching: 45
exercises: 15
---

::::::::::::::::::::::::::::::::::::::: objectives

- Identify the 6 Core Pillars of standard funding agency DMP templates.
- Select Preservation Formats: Distinguish between proprietary working formats and open-standard preservation formats.
- Design Metadata & Documentation Assets: Structure a standardized README.txt file and data dictionary.
- Formulate Ethical & Security Protocols: Establish appropriate anonymization, encryption, and access control measures for sensitive data.
- Implement the 3-2-1 Backup Strategy: Build a resilient storage and backup pipeline.
- Assign Data Stewardship Roles: Define explicit data management responsibilities and budget for curation costs in grant proposals.


::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- Formats & Workflows: "What software tools in your lab create locked or proprietary binary formats? Is there an automated pipeline or export script you could use to save open-standard copies?"
- Ethical Sharing: "If your study involves sensitive human participant data, how can you write your Participant Information Sheets (PIS) so that consent explicitly allows sharing anonymized data long-term?"
- Costing & Budgeting: "Have you ever included data management hardware, cloud storage, or curation effort line-items in a grant budget? Why or why not?"

::::::::::::::::::::::::::::::::::::::::::::::::::

Module 2.1: The 6 Pillars of a Data Management Plan

Standard DMP templates from major funding bodies (e.g., UKRI, NIH, Horizon Europe) are structured around six fundamental areas:

!["Are we dealing with supervised or unsupervised
learning?"](fig/pillar_21.png){alt="Flow Diagram for determining supvervised vs unsupervised"}.

Module 2.2: Pillar Breakdown & Best Practices
## Pillar 1: Data Creation, Types & Formats

- What to Address:
  - What types of data will be collected or generated (e.g., observational, experimental, simulation, qualitative)?
  - Estimated total data volume over the project lifecycle (e.g., Gigabytes vs. Terabytes).
  - Working file formats vs. Long-term archiving formats.
- Format Standards Table:

!["Are we dealing with supervised or unsupervised
learning?"](fig/pillar_22.1.png){alt="Flow Diagram for determining supvervised vs unsupervised"}.

## Pillar 2: Documentation, Metadata & Reproducibility
- What to Address:
  - How will someone else (or you in 5 years) know what your variables, column headers, and codes mean?
- Core Documentation Assets:
  - README.txt File: Root-level text document outlining directory structure, software dependencies, citation info, and usage parameters.
  - Data Dictionary / Codebook: Explaining variable names, units of measurement, missing value codes (e.g., -999 vs NA), and data types.
  - Formal Metadata Standards: Discipline-specific schema (e.g., Dublin Core, DDI for social sciences, Darwin Core for biodiversity, Schema.org).

## Pillar 3: Ethics, Legal Compliance & Intellectual Property

- What to Address:
  - Participant consent, GDPR/data protection regulations, confidential or commercially sensitive information.
  - Copyright ownership (University vs. Funder vs. Researcher) and licensing choice.
- Key Protocols:
  - Anonymization vs. Pseudonymization: Pseudonymized data (keys held separately) remains personal data under GDPR; fully anonymized data does not.
  - Licensing Selections:
    - CC-BY 4.0: Open access with attribution (recommended for datasets).
    - CC0 (Public Domain): Maximum reusability without restrictions.
    - MIT / GPL v3: Preferred licenses for code and computational scripts.
    
!["Are we dealing with supervised or unsupervised
learning?"](fig/pillar_22.3.png){alt="Flow Diagram for determining supvervised vs unsupervised"}.

## Pillar 4: Storage, Backup & Security

- What to Address:
  - Where active data resides during the project and how access permissions are managed.
  - Backup schedules, redunancy, and physical/digital security.
- The 3-2-1 Backup Strategy:

!["Are we dealing with supervised or unsupervised
learning?"](fig/pillar_22.4.png){alt="Flow Diagram for determining supvervised vs unsupervised"}.

Security Warning: Avoid syncing unencrypted sensitive participant data to commercial cloud services (e.g., personal Dropbox or Google Drive). Use institutionally managed, encrypted storage solution.

## Pillar 5: Selection, Preservation & Sharing
- What to Address:
  - What data must be kept long-term vs. what can be safely discarded (e.g., raw sensor logs vs. processed features)?
  - Which repository will host the dataset after project completion?
  - How long will the data be retained (funder standard is typically 10+ years)?
- Repository Types:
  - Domain-Specific Repositories (Best practice: e.g., GenBank, UK Data Service, GEO).
  - Institutional Repositories (University-backed repository assigning DOIs).
  - Generalist Repositories (e.g., Zenodo, Figshare, OSF).
  
!["Are we dealing with supervised or unsupervised
learning?"](fig/pillar_22.5.png){alt="Flow Diagram for determining supvervised vs unsupervised"}.

## Pillar 6: Responsibilities & Resourcing

- What to Address:
  - Who is explicitly responsible for each data management task throughout the project lifecycle?
  - What are the financial costs associated with data preparation, curation, and long-term storage?
- Resource Costing Checklist:

!["Are we dealing with supervised or unsupervised
learning?"](fig/pillar_22.6.png){alt="Flow Diagram for determining supvervised vs unsupervised"}.

:::::::::::::::::::::::::::::::::::::::: keypoints

- Standardize Formats Early: Always preserve an open-standard copy (.csv, .pdf, .flac, .tif) alongside your proprietary working files to ensure long-term readability.
- Document for a Stranger: Assume the person re-using your dataset has never spoken to you. Provide self-contained README files and data dictionaries.
- Protect Sensitive Data at the Consent Stage: Ethical data sharing begins with how informed consent forms are written. Include explicit wording permitting secondary research on anonymized outputs.
- Enforce 3-2-1 Backups: Never rely on a single laptop, USB drive, or unmanaged personal cloud folder for active research data.
- Assign Named Roles: Clearly assign named individuals (e.g., lead post-doc, lab manager, PI) to specific data tasks so accountability doesn't fall through the cracks.
::::::::::::::::::::::::::::::::::::::::::::::::::


