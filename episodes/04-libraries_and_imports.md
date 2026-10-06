---
title: Limitations & Creating Your Own Model
teaching: 15
exercises: 15
---

::::::::::::::::::::::::::::::::::::::: objectives

- Recognize the ethical and technical boundaries of AI, specifically regarding algorithmic bias and data privacy.
- Deconstruct the high-level, end-to-end pipeline required to build and deploy a compliant medical AI model.
- Shift the mindset from "AI replacing humans" to "AI amplifying human capability."

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- "If an AI model misdiagnoses a patient, who should carry the ultimate responsibility: the doctor who used it, the hospital that bought it, or the data scientist who built it?"
- "What is one manual, repetitive task in your specific domain that you would happily hand over to an AI assistant tomorrow if you knew it was safe?"

::::::::::::::::::::::::::::::::::::::::::::::::::

## Expansion: General Limitations of AI
### Core Concept: Math Patterns vs. Clinical Context

When an AI model generates a medical diagnosis, it is easy to mistakenly assume the machine is "thinking" like a clinician. It isn't. An AI possesses zero common sense and no actual understanding of human physiology.

Consider a chest X-ray model presented with a scan where a patient has accidentally swallowed a coin. The AI has no concept of a stomach, the mechanics of choking, or what a coin even is. Instead, it simply maps mathematical correlations across a grid of pixels, relying entirely on the consistency of statistical patterns.

Because it operates on statistics rather than understanding, it is incredibly fragile. If those data patterns shift even slightly in the real world—or if they were flawed from the very beginning—the model will output a prediction that looks incredibly confident, while being completely wrong.

**This is very similar to what was found during the GEMINI project**

### Correlation $\neq$ Causation

Machines are pattern-matchers, not logicians. If a dataset shows that patients who receive a specific temporary baseline medication happen to survive longer due to independent clinical routing, the model may conclude the medication is a miraculous cure, completely missing the true underlying clinical reason. A way to imagine this is that the machine is in a bubble and only understands what it taught/sees.

### Failure Mode 1: "Garbage In, Garbage Out"

When bad data enters an algorithm, the AI doesn't break down with an error message it builds a highly polished, dangerous model out of that bad data. In short, the model is a summation of everything it has been fed. The problem here is that "bad data", is a very simple term governing alot issues and sometimes its not clear what could be considered it.   

**Common issues with data**

Below are examples of what can be considered "bad" or problematic data:

- **Significant Biases and Underrepresented Minority Groups**: Machine learning models mirror the data they are fed, meaning they inherently absorb any biases present in the dataset. If a specific class or group is underrepresented, the model may fail to predict it entirely, or it might default to predicting only the majority class. Think of a model like a river: if the river forks, the water naturally follows the path of least resistance. Similarly, a model will take the easiest path to minimise error, requiring deliberate intervention and adjustment to ensure it performs fairly and accurately.
- **Poor Quality Images**: While clinical data often avoids this issue due to strict standardisation protocols, it can still occur. If a model is trained on highly blurry images where the target object is barely visible, it will struggle to generalise. You cannot expect a model trained on degraded data to function correctly when tested on clean, high-resolution images.
- **Missing Values**: Missing data poses a significant challenge because the reason for the absence matters. A blank space could represent crucial context (e.g., a intentional omission), or it could simply mean a piece of equipment failed to record the data. Treating these two scenarios the same can lead to severe consequences during training. Furthermore, missing fields are sometimes improperly filled with zeros. Because a value of zero carries its own specific meaning, any data imputation must be handled with the correct context-aware methodology.
- **Incorrect Data**: While similar to missing values, incorrect data presents a distinct hazard—especially when it goes undetected. If a model unknowingly trains on corrupted or inaccurate data, it learns incorrect relationships and patterns, fundamentally undermining its real-world performance.

!["Are we dealing with supervised or unsupervised
learning?"](fig/grabage_in.png){alt="Flow Diagram for determining supervised vs unsupervised"}.

:::::::::::::::::::::::::::::::::::::::: challenge

### Discussion

When an AI model is trained on "garbage data" (like blurry images, missing records, or unfair biases), it doesn't crash or show an error message—it confidently builds a highly polished, dangerous model.

Since real-world medical data is almost always messy and imperfect, how should developers decide when a dataset is "clean enough" to safely train a medical AI, and what rules should be in place to catch these hidden data flaws before they harm a patient?

::::::::::::::::::::::::::::::::::::::::::::::::::

### Failure Mode 2: Model Brittleness & The Generalization Gap

An AI model's performance can drop sharply when moving between hospital environments. This drop is known as Dataset Shift or The Generalisation Gap.

**The Illusion of Performance: "Shortcut Learning"**

When we train a deep learning network on images from a single, high-tech facility, the model often takes an unhelpful shortcut to maximise its accuracy score. It learns to recognise the specific signatures of that hospital's hardware, scan markers, or patient protocols rather than the actual medical pathology.

!["Are we dealing with supervised or unsupervised
learning?"](fig/xray_example.png){alt="Flow Diagram for determining supervised vs unsupervised"}.

### A Real-World Diagnostic Failure Case Study

Consider an AI model built to spot pneumonia on chest X-rays:

- **The Training Site (London Academic Center)**: The model is trained on thousands of scans from top-tier digital imaging suites. In these suites, stable, ambulatory patients stand up for clean, crisp posterior-anterior (PA) views.
- **The Shortcut**: The model notices that the highest-quality scans almost always belong to stable patients, while low-quality, high-noise scans taken by portable bedside units belong to critically ill patients in the ICU. The model covertly learns to classify "portable machine noise" as an indicator of severe lung disease.
- **The Deployment Site (Rural Clinic)**: The model is deployed to a community clinic that relies entirely on an older, portable X-ray unit for all patients due to space constraints.
- **The Crash**: Because every single image coming out of the rural clinic contains high noise and lower contrast, the model's performance breaks down completely. It continuously flags healthy patients as having severe pneumonia simply because it confuses the older machine's background noise with the markers of a critical ICU case.

:::::::::::::::::::::::::::::::::::::::: challenge

### Discussion

A medical AI trained at a high-tech hospital might cheat by learning to recognise the crisp quality of the expensive scanning machines rather than the actual disease—causing it to completely fail when sent to a rural clinic with older equipment.

How can we prevent AI from taking these lazy "shortcuts" during training, and what steps should a small clinic take to test a new AI tool before trusting it with real patients?

::::::::::::::::::::::::::::::::::::::::::::::::::

### Core Concept: The High Stakes of Clinical Software

If a music streaming app has a software bug, you get a bad song recommendation. If a commercial text predictor glitched, it typoed a text message. But in healthcare, a software bug or a hidden algorithmic flaw is a direct threat to patient safety.
When we integrate machine learning into patient care, we cannot manage it like standard consumer tech. We have to wrestle with deep historical biases, navigate complex legal accountability frameworks, and protect patient privacy under the strictest data laws on earth.

## Challenge A: The Dataset Bias Trap

In clinical practice, a physician’s diagnosis is shaped by diverse clinical presentations observed across varied patient populations. AI models, conversely, learn exclusively from the historical data on which they are trained. When these datasets reflect historical disparities, demographic imbalances, or localised practice patterns, the model internalises these systemic flaws—a vulnerability known as the “Dataset Bias Trap.”

In healthcare delivery, a biased algorithm—regardless of its high performance on internal validation sets—threatens health equity, worsens health disparities for underrepresented groups, and creates hidden failure modes when deployed in new clinical settings.

### The Anatomy of Data Imbalance & Historical Bias

Machine learning models optimise purely for aggregate performance metrics. Consequently, they tend to prioritise accuracy on the dominant demographic groups represented in the training data at the expense of minority populations.

Consider a deep learning model developed to screen for cutaneous melanoma using dermatological images:

- **The Demographic Imbalance**: Training datasets sourced primarily from academic medical centers in Northern Europe or North America predominantly feature Fitzpatrick Skin Types I and II (fair skin). Images representing Fitzpatrick Skin Types V and VI (darker skin tones) often comprise less than 5% of the total dataset.
- **The Clinical Consequence**: Because the algorithm has limited exposure to lesions on darker skin—where melanoma often presents differently (e.g., acral lentiginous melanoma on palms, soles, or nail beds)—it demonstrates significantly lower sensitivity for patients of colour. When deployed in diverse clinical environments, the AI routinely generates false negatives on underrepresented patient groups, leading to delayed diagnoses and adverse outcomes.

### Failure Modes: Distribution Shift & Contextual Bias

Beyond demographic representation, dataset bias manifests in operational and technical dimensions that compromise clinical generalisability:

**Out-of-Distribution (OOD) Shift & Site-Specific Drift**

An AI model trained on high-resolution imaging from a tertiary care center’s modern scanner may fail when deployed at a community clinic utilising older equipment or different acquisition protocols.

- **Example**: Variations in slice thickness on CT scans, staining protocols in histopathology slides, or digital radiography exposure parameters can trigger catastrophic drops in diagnostic performance because the model misinterprets site-specific technical signatures as diagnostic features.

**Historical & Health Systems Bias**

Algorithms trained on electronic health record (EHR) data inherit the societal biases and structural inequalities embedded in clinical workflows.

- **Example**: Algorithms designed to predict disease risk or manage high-risk care pathways frequently rely on historical healthcare spending or utilisation rates as proxies for health need. Because socioeconomically disadvantaged populations historically face systemic barriers to accessing care, their lower healthcare expenditures are misinterpreted by the model as lower health risk. As a result, the AI systematically under-allocates specialised care resources to those who need them most.

### Mitigating Dataset Bias: Clinical & Technical Guardrails

To prevent dataset bias from entering clinical workflows, healthcare organisations and developers employ multi-layered auditing and mitigation strategies:

- **Disaggregated Performance Auditing**: Models must be evaluated using stratified performance metrics (e.g., reporting sensitivity, specificity, and positive predictive value separately across age, sex, race, ethnicity, and socioeconomic brackets) rather than relying solely on overall accuracy or Area Under the Curve (AUC).
- **Dataset Nutrition Labels & Datasheets**: Implementing standardised documentation—such as Datasheets for Datasets—that explicitly logs demographic distributions, inclusion/exclusion criteria, data collection sites, and known limitations before model training.
- **Domain Adaptation & Federated Learning**: Utilising domain adaptation techniques to adjust models to local clinical environments and leveraging federated learning to train algorithms across geographically diverse healthcare systems without centralising sensitive patient data.

!["Are we dealing with supervised or unsupervised
learning?"](fig/skin_cancer.png){alt="Flow Diagram for determining supervised vs unsupervised"}.

## Challenge B: The Black Box & Explainability (XAI)

When a doctor prescribes a medication or orders a surgical intervention, they can articulate their clinical reasoning. They evaluate symptoms, lab values, and underlying physiological mechanisms. Deep learning models, however, operate on thousands of abstract statistical features across millions of parameters. They deliver high-accuracy outputs without revealing how they arrived at a conclusion—a problem commonly known as the "Black Box."

In clinical care, an unexplainable prediction—no matter how statistically accurate on paper—creates critical safety hazards, obscures algorithmic failure modes, and makes true informed consent nearly impossible.
The Shortcuts of Deep Learning

Deep neural networks excel at optimising for a target objective, but they do not understand clinical causality. Without explainability tools, a model can achieve near-perfect diagnostic metrics by exploiting unintended artifacts, background noise, or metadata in the image rather than learning genuine pathology.

### Spurious Correlations in Radiological Imaging

Consider a convolutional neural network trained to detect pneumothorax (collapsed lung) on chest X-rays:

- **The Artifact Trap**: Patients with acute pneumothorax in hospitals frequently receive immediate treatment via a chest tube insertion. In training datasets, chest X-rays of patients with pneumothorax often contain visible chest drain tubes or specific alignment markers used in emergency triage rooms.
- **The Clinical Consequence**: Rather than learning the subtle visceral pleural edge or lung tissue density changes, the model learns to identify the plastic tube or triage tag. When evaluated on standard test metrics, its performance appears exceptional. However, when deployed on a early-stage patient without a chest tube, the model fails to detect the condition—mistaking a treatment marker for the disease itself.

### Saliency Maps & Explainable AI (XAI) Methods

To open the black box, researchers and clinicians utilise Explainable AI (XAI) techniques, such as Grad-CAM (Gradient-weighted Class Activation Mapping), Integrated Gradients, and SHAP (SHapley Additive exPlanations). These frameworks highlight which regions of an input image or feature vector contributed most heavily to the model's output.

While XAI helps catch spurious correlations, it introduces its own set of clinical challenges:

- **Visual Reassurance vs. Ground Truth**: Heatmaps show where the model was "looking," but they do not prove logical reasoning. A saliency map highlighting a lung region does not guarantee the model evaluated the correct tissue structure.
- **Automation Bias**: If a highlighted region vaguely overlaps with an abnormality, clinicians may prematurely trust a flawed AI output, overriding their own clinical judgment.

!["Are we dealing with supervised or unsupervised
learning?"](fig/explainability.jpeg){alt="Flow Diagram for determining supvervised vs unsupervised"}.

## Challenge C: Data Privacy & Sovereign Borders

Tech giants scale their businesses by collecting massive consumer data pools into centralized clouds. In medicine, strict privacy frameworks like HIPAA (Health Insurance Portability and Accountability Act) and GDPR (General Data Protection Regulation) make this central gathering approach an operational and legal impossibility.

!["Are we dealing with supervised or unsupervised
learning?"](fig/data_privacy.png){alt="Flow Diagram for determining supvervised vs unsupervised"}.

### The Solution: Federated Learning**

To train powerful models without moving highly confidential patient files across institutional boundaries, medical networks utilise Federated Learning architectures.

!["Are we dealing with supervised or unsupervised
learning?"](fig/federated_learning.png){alt="Flow Diagram for determining supervised vs unsupervised"}.

Rather than forcing healthcare networks to pool private patient data into a vulnerable central repository, federated learning flips the pipeline completely:

- **Local Preservation**: The raw data stays safely behind local firewall networks at individual facilities (e.g., individual hospitals, research centers, or universities).
- **Model Dissemination**: A blank, unconfigured neural network model is sent out from a central federated server to each individual site.
- **Local On-Site Training**: The model trains locally on each hospital's local data servers. No patient charts, names, or identifiers ever leave the building.
- **Global Aggregation**: The sites send only their mathematical model adjustments (weight updates) back to the central server. The central server blends these updates into a master algorithm that benefits from the collective knowledge of multiple hospitals while maintaining absolute data confidentiality.

## Challenge D: Hallucinations & Fabricated Evidence

Large Language Models operate on probabilistic next-token prediction, meaning they determine the most statistically likely next word rather than querying a factual database. In high-stakes fields like medicine, law, or engineering, this architecture leads to "hallucinations"—convincing, authoritative-sounding outputs that are entirely fabricated or factually incorrect.

### The Solution: Retrieval-Augmented Generation (RAG)

To prevent models from relying solely on their static, imperfect internal memory, systems utilise Retrieval-Augmented Generation (RAG) architectures.

Rather than forcing the LLM to generate responses entirely from its original training weights, a RAG pipeline anchors the model's generation to trusted, verifiable data sources:

- **External Knowledge Retrieval**: When a user submits a query, the system first searches a curated, authoritative database (e.g., peer-reviewed medical journals, internal legal code, or technical manuals) for relevant documents.
- **Context Embedding**: The system extracts the most accurate document snippets and injects them directly into the LLM's prompt window alongside the original user question.
- **Grounded Generation**: The LLM reads the provided reference materials and uses them as an open-book source to draft its answer. It is explicitly instructed to only use the provided text.
- **Source Citation**: The final output is generated with direct citations linking back to the source documents, allowing human experts to cross-reference and verify the model's claims instantly.

!["Are we dealing with supervised or unsupervised
learning?"](fig/Hallucinations_Fabricated_Evidence.jpeg){alt="Flow Diagram for determining supervised vs unsupervised"}.
    
## Summary Wrap-Up for the Session
Key Takeaway: Ethical healthcare AI requires moving past the simple metric of "accuracy." We must actively inspect our datasets for demographic gaps, use XAI tools like SHAP force plots to keep clinical logic transparent, and utilise decentralised frameworks like federated learning to respect sovereign data walls.

## How to Build a Model: The Bare Minimum

**Core Concept**

"If you ever want to launch an AI research project or build a tool for your department, you need to understand that coding is only about 10% of the timeline. The real work is data governance, labelling, and workflow integration. Let's walk through the actual clinical blueprint."

### The Multi-Phase Clinical AI Pipeline

!["Are we dealing with supervised or unsupervised
learning?"](fig/multi-phase.png){alt="Flow Diagram for determining supervised vs unsupervised"}.

### Frameworks & Data Scaling

Transitioning machine learning from theory to implementation requires selecting an optimal framework and engineering structured data pipelines. For deep learning, PyTorch provides an intuitive, dynamic computation graph for debugging complex networks inline, while TensorFlow/Keras optimizes production deployments. For tabular data, Scikit-learn manages classical algorithms, while XGBoost and LightGBM typically yield superior predictive accuracy. For genomic sequences or text, Hugging Face standardises pre-trained transformer blocks.

Raw features must be mathematically transformed into optimised tensors to ensure gradient stability and network convergence:

- **Standardisation**: Translates data to a mean of 0 and a standard deviation of 1, preserving outlier relative positioning.
- **Min-Max Scaling**: Compresses arrays into a rigid $[0, 1]$ boundary, which is essential for uniform structures like image pixel matrices.
- **Embedding Layers**: Replace memory-intensive one-hot encoding by mapping high-cardinality discrete categories into dense, low-dimensional continuous vector spaces.

### Execution Pipelines & Infrastructure

To maximize hardware throughput and eliminate data starvation—where an accelerator sits idle waiting for disk reads—workflows decouple data retrieval from model execution. Custom data loaders use background CPU cores to batch, shuffle, and apply data augmentations asynchronously in parallel with the GPU's forward-backward passes.

As models and data scale beyond interactive notebook capacity, workflows are modularized into non-interactive scripts for High-Performance Computing (HPC) clusters managed by orchestrators like SLURM. Developers submit batch scripts requesting specific hardware isolation.

## Wrap-Up & Next Steps (10 Mins)

**Final Closing Thoughts**

"As we close out this foundational series, remember this fundamental truth: The goal of AI in healthcare is not to replace the clinician.
The true promise of these tools is to automate the repetitive, administrative, and exhausting tasks—the endless documentation, the initial sorting of normal scans, the manual data tracking. By offloading that cognitive load to machines, we can give human clinicians their most valuable asset back: time. Time to focus on complex cases, and time to spend at the bedside doing what humans do best—caring for patients."


:::::::::::::::::::::::::::::::::::::::: keypoints

- The Bias Trap: Models trained on narrow demographics (e.g., primarily Caucasian skin types for dermatology AI) drop significantly in accuracy when applied to diverse populations.
- Brittleness & Drift: A model optimized for a high-tech metropolitan hospital will often fail in a rural clinic due to differences in equipment, patient demographics, and charting habits ("Garbage In, Garbage Out").
- The Model Lifecycle: Building a model is only 20% math. The other 80% is data governance (HIPAA/GDPR compliance), establishing an expert "ground truth" through manual labeling, and workflow integration.

::::::::::::::::::::::::::::::::::::::::::::::::::


