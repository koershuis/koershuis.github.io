---
layout: post
title: "LabCAS: When NASA Meets Cancer Research in the Cloud"
subtitle: "How space science infrastructure is powering biomarker discovery"
date: 2026-05-04
tags: [cloud computing, biomedicine, cancer research, data science, artificial intelligence]
---

# LabCAS: When NASA Meets Cancer Research in the Cloud

## How space science infrastructure is powering biomarker discovery

Posted on May 4, 2026

**Article explored:** Crichton DJ, Cinquini L, Kincaid H, et al. *From space to biomedicine: Enabling biomarker data science in the cloud.* Cancer Biomarkers. 2022;33(4):479–488. doi:10.3233/CBM-210350.

---

## Introduction

What do Mars rovers and cancer biomarker research have in common? More than you might expect. NASA's Jet Propulsion Laboratory (JPL) — an institution best known for sending spacecraft to distant planets — has been quietly building the data infrastructure behind some of the National Cancer Institute's most ambitious early cancer detection programs [1].

The connection is not as strange as it sounds. Both space science and cancer research generate massive observational datasets that must be transferred, stored, processed, and analyzed. Both require linking heterogeneous data types — from raw instrument readings to high-level interpreted results. And both are increasingly dependent on cloud computing, artificial intelligence, and large-scale collaborative infrastructure to make progress [1].

The paper I am exploring in this post describes **LabCAS** (Laboratory Catalog and Archive Service), a cloud-based data commons developed by JPL to support cancer biomarker research at the NCI. It is a compelling example of how infrastructure built for one scientific domain can be transferred — with real impact — to another.

---

## What is LabCAS?

LabCAS is a web-enabled, cloud-based environment designed to capture, organize, and provide centralized access to cancer biomarker data across multiple research institutions [1]. It was developed by JPL based on the same data science architectures used for Earth and space missions, and it serves as the backbone data commons for two of NCI's major programs:

- The **Early Detection Research Network (EDRN)**, focused on discovering and validating cancer biomarkers
- The **Consortium for Molecular and Cellular Characterization of Screen-Detected Lesions (MCL)**, focused on characterizing precancerous lesions

At the time of writing, the system holds approximately:

- **1,600 cancer biomarker annotations**
- **200 research protocols**
- **2,500 publications**
- **100 terabytes of cancer research data and images** [1]

These are not small numbers. LabCAS is not a prototype — it is an active, production-scale research infrastructure.

---

## What does LabCAS actually do?

The platform handles the full data lifecycle for biomarker research, from capture to publication. Its architecture has two main layers [1]:

**Front end:** A web portal where researchers can browse, search, visualize, and download data. It includes an interactive data dashboard, image viewers compatible with formats like DICOM and SVS, a clinical biospecimen viewer for cohort discovery, and support for favoriting frequently used datasets.

**Back end:** A cloud infrastructure built on Apache Solr for metadata search and Amazon S3 for data storage, exposing rich APIs that can be embedded directly into analytical tools like Jupyter Notebooks and R routines.

One design choice that stands out is how LabCAS handles data organization. Collections contain datasets, which can be nested hierarchically and contain files. Metadata is standardized through **Common Data Elements (CDEs)** — shared data structures that make it possible to link clinical data, imaging, genomics, and other measurement types in a consistent, machine-readable way [1].

Data in LabCAS can also be assigned a DOI through DataCite, enabling it to be formally cited in publications — treating datasets as first-class scientific outputs alongside papers.

---

## The space science connection

The most distinctive aspect of this paper is the explicit parallel between NASA's Science Data Systems (SDS) and LabCAS. The same high-level architecture — a **workflow execution engine** plus a **computing cluster** — underlies both the data pipelines of the Mars 2020 Perseverance rover instruments and the cancer image analysis workflows in LabCAS [1].

In LabCAS, this translates to:

- **Apache Airflow** as the workflow engine, running on AWS as Docker containers, managing sequences of data processing tasks
- **Kubernetes** as the container orchestration layer, scaling computation across worker nodes in the cloud

This means that running a deep learning model for tumor detection on mammograms uses the same fundamental infrastructure pattern as processing spectral data from Martian rock samples. That is a genuinely interesting insight, and it suggests that investment in general-purpose scientific data infrastructure can pay dividends across very different research domains.

---

## AI and machine learning in practice

The paper describes several applied examples of machine learning being deployed within LabCAS, which go beyond architectural descriptions into concrete scientific results [1]:

**Mammography analysis:** A pipeline adapted from Joseph Lo et al. uses a variant of RetinaNet (a YOLO model with multi-head attention) to detect malignancies in 2D full-field digital mammography images. It identifies lesions, lymph nodes, and architectural distortions, with pretrained weights that can be applied to new images or fine-tuned via transfer learning.

**Multiplexed tissue image registration:** LabCAS has been used to process very large multiplexed tissue scans with up to 45 image frames and billions of pixels, registering them spatially and then using convolutional neural networks to segment nuclei and identify tumor regions.

**Prostate cancer detection:** A technique borrowed from astronomy — the same logic used to create Hertzsprung-Russell diagrams of stellar populations — is applied to combine multiple MRI modalities, and a Faster R-CNN model trained on the result is used to identify tumors across different confidence thresholds in active surveillance patients.

**Neo-vascularization quantification in breast tissue:** An approach analogous to studying galactic filaments in cosmology is adapted to quantify vessel densities in breast MRI longitudinal data using 2D and 3D CNNs.

These are not toy examples. They represent serious applied research enabled by having the right data infrastructure in place.

---

## Crowdsourcing and virtual reality

Two more unconventional tools round out the paper's picture of the LabCAS ecosystem.

**Zooniverse**, a citizen science platform originally used to classify galaxies, is integrated into workflows for labeling tumors in lung imaging datasets. It can be restricted to domain experts or opened more broadly for simpler annotation tasks, and the labeled outputs are used to train convolutional neural networks — helping address the perennial challenge that supervised ML requires large, high-quality training datasets [1].

**Virtual Reality** is used to create a workspace for direct interaction with 3D CT data, allowing annotators to mark candidate lung nodules by navigating through slicing tools and density isosurfaces. This kind of interface can improve annotation quality and consistency, and the team is extending it to breast and other organ imaging [1].

---

## My critical view

LabCAS is genuinely impressive as an infrastructure project, and the paper does a good job of grounding it in concrete science examples rather than staying purely architectural. That said, there are dimensions worth thinking about critically.

### Main strengths

- Real-world scale: 100 terabytes of data, 1,600 biomarkers, and active use across multiple NCI consortia
- Clever technology transfer: space science infrastructure adapted with clear rationale, not just by analogy
- Practical AI integration: machine learning is applied to specific scientific tasks, not just described as a future possibility
- Open access where appropriate: post-publication data access, DOI-based data citation, open source tooling
- Security by design: role-based access control at collection, dataset, and file levels [1]

### Main limitations

- The paper reads partly as a system description and partly as a progress report, which makes it harder to assess rigorous scientific outcomes versus infrastructure achievements
- The ML models described are presented without detailed performance metrics in many cases — it would be useful to know accuracy, false positive rates, and clinical relevance more explicitly
- The cost and sustainability of cloud infrastructure at this scale is not discussed, which is a real concern for long-term biomarker programs
- Transfer learning and pretrained models are mentioned as capabilities, but the practical challenges of distribution shift across clinical sites are not deeply addressed [1]

None of these limitations undermine the value of the work, but they are worth keeping in mind when evaluating claims about what the infrastructure enables versus what it has demonstrably achieved.

---

## Conclusion

LabCAS is a strong example of how cloud computing infrastructure, when designed with the full data lifecycle in mind, can change what is scientifically possible. By centralizing data, computation, and algorithms in a single cloud environment, the JPL–NCI collaboration has made it feasible to apply machine learning at scale to cancer biomarker research across dozens of institutions [1].

The deeper lesson of the paper, however, is about **technology transfer**. The same architectural patterns that help scientists process data from a Mars rover can help oncologists link genomic sequences to precancerous tissue images. That kind of cross-domain thinking — taking proven infrastructure from one data-intensive science and adapting it carefully to another — may be one of the most underrated strategies in biomedical data science.

As data volumes in cancer research continue to grow, and as AI methods demand ever larger and better annotated training sets, the value of robust shared infrastructure like LabCAS will only increase.

---

## References

1. Crichton DJ, Cinquini L, Kincaid H, Mahabal A, Altinok A, Anton K, Colbert M, Kelly S, Liu D, Patriotis C, Lombeyda S, Srivastava S. From space to biomedicine: Enabling biomarker data science in the cloud. *Cancer Biomarkers*. 2022;33(4):479–488. doi:10.3233/CBM-210350.

---

*Tags: cloud computing · biomedicine · cancer research · data science · artificial intelligence*
