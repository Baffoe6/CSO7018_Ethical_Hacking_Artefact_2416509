# CSO7018 Ethical Hacking — Lab Report
## Unit 2 Lesson 1: OSINT Investigation Using Maltego

---

| | |
|---|---|
| Student ID | 2416509 |
| Module | CSO7018 Ethical Hacking |
| Assessment | Artefact 2 — VM Lab Practical Activities |
| Activity | Unit 2, Lesson 1 — Open Source Intelligence Using Maltego |
| Date Performed | 22 May 2026 |
| Environment | Kali Linux VM — Authorized University Lab |

---

## Table of Contents

1. Introduction
2. Objectives
3. Methodology
4. Tool Overview — Maltego
5. Commands and Actions
6. Findings
7. Screenshots and Analysis
8. Ethical Considerations
9. Reflection
10. Conclusion
11. References

---

## 1. Introduction

Open Source Intelligence (OSINT) is a foundational discipline within ethical hacking and penetration testing. OSINT involves the collection, analysis, and correlation of information from publicly available sources — including websites, social media platforms, public registries, and academic publications — to build a comprehensive intelligence picture of a target without direct interaction with protected systems.

Maltego, developed by Paterva, is a widely used OSINT platform that enables investigators to visualise complex data relationships through an interactive graph-based interface. It automates the process of querying multiple public data sources through "transforms" — programmatic queries that return structured entity data — and plots the results as a navigable network graph.

This activity demonstrates the application of Maltego within a controlled, authorized educational context, adhering to the principles of responsible and ethical intelligence gathering.

---

## 2. Objectives

By the end of this activity, the following outcomes were achieved:

- Successfully install and configure Maltego Community Edition on Kali Linux.
- Create an OSINT investigation by defining a seed entity (Phrase or Domain).
- Execute public-source transforms, including Wikipedia lookups and NLP-based entity extraction.
- Interpret the resulting entity graph to identify relationships between discovered data points.
- Critically evaluate the implications of publicly available OSINT data for organizational security posture.

---

## 3. Methodology

The investigation followed a structured OSINT methodology:

1. Preparation — Maltego CE was launched on Kali Linux. A new investigation graph was created.
2. Seed Entity Creation — A Phrase entity was added to the graph as the investigation anchor.
3. Transform Execution — Public transforms were run against the seed entity, including Wikipedia-sourced data and IBM Watson/Paterva NLP entity extraction.
4. Graph Analysis — The resulting entity nodes and their interconnections were examined and documented.
5. Evidence Capture — Screenshots were taken at each significant step.

All activities remained within the Community Edition free tier, using only publicly available data sources.

---

## 4. Tool Overview — Maltego

| Attribute | Detail |
|-----------|--------|
| Tool Name | Maltego Community Edition (CE) |
| Developer | Paterva (now part of Maltego Technologies) |
| Platform | Cross-platform (Java-based); available on Kali Linux |
| Primary Use | OSINT / link analysis / threat intelligence |
| Interface | GUI — Graph-based entity relationship mapping |
| Transform Sources | Wikipedia, Shodan, VirusTotal, DNS, WHOIS (varies by edition) |
| Cost | Community Edition: Free (limited transforms per day) |

Maltego uses an entity-relationship model where:
- Entities represent data objects (persons, domains, phrases, organisations, IP addresses)
- Transforms are automated queries that discover relationships between entities
- Graphs visualise the connections between discovered entities

---

## 5. Commands and Actions

| Step | Action / Command | Description |
|------|-----------------|-------------|
| 1 | Launch Maltego CE | Start the Maltego application from the Kali Applications menu or terminal |
| 2 | New Graph → Add Entity → Phrase | Create a Phrase entity as the investigation seed |
| 3 | Configure entity text value | Set the phrase/keyword for the investigation |
| 4 | Right-click entity → Run Transform → Wikipedia | Execute Wikipedia transform to retrieve related articles and entities |
| 5 | Run IBM Watson / To Entities | Execute NLP entity extraction on identified text |
| 6 | Zoom to Fit / Arrange Graph | Visualise full entity graph |

---

## 6. Findings

> Note: Only document findings visible in your actual screenshots. Do not invent data.

### 6.1 Entity Discovery

### 6.2 Relationship Mapping

### 6.3 NLP Entity Extraction

---

## 7. Screenshots and Analysis

### Screenshot 1 — Maltego Installation and Launch

Figure 1: Maltego Community Edition application launched on Kali Linux.

Analysis: The screenshot confirms that Maltego CE is installed and operational on the Kali Linux VM. The application home screen presents the investigation workspace and available transform options. The Community Edition interface is visible, indicating free-tier access with standard public transforms.

---

### Screenshot 2 — Phrase Entity Configuration

Figure 2: Phrase entity added to the Maltego investigation graph.

Analysis: A Phrase entity has been instantiated as the seed node for the investigation. The entity text value serves as the investigation anchor from which transforms will extract related data. This demonstrates the initial step in any Maltego OSINT investigation — defining the entry point.

---

### Screenshot 3 — Wikipedia Transform Results

Figure 3: Wikipedia transform executed against the seed entity, showing returned results.

Analysis: The Wikipedia transform queried the public Wikipedia API using the phrase entity as a search parameter. This demonstrates how Maltego automates correlation between a simple seed value and publicly indexed encyclopaedic knowledge.

---

### Screenshot 4 — IBM Watson / NLP Entity Extraction

Figure 4: IBM Watson NLP transform results showing extracted named entities.

Analysis: The NLP entity extraction transform analysed retrieved text and identified named entities including. This technique mirrors professional threat intelligence workflows, where unstructured text is processed to extract actionable intelligence data.

---

### Screenshot 5 — Full Investigation Graph

Figure 5: Complete Maltego OSINT investigation graph showing all entity relationships.

Analysis: The full graph reveals the breadth of publicly available data associated with the seed entity. The visual representation demonstrates how seemingly unrelated data points, when aggregated, can reveal significant intelligence about a subject.

---

## 8. Ethical Considerations

OSINT activities, while involving only publicly available data, carry inherent ethical responsibilities. The following principles governed this investigation:

Authorization: This activity was conducted within the explicitly authorized scope of the CSO7018 module curriculum. No investigation of real individuals or organizations was performed without authorization.

Data Minimization: Only the data returned by the Community Edition public transforms was collected. No attempts were made to access private, restricted, or protected data sources.

Privacy: Maltego investigations can expose significant personal information when directed at individuals. In professional practice, investigators must ensure OSINT activities comply with applicable data protection legislation, including the UK GDPR and the Data Protection Act 2018.

Purpose Limitation: Data collected in this activity is used solely for the educational purpose of demonstrating OSINT methodology and will not be processed for any other purpose.

Proportionality: The investigation scope was limited to what was necessary to meet the activity objectives, consistent with the principle of proportionality in intelligence collection.

---

## 9. Reflection

This activity provided practical experience with a professional-grade OSINT platform used widely in the cyber threat intelligence and penetration testing industries. The graph-based visualisation approach in Maltego demonstrated how aggregating multiple small, individually innocuous data points from public sources can construct a comprehensive intelligence picture.

A key learning was the importance of seed entity selection — the choice of starting entity significantly influences the breadth and relevance of transform results. Poor seed selection results in noisy, irrelevant graph data, while a precise seed produces actionable intelligence.

The activity also highlighted the dual-use nature of OSINT tools: the same techniques used by security professionals for defensive intelligence gathering are available to adversarial actors. This reinforces the importance of organizations actively monitoring their own digital footprint and managing publicly accessible information.

---

## 10. Conclusion

This activity successfully demonstrated the application of Maltego as an OSINT investigation platform within a controlled educational environment. By progressing from a single seed entity through automated public transforms, a multi-node entity graph was constructed, visualising the relationships between publicly available data points.

The exercise confirmed the power of graph-based OSINT analysis for building intelligence from disparate public sources. The findings have direct relevance to the reconnaissance phase of a structured penetration test, where comprehensive target knowledge informs subsequent exploitation strategy.

All activities were conducted ethically, within authorized scope, and in compliance with the principles of responsible information security practice.

---

## 11. References

Bazzell, M. (2023) Open Source Intelligence Techniques: Resources for Searching and Analysing Online Information. 10th edn. IntelTechniques.

Computer Misuse Act 1990 (c.18) UK Parliament. Available at: https://www.legislation.gov.uk/ukpga/1990/18/contents [Accessed: 22 May 2026].

Engebretson, P. (2013) The Basics of Hacking and Penetration Testing. 2nd edn. Syngress.

Hutchins, E., Cloppert, M. and Amin, R. (2011) Intelligence-Driven Computer Network Defense Informed by Analysis of Adversary Campaigns and Intrusion Kill Chains. Lockheed Martin Corporation.

IBM (2024) IBM Watson Natural Language Understanding. Available at: https://www.ibm.com/cloud/watson-natural-language-understanding [Accessed: 22 May 2026].

Maltego Technologies (2024) Maltego Documentation and User Guide. Available at: https://docs.maltego.com [Accessed: 22 May 2026].

Paterva (2023) Introduction to Maltego Transforms. Available at: https://www.maltego.com/transform-hub/ [Accessed: 22 May 2026].

SANS Institute (2022) Open-Source Intelligence (OSINT): A Practitioner's Guide. Available at: https://www.sans.org/white-papers/ [Accessed: 22 May 2026].

UK Government (2018) Data Protection Act 2018. Available at: https://www.legislation.gov.uk/ukpga/2018/12/contents [Accessed: 22 May 2026].

UK Information Commissioner's Office (2024) Guide to the UK General Data Protection Regulation (UK GDPR). Available at: https://ico.org.uk/for-organisations/guide-to-data-protection/ [Accessed: 22 May 2026].

---

Report prepared as part of CSO7018 Ethical Hacking, Artefact 2. Student ID: 2416509.
