```markdown
---
title: "Hardware Specifications"
category: "computing-resources"
description: "Details about the computing hardware available at SCRC, including cloud server specifications and network infrastructure."
---

# Hardware Specifications

This page provides details about the computing hardware resources available at the NYU Stern Center for Research Computing (SCRC). This includes specifications for cloud servers and information about the network and storage infrastructure.

## Cloud Servers

SCRC provides access to several high-performance cloud servers suitable for various computational tasks, including GPU processing. The specifications for these servers are as follows:

*   **tiffany:**
    *   **RAM:** 766 GB
    *   **CPU:** 96 x 2.1 GHz Intel Xeon Platinum 8160
*   **einstein:**
    *   **RAM:** 1.5 TB
    *   **CPU:** 96 x 2.1 GHz Intel Xeon Platinum 8160
*   **hawking:**
    *   **RAM:** 768 GB
    *   **CPU:** 56 x 2.59 GHz Intel Xeon Gold 6132
*   **nobel:**
    *   **RAM:** 384 GB
    *   **CPU:** 64 x 2.59 GHz Intel Xeon GPU E5-2697A v4

These servers form part of a small VMware cloud environment used to support researchers with specialized needs, allowing for the creation of customized virtual machines (VMs).

## Other Hardware

Beyond the primary cloud servers, the SCRC infrastructure includes:

*   **Network Switches:** NetGear 10GB switches are utilized to ensure high-speed intra-cluster and inter-cluster communication, facilitating efficient data transfer and parallel processing.
*   **Storage:** The center employs both Network-Attached Storage (NAS) and Storage Area Network (SAN) devices, providing a total storage capacity exceeding 120 TB for research data. This includes the `bighome` directory space for large dataset storage.
```