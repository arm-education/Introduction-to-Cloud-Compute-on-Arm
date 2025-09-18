# Part 1

## Introduction to Neoverse Cores — Questions

------------------------------------------------------------------------

### 1. Which of the following scenarios most accurately illustrates how architectural “optional features” in Armv9–A impact cross-platform software development on Neoverse?

1)  Code that depends on a mandatory instruction set always works across
    all Armv9–A implementations
2)  Software must dynamically query for the presence of optional
    features and adapt, as their implementation is not guaranteed
3)  The absence of optional features triggers a hardware fault, stopping
    execution
4)  Optional features are always implemented for compatibility

**Answer:** B

**Feedback:**  
- *Correct (B):* Optional features may or may not be present, so robust
software must detect them at runtime and adapt, ensuring broad
compatibility.  
- *Incorrect (A):* Mandatory features are consistent, but this does not
address the challenge of optional features.  
- *Incorrect (C):* The absence of optional features is handled according
to the architecture, not by faulting.  
- *Incorrect (D):* Optional features are not guaranteed to be present,
so assuming their presence is unsafe.  
- *Section:* 5.1 Architecture, Implementation and Manufacturing

------------------------------------------------------------------------

### 2. Suppose a developer is porting a hypervisor designed for x86 VT-x to a Neoverse V2 platform. Which architectural feature(s) should be the *primary focus* for ensuring functional parity in hardware virtualization support?

1)  TrustZone
2)  Exception Levels EL2 and ARM Virtualization Extensions
3)  Only SVE2
4)  SystemReady Certification

**Answer:** B

**Feedback:**  
- *Correct (B):* EL2 and virtualization extensions in Armv8/9–A mirror
VT-x, providing essential hardware support for hypervisors.  
- *Incorrect (A):* TrustZone is designed for secure/non-secure world
separation, not for virtualization at the hypervisor level.  
- *Incorrect (C):* SVE2 is for vector processing, not virtualization.  
- *Incorrect (D):* SystemReady concerns platform standardization, not
hardware virtualization features.  
- *Section:* 4.1 Exceptions, Modes, States; Correlation with x86
Features

------------------------------------------------------------------------

### 3. Which of the following best explains why Neoverse E1 was the *first* Arm core to implement Simultaneous Multi-Threading (SMT), and what specific workload characteristic justified this design choice?

1)  SMT increases security for confidential compute
2)  SMT allows higher single-thread latency for throughput-oriented
    network edge workloads
3)  SMT reduces instruction fetch bandwidth
4)  SMT is necessary for real-time deterministic control loops

**Answer:** B

**Feedback:**  
- *Correct (B):* E1 targets edge/data transport where throughput is
prioritized over single-thread latency; SMT leverages pipeline
utilization for such workloads.  
- *Incorrect (A):* SMT does not inherently increase security; it’s
focused on efficiency and throughput.  
- *Incorrect (C):* SMT may actually increase fetch pressure, not reduce
it.  
- *Incorrect (D):* Real-time deterministic loops often avoid SMT due to
non-determinism.  
- *Section:* 5.5 Neoverse E1

------------------------------------------------------------------------

### 4. Which cache and coherency architecture choice most distinguishes Neoverse N1’s scalability for hyperscale applications compared to previous Neoverse cores?

1)  Use of only private L1 caches and direct memory access
2)  Configurable bus architecture allowing up to 128-core clusters per
    socket via CCIX connectivity
3)  No L3 cache implementation
4)  Non-coherent interconnects to save power

**Answer:** B

**Feedback:**  
- *Correct (B):* The advanced interconnect and scalable cache structure
(including CCIX for multi-chip packaging) are key to N1’s suitability
for hyperscale infrastructure.  
- *Incorrect (A):* Only private L1 caches do not enable system
scalability for large core counts.  
- *Incorrect (C):* Absence of L3 does not enable or characterize
hyperscale.  
- *Incorrect (D):* Non-coherent interconnects would break the
programming model for large shared-memory systems.  
- *Section:* 5.4 Neoverse N; 5.6 Neoverse Compute Subsystems

------------------------------------------------------------------------

### 5. In what way does the introduction of Realm and Root security states (via RME) in Armv9.x fundamentally alter the security threat model compared to earlier TrustZone implementations?

1)  It enables non-secure code to access secure state with privilege
2)  Realms provide isolated compartments inaccessible even to the
    hypervisor/OS, not possible with classic TrustZone
3)  It eliminates the need for any privileged firmware
4)  TrustZone never supported non-secure states

**Answer:** B

**Feedback:**  
- *Correct (B):* RME/Realms create hardware-enforced isolation that
protects even from the hypervisor/OS, addressing advanced threat
models.  
- *Incorrect (A):* RME/Realms further restrict access, not grant it.  
- *Incorrect (C):* Privileged firmware is still required for system
management and security boundaries.  
- *Incorrect (D):* TrustZone explicitly separates secure and non-secure
states.  
- *Section:* 4.1 Security States

------------------------------------------------------------------------

### 6. Which version of Armv9–A first made Memory Partitioning and Monitoring (MPM) a mandatory feature, and what system-level problem does MPAM address?

1)  Armv9.0–A; supports pointer authentication
2)  Armv9.1–A; mitigates performance interference by controlling memory
    bandwidth per process
3)  Armv9.2–A; improves atomic memory operations
4)  Armv9.4–A; guards branch history

**Answer:** B

**Feedback:**  
- *Correct (B):* Armv9.1–A introduced mandatory MPAM for partitioning
and bandwidth monitoring to isolate and manage memory interference
across workloads.  
- *Incorrect (A):* Pointer authentication is separate from MPAM and was
introduced earlier.  
- *Incorrect (C):* Armv9.2–A improved atomic ops, not memory
partitioning.  
- *Incorrect (D):* Armv9.4–A added branch history protections, not
MPAM.  
- *Section:* 4.3 Armv9.1–A

------------------------------------------------------------------------

### 7. Which of the following most accurately characterizes the correlation between x86 AVX-512 and Arm’s SVE/SVE2 extensions in Neoverse V-series?

1)  AVX-512 and SVE2 both fix their vector length to 512 bits
2)  SVE2 enables variable-length vectors up to 2048 bits, supporting
    scalable HPC and AI, unlike fixed-length AVX-512
3)  AVX-512 supports vector lengths above 2048 bits, SVE2 does not
4)  SVE2 and AVX-512 are not relevant for machine learning workloads

**Answer:** B

**Feedback:**  
- *Correct (B):* SVE/SVE2’s variable-length approach provides unique
scalability for high-performance and AI, beyond AVX-512’s fixed width.  
- *Incorrect (A):* Only AVX-512 is fixed-width; SVE2 is variable.  
- *Incorrect (C):* AVX-512 maxes out at 512 bits, SVE2 can be up to
2048.  
- *Incorrect (D):* Both are critical for modern AI/HPC workloads.  
- *Section:* 5.8 Correlation with x86 Features

------------------------------------------------------------------------

### 8. What is a subtle, but crucial, consequence of Arm’s “weakly-ordered” memory model for concurrent software on Neoverse platforms, and how should it be addressed in systems code?

1)  All memory accesses are always strongly ordered, so concurrency bugs
    are rare
2)  Compilers and hardware may reorder accesses, so explicit memory
    barriers or atomic instructions are needed to enforce ordering
3)  Devices on Neoverse cannot use shared memory
4)  It is only relevant for instruction fetches, not data

**Answer:** B

**Feedback:**  
- *Correct (B):* Weak ordering means that the CPU and compiler may
reorder memory ops; barriers/atomics are essential for correctness in
synchronization primitives.  
- *Incorrect (A):* Arm specifically allows reordering, so race
conditions are a real risk.  
- *Incorrect (C):* Shared memory is commonly used, but must be carefully
controlled.  
- *Incorrect (D):* Memory ordering is critical for both instruction and
data paths, especially in SMP.  
- *Section:* 9. Applications — Memory Model

------------------------------------------------------------------------

### 9. For a cloud vendor wanting to deploy Arm-based servers that maximize out-of-box software compatibility and minimize engineering costs for firmware/OS support, which Neoverse-related program should they prioritize, and why?

1)  Armv7-M compliance; for microcontroller compatibility
2)  SystemReady certification; ensures standards-based firmware/hardware
    for ecosystem compatibility
3)  Only proprietary bootloaders
4)  Corstone subsystem adoption

**Answer:** B

**Feedback:**  
- *Correct (B):* SystemReady assures cross-platform compatibility,
simplifying OS and software enablement and reducing custom
engineering.  
- *Incorrect (A):* Armv7-M is for microcontrollers, irrelevant to
server/cloud.  
- *Incorrect (C):* Proprietary bootloaders undermine compatibility and
ecosystem support.  
- *Incorrect (D):* Corstone is for rapid subsystem prototyping, not
ecosystem certification.  
- *Section:* 6.1 SystemReady

------------------------------------------------------------------------

### 10. Which technical factor distinguishes an architecture licensee’s product from an implementation licensee’s, and what unique risk or benefit does it introduce?

1)  Architecture licensees must use Arm’s microarchitecture, reducing
    flexibility
2)  Architecture licensees design their own cores, allowing
    differentiation but requiring large teams and risk of non-compliance
3)  Implementation licensees cannot customize cache size
4)  Both must manufacture only in Cambridge

**Answer:** B

**Feedback:**  
- *Correct (B):* Architecture licensees can innovate at the
microarchitectural level, potentially gaining competitive edge but at
the cost of higher engineering complexity and compliance risk.  
- *Incorrect (A):* The whole point is to allow custom microarchitecture,
not restrict it.  
- *Incorrect (C):* Implementation licensees have flexibility over cache
and other parameters.  
- *Incorrect (D):* There is no manufacturing location restriction.  
- *Section:* 3.2 Rapid Evolution

------------------------------------------------------------------------

### 11. Which Neoverse Compute Subsystem (CSS) is designed for the highest AI/ML and HPC scalability, and what unique memory/I/O support features does it provide?

1)  CSS N2; supports only DDR3 memory
2)  CSS V3; up to 64 Neoverse V3 cores, 12 channels DDR5, 64-lane
    PCIe/CXL, AI accelerator connectivity
3)  CSS E1; includes only on-chip SRAM
4)  CSS N3; limited to 4 cores and no die-to-die connectivity

**Answer:** B

**Feedback:**  
- *Correct (B):* CSS V3 is optimized for AI/HPC, with extensive memory
and I/O bandwidth for scaling out.  
- *Incorrect (A):* CSS N2 supports modern memory; DDR3 is obsolete.  
- *Incorrect (C):* CSS E1 is not for AI/HPC at scale.  
- *Incorrect (D):* CSS N3 supports up to 32 cores and includes
die-to-die links.  
- *Section:* 5.6 Neoverse Compute Subsystems



