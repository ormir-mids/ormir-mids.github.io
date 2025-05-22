# ORMIR-MIDS
**Standardizing the Organization of Musculoskeletal Imaging Data**
<!-- ---
title: ORMIR-MIDS
subtitle: Standardizing the organization of musculoskeletal imaging data
authors:
  - name: The ORMIR community
    email: ormircommunity@gmail.com
license: CC-BY-4.0
keywords: MSK data, MSK imaging, ORMIR community, BIDS

--- -->

<br>
<br>

```{image} ./figures/ORMIR-MIDS_figure.png
:alt: ORMIR-MIDS data structure
:width: 700px
:align: center
```

---


## What is ORMIR-MIDS?

Musculoskeletal (MSK) imaging data can be **structured in various ways**, depending on institutional, group, or personal preferences. 

Having a **standardized data structure** is highly desirable to **facilitate data sharing** and to provide a **common interface for processing and analysis software** to read and write data in an interoperable way 

Currently, **there is no defined standard** on how the MSK imaging data should be structured. 

Inspired by the Brain Imaging Data Structure ([BIDS](https://bids.neuroimaging.io/index.html)) tools, the **[ORMIR](https://www.ormir.org/) community is creating ORMIR-MIDS** to structure MSK imaging data


ORMIR-MIDS includes two aspects:


::::{grid}
:gutter: 2

:::{grid-item-card} ✏️ {ref}`A Standard Specification <specs>`
How to organize MSK medical images and corresponding clinical information
:::

:::{grid-item-card} 🚀 {ref}`A Python Package <package>`
To transform MSK imaging data into a standard structure
:::

::::


---

## Why is ORMIR-MIDS important for MSK computational tools?


We want to have a **uniform interface** for software tools for MSK image processing and analysis.   
Ideally, each tool will have a command-line interface with the following syntax:

```
msk_software_tool <patient_folder>
```
where `patient_folder` is the *location of the root (or parent) folder* containing the acquired data, structured according to the ORMIR-MIDS standard specification

The MSK tools should also **output data in the correct format** in the same folder structure

---

## Learn more about ORMIR-MIDS

In this video, you will find a presentation about ORMIR-MIDS, followed by a hands-on tutorial on how to use it

<iframe width="560" height="315" 
    src="https://www.youtube.com/embed/MpF3J07TcG8" 
    frameborder="0" 
    allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" 
    allowfullscreen>
</iframe>

Find the slides on [Zenodo](www.doi.org/10.5281/zenodo.15488134) and the Jupyter Notebook on [GitHub](https://github.com/ormir-mids/ormir-mids/blob/main/jupyter/ormir-mids-dcm2omids.ipynb)

---

:::{admonition} Why the name ORMIR-MIDS? How did ORMIR-MIDS start?
:class: hint
:class: dropdown

*ORMIR-MIDS* comes from ORMIR (Open and Reproducible Musculoskeletal Imaging Research (ORMIR) community and *MIDS*  (Medical Imaging Data Structure)

The development of ORMIR-MIDS specification and package started during the 2nd [ORMIR](https://ormircommunity.github.io/) workshop [Sharing and Curating Open Data in Musculoskeletal Imaging Research](https://github.com/ORMIRcommunity/2024_2nd_ORMIR_WS/blob/main/README.md) and is currently ongoing. 

ORMIR-MIDS is an extension of [muscle-BIDS](https://github.com/muscle-bids/muscle-bids), which was partly developed during the 1st [ORMIR](https://ormircommunity.github.io/) workshop [Building the Jupyter Community in Musculoskeletal Imaging Research](https://github.com/JCMSK/2022_JCW/blob/main/README.md). 

Both [ORMIR-MIDS](https://github.com/ormir-mids/ormir-mids) and [muscle-BIDS](https://github.com/muscle-bids/muscle-bids) are part of the [ORMIR](https://ormircommunity.github.io/) community core projects.

:::


:::{admonition} How do I cite ORMIR-MIDS?
:class: note

Thank you for citing ORMIR-MIDS! Here is our publication:

S. Bonaretti, M. A. Espinosa Hernandez, F. Chiumento, Y. Founas, M. Froeling, J. Hirvasniemi, G. Iori, Y. Lee, S. Matuschik, M. Monzon, F. Santini, D. Cameron. ***ORMIR-MIDS: An open standard for curating and sharing musculoskeletal imaging data***. 24{sup}`th` International Workshop on Quantitative Musculoskeletal Imaging (QMSKI). The Barossa Valley, South Australia. November 3-8, 2024. 

:::

---
