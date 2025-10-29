# Introduction-to-Neoverse

The purpose of this material is to introduce the Arm® Neoverse™ range of processors for developers who wish to write software for devices powered by Neoverse cores
Readers should gain an appreciation of the purpose and reasoning behind major features of the Armv9 architecture and of the range of Neoverse processors. This is intended to enable readers to make informed choices when selecting a target platform for a particular use case, including tool selection and software development methodology. This material can also serve as a resource for those looking to learn or teach about server computing.

# Navigate this document by use case (jump-off routes)

Here are some possible use cases, should you wish to find specific sections of this resource that are relevant to your interests.

## Cloud-native app developer (containers, CI/CD)

- Where to run (instance families, vCPU shapes): **Part 1 Section 6.3 - Cloud Implementations**
- Pick a broadly supported distro/hypervisor: **Part 2 Section 6 - Operating Systems & Hypervisors**
- Build/test in-cloud with familiar tools (Docker, Kubernetes, Jenkins, etc.): **Part 2 Section 8 - Cloud-Native Tooling**
- Package/port your app; call out arch/CPU target: **Part 2 Section 9 - Applications**

## HPC / vectorized compute (SVE/SVE2 focus)

- Choose the core line aimed at peak throughput: **Part 1 Section 5.3 - Neoverse V-Series**
- Review Armv9 overview to understand vector features in context: **Part 1 Section 4 - Armv9 Overview**
- Build with the right arch/CPU switches; verify features via `lscpu`: **Part 2 Section 9 - Applications**

## OS/Infra, porting, or “how the system comes up” 

- Land on a portable baseline (certified platforms): **Part 1 Section 6.1 - SystemReady** 
- How pieces fit (AP/SCP/MCP; realms vs non-secure): **Part 2 Section 3 - A Typical Software Stack**
- Chain of trust to UEFI/OS (flow + steps): **Part 2 Section 4 - The Boot Sequence: Hardware to Operating System**
- Discover hardware properly (ACPI vs Device Tree): **Part 2 Section 5 - Device and Platform Discovery**

## Confidential computing / CCA
Start with placement and isolation, then the trust boundary:
- Why it matters (“control without access”): **Part 2 Section 2 - Security Considerations**
- System view of Root/Secure/Realm: **Part 2 Section 3 - A Typical Software Stack**

## Inclusive Language Commitment
Arm is committed to making the language we use inclusive, meaningful, and respectful. Our goal is to remove and replace non-inclusive language from our vocabulary to reflect our values and represent our global ecosystem.

Arm is working actively with our partners, standards bodies, and the wider ecosystem to adopt a consistent approach to the use of inclusive language and to eradicate and replace offensive terms. We recognise that this will take time. This course has been updated to replace references to non-inclusive language. We recognise that some of you will be accustomed to using the previous terms and may not immediately recognise their replacements. Please refer to the following example:
- When introducing the AMBA 3 AHB-Lite Protocols, we will use the term ‘Manager’ instead of ‘Master’ and ‘Subordinate’ instead of ‘Slave’.

This course may still contain other references to non-inclusive language; it will be updated with newer terms as those terms are agreed and ratified with the wider community.

Contact us at education@arm.com with questions or comments about this course. You can also report non-inclusive and offensive terminology usage in Arm content at terms@arm.com.
