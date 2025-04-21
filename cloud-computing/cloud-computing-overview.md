```markdown
---
title: "Cloud Computing Overview"
category: "cloud-computing"
description: "Introduction to Stern's private cloud computing environment, its benefits, and general use cases."
---

# Cloud Computing Overview

## Introduction

The Stern Center for Research Computing (SCRC) offers a private cloud computing environment designed to support researchers with specialized computational needs. This environment allows the SCRC team to quickly provide you with a virtual machine (VM) tailored for your research.

This service is particularly useful for faculty who have research funds for equipment; typically, they purchase a cloud server, and their applications run in dedicated VMs on that server, alongside other VMs. This approach enhances flexibility, resource utilization, power savings, and administrative ease.

## What is a Virtual Machine?

A virtual machine (VM) functions essentially like a complete physical computer but runs within Stern's shared cloud infrastructure. Key aspects include:

*   **Customization:** Each VM can be configured with specific amounts of memory, disk space, number of processors, operating system (Windows or Linux), and pre-installed software based on your research requirements.
*   **Isolation:** VMs operate independently, ensuring your environment is separate from others.

## Benefits of Using Stern's Cloud Environment

Utilizing Stern's private cloud and virtual machines offers several advantages for researchers:

*   **Customization:** Tailor VM resources (memory, disk, CPU, OS, software) precisely to your project needs.
*   **Accessibility:** Access your dedicated computing environment securely from anywhere (office, home, or abroad). Off-campus access requires connecting to the NYU VPN.
*   **Collaboration:** Facilitates collaboration with colleagues, regardless of their physical location.
*   **Efficiency & Cost-Effectiveness:** Get computing resources provisioned and configured quickly without the financial overhead and delay of purchasing and setting up physical hardware.
*   **Resource Optimization:** Frees up your personal computer, allowing it to be used for other tasks while computations run on the VM.
*   **Flexibility & Reliability:** VMs can be migrated between physical cloud servers if maintenance or resource balancing is necessary, improving overall service reliability.

## Getting Started

### Requesting a Virtual Machine

SCRC maintains a VMware cloud environment to support researchers.

1.  **Send a Request:** Email `scrc-list@stern.nyu.edu` with a description of your research needs. Include details such as:
    *   Required operating system (Windows or Linux are supported).
    *   Specific software packages needed.
    *   Estimates for computational requirements (CPU cores, memory/RAM, disk storage).
2.  **Consultation:** SCRC staff will schedule a meeting to discuss your requirements in detail.
3.  **Provisioning:** A customized VM can typically be provisioned within a day or so after the consultation. A common starting configuration is 6 CPU cores and 32GB RAM, but this is adjustable.

### Accessing Your Virtual Machine

You will receive specific instructions on how to connect to your VM once it is ready. Remember to connect to the [NYU VPN](link-to-nyu-vpn) first if you are accessing the VM from off-campus.

## Cloud Server Hardware

The SCRC's private cloud environment is supported by powerful server hardware. While your VM provides isolated resources, it runs on physical servers such as these:

*   **tiffany:** 766GB RAM, 96 CPU x 2.1 GHz Intel Xeon Platinum 8160
*   **einstein:** 1.5TB RAM, 96 CPU x 2.1 GHz Intel Xeon Platinum 8160
*   **hawking:** 768GB RAM, 56 CPU x 2.59 GHz Intel Xeon Gold 6132
*   **nobel:** 384GB RAM, 64 CPU x 2.59 GHz Intel Xeon GPU E5-2697A v4

**Note:** The specific resources allocated to your VM are determined during the request and consultation process, based on your needs and overall system availability.
```