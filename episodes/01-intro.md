---
title: Introductions
teaching: 30
exercises: 0
---

::::::::::::::::::::::::::::::::::::::: objectives

- Understand Funder Requirements: Identify core expectations from major funding bodies regarding research data stewardship.
- Apply the FAIR Principles: Operationalize Findability, Accessibility, Interoperability, and Reusability in daily workflows.
- Draft a Section-by-Section DMP: Create a practical, living DMP for their current or upcoming research projects.
- Budget & Risk Assess Data: Estimate costs associated with data storage, curation, anonymization, and long-term preservation.

::::::::::::::::::::::::::::::::::::::::::::::::::

## Workshop Overview

- Title: Designing Robust Data Management Plans (DMPs) for Research Success
- Target Audience: Early Career Researchers (ECRs), PhD students, and Principal Investigators (PIs) across STEM and HSS disciplines.
- Duration: 3 hours (Half-day interactive workshop)
- Format: Hybrid / In-person hands-on workshop (Includes short lectures, individual exercises, group peer review, and tool demonstrations)
- Key Tools Covered: DMPonline / DMPTool, institutional repositories, license selectors, and FAIR sharing registries.

## Workshop Schedule

schedule_data <- data.frame(
  Time = c("09:00 - 09:20", "09:20 - 10:15", "10:15 - 10:30", "10:30 - 11:15", "11:15 - 11:45", "11:45 - 12:00"),
  Duration = c("20 min", "55 min", "15 min", "45 min", "30 min", "15 min"),
  Session_Topic = c("1. Why DMPs Matter", "2. Walkthrough of DMP Components", "Break", "3. Hands-On Drafting Session", "4. Peer Review & Edge Cases", "5. Tooling, Resources & Q&A"),
  Core_Activities = c(
    "Introduction to research data life cycle, funder compliance, avoiding data loss, and the FAIR Data Principles.",
    "Interactive teardown of the 6 core pillars of a standard DMP template (Data Creation, Documentation, Ethics, Storage, Sharing, Responsibilities).",
    "Refreshments & Networking",
    "Participants use DMPonline / DMPTool or a structured template to draft sections for their own project.",
    "Group evaluation of draft plans using a review checklist. Focus on high-risk areas (sensitive data, large file volumes, proprietary software).",
    "Summary of institutional support, data repositories, DOI assignment, and final Q&A."
  )
)

knitr::kable(
  schedule_data, 
  col.names = c("Time", "Duration", "Session Topic", "Core Activities & Focus"),
  caption = "Half-Day Workshop Schedule"
)


Detailed Session Breakdown
Session 1: Foundation & The FAIR Principles (20 mins)

- Data Lifecycles vs. Project Lifecycles: Moving beyond project end-dates to long-term stewardship.
- FAIR Principles Breakdown:
  - Findable: Persistent Identifiers (DOIs, ORCIDs), rich metadata.
  - Accessible: Standard communications protocols, open vs. restricted access routes.
  - Interoperable: Standard formats, controlled vocabularies, ontologies.
  - Reusable: Clear licensing (e.g., Creative Commons, MIT), provenance documentation.

Session 2: The Core Components of a DMP (55 mins)

1. Data Collection & Types:
  - Distinguishing between raw, processed, and final research outputs.
  - File formats: Choosing non-proprietary formats for long-term sustainability (e.g., .csv over .xlsx, .flac or .wav over .mp3).
  - Volume estimates and storage scaling.
2. Documentation & Metadata:
  - README file structures, codebook design, and data dictionaries.
  - Discipline-specific metadata standards (e.g., Dublin Core, DDI, Schema.org).
3. Ethics, Legal & Intellectual Property:
  - Handling sensitive data: Consent forms for data sharing, anonymization vs. pseudonomization, GDPR/data protection alignment.
  - Copyright, ownership (university vs. funder vs. researcher), and choosing open licenses.
4. Storage, Backup & Security:
  - The 3-2-1 Backup Strategy (3 copies, 2 different media, 1 offsite/cloud).
  - Encryption protocols for sensitive data in transit and at rest.
5. Selection, Preservation & Sharing:
  - Deciding what data to keep vs. what to destroy.
  - Choosing a repository (Generalist vs. Domain-Specific vs. Institutional).
6. Responsibilities & Resources:
  - Roles (who maintains the data during and after the project).
  - Costing data management into grant applications (e.g., repository fees, transcription costs, curation effort).

Session 3: Practical Drafting Exercise (45 mins)

Activity Prompt: Participants log into DMPonline/DMPTool or open the provided Word template and complete three target sections:
- Section A: Data Description & Formats.
- Section B: Ethics, Access Rights, and Anonymization Plan.
- Section C: Storage, Backup, and Long-Term Preservation Strategy.

Exercise Facilitator Tip: Circulate around the room to address specific technical edge cases (e.g., high-performance computing storage limits, commercial restrictions, biological or human subject data constraints).

Session 4: Peer Review Matrix & High-Risk Scenario Analysis (30 mins)

Group Case Study Options (10 mins discussion):
- Scenario A: Managing several terabytes of imaging/sensor outputs on high-performance compute clusters.
- Scenario B: Sharing anonymized interview transcripts with sensitive clinical context.

:::::::::::::::::::::::::::::::::::::::: questions

- "What ML/AI tools are you already aware of in healthcare, and what is your immediate gut reaction to them optimism, skepticism, or anxiety?"
- "Where do you think AI can make the biggest impact in your day-to-day workflow: reducing paperwork or assisting in patient diagnosis?"


::::::::::::::::::::::::::::::::::::::::::::::::::




:::::::::::::::::::::::::::::::::::::::: keypoints

- AI in healthcare isn't a futuristic concept; it is already operating in triaging, billing, and radiology.
- The explosion of healthcare AI is driven by three factors: massive computing power, digitized health records (EHRs), and an explosion of genomic data.
- Effective healthcare AI requires collaboration data scientists understand the math, but clinicians understand the patient.

::::::::::::::::::::::::::::::::::::::::::::::::::


