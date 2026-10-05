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

- Significant Biases and Underrepresented Minority Groups: Machine learning models mirror the data they are fed, meaning they inherently absorb any biases present in the dataset. If a specific class or group is underrepresented, the model may fail to predict it entirely, or it might default to predicting only the majority class. Think of a model like a river: if the river forks, the water naturally follows the path of least resistance. Similarly, a model will take the easiest path to minimize error, requiring deliberate intervention and adjustment to ensure it performs fairly and accurately.
- Poor Quality Images: While clinical data often avoids this issue due to strict standardization protocols, it can still occur. If a model is trained on highly blurry images where the target object is barely visible, it will struggle to generalize. You cannot expect a model trained on degraded data to function correctly when tested on clean, high-resolution images.
- Missing Values: Missing data poses a significant challenge because the reason for the absence matters. A blank space could represent crucial context (e.g., a intentional omission), or it could simply mean a piece of equipment failed to record the data. Treating these two scenarios the same can lead to severe consequences during training. Furthermore, missing fields are sometimes improperly filled with zeros. Because a value of zero carries its own specific meaning, any data imputation must be handled with the correct context-aware methodology.
- Incorrect Data: While similar to missing values, incorrect data presents a distinct hazard—especially when it goes undetected. If a model unknowingly trains on corrupted or inaccurate data, it learns incorrect relationships and patterns, fundamentally undermining its real-world performance.

!["Are we dealing with supervised or unsupervised
learning?"](fig/grabage_in.png){alt="Flow Diagram for determining supvervised vs unsupervised"}.

:::::::::::::::::::::::::::::::::::::::: challenge

### Discussion

When an AI model is trained on "garbage data" (like blurry images, missing records, or unfair biases), it doesn't crash or show an error message—it confidently builds a highly polished, dangerous model.

Since real-world medical data is almost always messy and imperfect, how should developers decide when a dataset is "clean enough" to safely train a medical AI, and what rules should be in place to catch these hidden data flaws before they harm a patient?

::::::::::::::::::::::::::::::::::::::::::::::::::

### Failure Mode 2: Model Brittleness & The Generalization Gap

An AI model's performance can drop sharply when moving between hospital environments. This drop is known as Dataset Shift or The Generalization Gap.

**The Illusion of Performance: "Shortcut Learning"**

When we train a deep learning network on images from a single, high-tech facility, the model often takes an unhelpful shortcut to maximize its accuracy score. It learns to recognize the specific signatures of that hospital's hardware, scan markers, or patient protocols rather than the actual medical pathology.

!["Are we dealing with supervised or unsupervised
learning?"](fig/xray_example.png){alt="Flow Diagram for determining supvervised vs unsupervised"}.

**A Real-World Diagnostic Failure Case Study**

Consider an AI model built to spot pneumonia on chest X-rays:

- The Training Site (London Academic Center): The model is trained on thousands of scans from top-tier digital imaging suites. In these suites, stable, ambulatory patients stand up for clean, crisp posterior-anterior (PA) views.
- The Shortcut: The model notices that the highest-quality scans almost always belong to stable patients, while low-quality, high-noise scans taken by portable bedside units belong to critically ill patients in the ICU. The model covertly learns to classify "portable machine noise" as an indicator of severe lung disease.
- The Deployment Site (Rural Clinic): The model is deployed to a community clinic that relies entirely on an older, portable X-ray unit for all patients due to space constraints.
- The Crash: Because every single image coming out of the rural clinic contains high noise and lower contrast, the model's performance breaks down completely. It continuously flags healthy patients as having severe pneumonia simply because it confuses the older machine's background noise with the markers of a critical ICU case.

:::::::::::::::::::::::::::::::::::::::: challenge

### Discussion

A medical AI trained at a high-tech hospital might cheat by learning to recognize the crisp quality of the expensive scanning machines rather than the actual disease—causing it to completely fail when sent to a rural clinic with older equipment.

How can we prevent AI from taking these lazy "shortcuts" during training, and what steps should a small clinic take to test a new AI tool before trusting it with real patients?

::::::::::::::::::::::::::::::::::::::::::::::::::

### Core Concept: The High Stakes of Clinical Software

If a music streaming app has a software bug, you get a bad song recommendation. If a commercial text predictor glitched, it typoed a text message. But in healthcare, a software bug or a hidden algorithmic flaw is a direct threat to patient safety.
When we integrate machine learning into patient care, we cannot manage it like standard consumer tech. We have to wrestle with deep historical biases, navigate complex legal accountability frameworks, and protect patient privacy under the strictest data laws on earth.

## Challenge A: The Dataset Bias Trap

Algorithms do not have moral compasses; they are historical mirrors. If the data used to train an AI model reflects societal or systemic gaps in healthcare access, the model will codify and supercharge those disparities under the guise of objective mathematics.

**The Fitzpatrick Scale Disparity in Dermatology**

In medical computer vision, skin cancer screening tools rely heavily on image pattern recognition. A historical problem is that major open-source dermatology training repositories (like the ISIC archive) have historically consisted of images taken from individuals with lighter skin tones.

- The Systemic Drop: When an algorithm trained primarily on Fitzpatrick Types 1–3 (lighter skin) is asked to evaluate a lesion on Fitzpatrick Types 5–6 (darker skin), its diagnostic accuracy drops precipitously.
- The Clinical Consequence: The model fails to recognize the edge boundaries, color variations, or texture changes of a malignant melanoma against a darker background melanin index. This leads directly to higher false-negative rates and delayed, late-stage cancer diagnoses for minority patient groups.

!["Are we dealing with supervised or unsupervised
learning?"](fig/skin_cancer.png){alt="Flow Diagram for determining supvervised vs unsupervised"}.

## Challenge B: The Black Box & Explainability (XAI)

Deep learning models operate by routing inputs through millions of abstract mathematical connections. This yields a Black Box problem: an input goes in, an output comes out, but the exact clinical logic remains completely invisible.

**Moving Past the Black Box with SHAP & LIME**

Physicians have an ethical and legal duty of care. You cannot prescribe a aggressive treatment protocol or send a patient to emergency surgery simply because a model generated a high risk score. You need to know why.
Medicine solves this using Explainable AI (XAI) frameworks. The two industry standards are:

- SHAP (SHapley Additive exPlanations): Uses cooperative game theory to calculate the exact structural contribution of each medical feature to the final prediction.
- LIME (Local Interpretable Model-agnostic Explanations): Purposely perturbs the data around a single patient to see which variables cause the prediction to flip.

**Reading a SHAP Force Plot**

When integrated into an Electronic Health Record (EHR), an XAI tool transforms a blind risk percentage into an actionable diagnostic map.

!["Are we dealing with supervised or unsupervised
learning?"](fig/EHR_example.png){alt="Flow Diagram for determining supvervised vs unsupervised"}.

As shown in the force plot visualization above, the model reveals its internal decision-making path for individual patients:

- The Baseline Value: The system starts at a standard population risk baseline.
- The Dynamic Vectors: Clinical variables act as directional forces. Red bars push the patient's score higher toward a critical alert threshold, while blue bars pull the prediction down toward safety.
- Clinical Verification: A clinician can quickly review the chart and see that a high risk score was driven specifically by a high respiratory rate (RR = 23.0) paired with a compromised oxygenation status (PaO2 = 53.0), allowing them to clinically validate the AI's warning.

## Challenge C: Data Privacy & Sovereign Borders

Tech giants scale their businesses by collecting massive consumer data pools into centralized clouds. In medicine, strict privacy frameworks like HIPAA (Health Insurance Portability and Accountability Act) and GDPR (General Data Protection Regulation) make this central gathering approach an operational and legal impossibility.

!["Are we dealing with supervised or unsupervised
learning?"](fig/data_privacy.png){alt="Flow Diagram for determining supvervised vs unsupervised"}.

**The Solution: Federated Learning**

To train powerful models without moving highly confidential patient files across institutional boundaries, medical networks utilize Federated Learning architectures.

!["Are we dealing with supervised or unsupervised
learning?"](fig/federated_learning.png){alt="Flow Diagram for determining supvervised vs unsupervised"}.

Rather than forcing healthcare networks to pool private patient data into a vulnerable central repository, federated learning flips the pipeline completely:

- Local Preservation: The raw data stays safely behind local firewall networks at individual facilities (e.g., individual hospitals, research centers, or universities).
- Model Dissemination: A blank, unconfigured neural network model is sent out from a central federated server to each individual site.
- Local On-Site Training: The model trains locally on each hospital's local data servers. No patient charts, names, or identifiers ever leave the building.
- Global Aggregation: The sites send only their mathematical model adjustments (weight updates) back to the central server. The central server blends these updates into a master algorithm that benefits from the collective knowledge of multiple hospitals while maintaining absolute data confidentiality.

## Challenge D: Hallucinations & Fabricated Evidence

Large Language Models operate on probabilistic next-token prediction, meaning they determine the most statistically likely next word rather than querying a factual database. In high-stakes fields like medicine, law, or engineering, this architecture leads to "hallucinations"—convincing, authoritative-sounding outputs that are entirely fabricated or factually incorrect.

### The Solution: Retrieval-Augmented Generation (RAG)

To prevent models from relying solely on their static, imperfect internal memory, systems utilize Retrieval-Augmented Generation (RAG) architectures.

Rather than forcing the LLM to generate responses entirely from its original training weights, a RAG pipeline anchors the model's generation to trusted, verifiable data sources:

- External Knowledge Retrieval: When a user submits a query, the system first searches a curated, authoritative database (e.g., peer-reviewed medical journals, internal legal code, or technical manuals) for relevant documents.
- Context Embedding: The system extracts the most accurate document snippets and injects them directly into the LLM's prompt window alongside the original user question.
- Grounded Generation: The LLM reads the provided reference materials and uses them as an open-book source to draft its answer. It is explicitly instructed to only use the provided text.
- Source Citation: The final output is generated with direct citations linking back to the source documents, allowing human experts to cross-reference and verify the model's claims instantly.

!["Are we dealing with supervised or unsupervised
learning?"](fig/Hallucinations_Fabricated_Evidence.jpeg){alt="Flow Diagram for determining supvervised vs unsupervised"}.
    
## Summary Wrap-Up for the Session
Key Takeaway: Ethical healthcare AI requires moving past the simple metric of "accuracy." We must actively inspect our datasets for demographic gaps, use XAI tools like SHAP force plots to keep clinical logic transparent, and utilize decentralized frameworks like federated learning to respect sovereign data walls.

## How to Build a Model: The Bare Minimum

**Core Concept**

"If you ever want to launch an AI research project or build a tool for your department, you need to understand that coding is only about 10% of the timeline. The real work is data governance, labeling, and workflow integration. Let's walk through the actual clinical blueprint."

### The Multi-Phase Clinical AI Pipeline

!["Are we dealing with supervised or unsupervised
learning?"](fig/multi-phase.png){alt="Flow Diagram for determining supvervised vs unsupervised"}.

### Frameworks & Data Scaling

Transitioning machine learning from theory to implementation requires selecting an optimal framework and engineering structured data pipelines. For deep learning, PyTorch provides an intuitive, dynamic computation graph for debugging complex networks inline, while TensorFlow/Keras optimizes production deployments. For tabular data, Scikit-learn manages classical algorithms, while XGBoost and LightGBM typically yield superior predictive accuracy. For genomic sequences or text, Hugging Face standardizes pre-trained transformer blocks.

Raw features must be mathematically transformed into optimized tensors to ensure gradient stability and network convergence:

- Standardization: Translates data to a mean of 0 and a standard deviation of 1, preserving outlier relative positioning.
- Min-Max Scaling: Compresses arrays into a rigid $[0, 1]$ boundary, which is essential for uniform structures like image pixel matrices.
- Embedding Layers: Replace memory-intensive one-hot encoding by mapping high-cardinality discrete categories into dense, low-dimensional continuous vector spaces.

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


