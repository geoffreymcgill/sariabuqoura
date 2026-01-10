---
label: NIST Cybersecurity
icon: book 
order: 999
---
!!!
Last Update on Jan, 2026.
!!!

# NIST Cybersecurity (CSF)

## Overview
The NIST Cybersecurity Framework (CSF) 2.0 provides guidance to industry, government agencies, and other organizations to manage cybersecurity risks. 

It offers a taxonomy of high level cybersecurity outcomes that can be used by any organization regardless of its size, sector, or maturity to better understand, assess, prioritize, and communicate its cybersecurity efforts.

Ideally, the CSF will be used to address `cybersecurity risks` alongside other risks of the enterprise, including those that are `financial`, `privacy`, `supply chain`, `reputational`, `technological`, or `physical` in nature.

The CSF describes desired outcomes that are intended to be understood by a broad audience,including executives, managers, and practitioners, regardless of their cybersecurity expertise. 

While many cybersecurity risk management activities focus on preventing negative events from occurring, they may also support taking advantage of positive opportunities. Actions to reduce cybersecurity risk might benefit an organization in other ways, like increasing revenue.
(e.g., first offering excess facility space to a commercial hosting provider for hosting their own and other organizations’ data centers, then moving a major financial system from the organization’s in-house data center to the hosting provider to reduce cybersecurity risks).


> [!NOTE] Outcomes
> * Outcomes are clear, measurable security results that an organization aims to achieve.
> * Outcomes describe the desired security state.
> * Controls, Tools, and Processes exist only to achieve these outcomes.
> * Outcomes are mapped directly to a list of potential security controls for immediate consideration to mitigate cybersecurity risks.
> * Example: “Unauthorized users are prevented from accessing systems”. This is an outcome, not “use firewall” or “install IAM tool”, Technology-agnostic (no vendor lock-in)

## Framework
### Components 

==- 1- CSF Core
A set of cybersecurity outcomes arranged by Function, then Category, and finally Subcategory, as shown in Fig.1. 
The structure of the Core is intended to resonate most with those charged with operationalizing risk management within an organization.
The CSF Core Functions — GOVERN, IDENTIFY, PROTECT, DETECT, RESPOND, and RECOVER.   

* GOVERN: Function provides outcomes to inform what an organization may do to achieve and prioritize the outcomes of the other five Functions.
* IDENTIFY: The organization’s current cybersecurity risks are understood.
* PROTECT: Safeguards to manage the organization’s cybersecurity risks are used.
* DETECT: Possible cybersecurity attacks and compromises are found and analyzed.
* RESPOND: Actions regarding a detected cybersecurity incident are taken.
* RECOVER: Assets and operations affected by a cybersecurity incident are restored.

The CSF Core is forward-looking and intended to apply to future changes in technologies and environments.

![Framework Core Categories and Functions](/static/images/CSFCore.png)

* CSF Functions as a wheel because all of the Functions relate to one another.For example:
* an organization will categorize assets under IDENTIFY and take steps to secure those assets under PROTECT.
* Investments in planning and testing in the GOVERN and IDENTIFY Functions will support timely detection of unexpected events in the DETECT Function, as well as enabling incident response and recovery actions for cybersecurity incidents in the RESPOND and RECOVER Functions.
* GOVERN is in the center of the wheel because it informs how an organization will implement the other five Functions. 

![CSF Functions](/static/images/CSFFunctions.png)
===
==- 2- CSF Organizational Profiles
A mechanism for describing an organization’s current and/or target cybersecurity posture in terms of the CSF Core’s outcomes.
![CSF Organizational Profile](/static/images/CSFOrganizationalProfile.png)
===
==- 3- CSF Tiers
Can be applied to CSF Organizational Profiles to characterize the rigor of an organization’s cybersecurity risk governance and management practices.
![CSF Tiers](/static/images/CSFTiers.png)
===

### Components Benefit 
An organization can use the `CSF Core`, `Profiles`, and `Tiers` with the supplementary resources to:
* Understand, assess. (Describe the current or target cybersecurity posture & determine gaps) 
* Prioritize. (Identify, organize, and prioritize actions for managing cybersecurity risks)
* Communicate cybersecurity risks.  (Provide a common language for communicating inside and outside the organization about cybersecurity risks, capabilities, needs, and expectations)


!!!warning Warning
* Before version 2.0, the Cybersecurity Framework was called the “Framework for Improving Critical Infrastructure Cybersecurity.” This title is not used for CSF 2.0. 
* The CSF does not prescribe how outcomes should be achieved. Rather, it links to online resources that provide additional guidance on practices and controls that could be used to achieve those outcomes.
* This document describes what desirable outcomes an organization can aspire to achieve. It does not prescribe outcomes nor how they may be achieved. 
* Descriptions of how an organization can achieve those outcomes are provided in a suite of online resources that complement the CSF and are available through the NIST CSF website. https://www.nist.gov/cyberframework 
!!!

## Sources
* https://www.nist.gov/cyberframework
* https://nvlpubs.nist.gov/nistpubs/CSWP/NIST.CSWP.29.pdf


