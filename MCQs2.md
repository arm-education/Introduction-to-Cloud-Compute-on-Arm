# Part 2

## The Software Stack — Questions

------------------------------------------------------------------------

### 1. A Neoverse-based cloud platform is designed to support both Linux and Windows guests, plus live migration of workloads between hosts. Which firmware abstraction mechanism should its platform software stack *prefer*, and why?

1)  Device Tree, for rich embedded hardware description
2)  ACPI, as it is broadly supported for abstracting hardware and
    essential for cross-OS live migration in data centers
3)  No abstraction, hardcode all drivers
4)  Only ARM Trusted Firmware

**Answer:** B

**Feedback:**  
- *Correct (B):* ACPI is preferred in cloud/datacenter and supports
broad OS compatibility and hot-plug/migration.  
- *Incorrect (A):* Device Tree is mostly used for embedded, not data
center/cloud environments.  
- *Incorrect (C):* Hardcoding drivers is brittle and not portable.  
- *Incorrect (D):* ARM Trusted Firmware handles boot/secure firmware,
not hardware abstraction for OSes.  
- *Section:* 5. Device and Platform Discovery

------------------------------------------------------------------------

### 2. Why must a developer targeting Neoverse systems avoid writing device drivers that make hard assumptions about cache, interrupt, or memory controller characteristics, even when developing against a Reference Design?

1)  All Neoverse implementations are identical
2)  The licensee’s choices and manufacturing process can create
    significant differences in microarchitectural features
3)  Reference Design drivers are never used
4)  Linux kernel hides all hardware differences

**Answer:** B

**Feedback:**  
- *Correct (B):* Implementer choices mean caches, interconnects, etc.
may vary, so drivers must interrogate hardware rather than assume
specifics.  
- *Incorrect (A):* Neoverse implementations vary widely.  
- *Incorrect (C):* Reference Design drivers are a common starting
point.  
- *Incorrect (D):* Some hardware specifics must be handled in the
driver.  
- *Section:* 1.2 Example Platform; 5. Device and Platform Discovery

------------------------------------------------------------------------

### 3. A developer is using a Fixed Virtual Platform (FVP) for Neoverse N2. What is a key limitation of FVP for performance evaluation and code optimization, and how should developers adjust their workflow?

1)  FVP executes faster than real hardware, so it’s ideal for
    performance tuning
2)  FVPs are highly accurate in functional behavior, but orders of
    magnitude slower, making them unsuitable for precise benchmarking or
    microarchitectural optimization
3)  FVPs do not support boot firmware
4)  FVP cannot simulate interrupts

**Answer:** B

**Feedback:**  
- *Correct (B):* FVP is for functional verification, not performance
tuning; use silicon or cycle-accurate models for true optimization.  
- *Incorrect (A):* FVPs are much slower than hardware, not faster.  
- *Incorrect (C):* FVPs do support boot firmware.  
- *Incorrect (D):* Interrupt simulation is supported.  
- *Section:* 1.2 Example Platform

------------------------------------------------------------------------

### 4. In the context of Confidential Compute Architecture (CCA) and RME, which software component is *most trusted* and has the smallest attack surface in the system?

1)  Operating system kernel
2)  Hypervisor
3)  Secure Runtime Services/Root state firmware
4)  Application code running in Realm state

**Answer:** C

**Feedback:**  
- *Correct (C):* Minimal Secure Runtime Services in Root/Secure state
can be verified and form the system’s trust anchor; OS and hypervisor
are deliberately untrusted.  
- *Incorrect (A):* The OS is large, complex, and untrusted in modern
threat models.  
- *Incorrect (B):* The hypervisor is too complex to be fully trusted.  
- *Incorrect (D):* Realm state code is isolated but not foundational to
trust.  
- *Section:* 2. Security Considerations

------------------------------------------------------------------------

### 5. Which property of the Neoverse boot sequence ensures the “chain of trust” from hardware power-on to OS launch, and what could break this chain?

1)  Only runtime kernel verification
2)  Each boot stage validates the next using immutable,
    device-provisioned keys; a compromise at any stage (e.g., insecure
    key storage) can break the chain
3)  Boot stages can be loaded without verification if speed is needed
4)  Only the first boot stage is checked

**Answer:** B

**Feedback:**  
- *Correct (B):* Each step’s validation is crucial; failure to validate
or insecure keys can compromise the whole system.  
- *Incorrect (A):* Relying solely on runtime kernel verification is
insufficient for full system integrity.  
- *Incorrect (C):* Unverified loading breaks trust.  
- *Incorrect (D):* All boot stages must be validated for end-to-end
trust.  
- *Section:* 4. The Boot Sequence

### 6. In a typical Neoverse software stack, which interaction between SCP, MCP, and AP could lead to subtle bugs if platform firmware is not implemented correctly, particularly in hot-plug or power management events?

1)  Only the AP is responsible for all power sequencing
2)  SCP/MCP handle power and management—race conditions or
    miscommunication between these and the AP can cause inconsistent
    core or peripheral states
3)  All firmware runs in EL0
4)  None; hot-plug is always fully hardware managed

**Answer:** B

**Feedback:**  
- *Correct (B):* Bugs can result if SCP/MCP/AP lose sync on power or
state transitions, as each manages part of the system.  
- *Incorrect (A):* Power sequencing is a collaborative process.  
- *Incorrect (C):* Management and firmware often run in higher exception
levels.  
- *Incorrect (D):* Firmware plays a key role in managing hardware
events.  
- *Section:* 3. A Typical Software Stack

------------------------------------------------------------------------

### 7. A developer wishes to maximize deterministic low-latency interrupt handling on Neoverse. Which SoC component and configuration would most likely introduce unexpected latency, and what is a mitigation?

1)  Using the GIC-700 with virtualization and large numbers of vCPUs,
    which can add indirection/latency—mitigate by partitioning interrupt
    affinity and tuning GIC settings
2)  Only using local timers
3)  Avoiding MMU
4)  Using Device Tree instead of ACPI

**Answer:** A

**Feedback:**  
- *Correct (A):* Virtualized interrupt distribution can add variable
delay; affinity/priority tuning is needed for low-latency paths.  
- *Incorrect (B):* Local timers avoid system-wide interrupts but are not
a solution for all interrupt latency.  
- *Incorrect (C):* MMU usage does not directly address interrupt
latency.  
- *Incorrect (D):* Hardware abstraction method does not control
interrupt latency.  
- *Section:* 10.1 Generic Interrupt Controller (GIC–700)

------------------------------------------------------------------------

### 8. Given Arm’s broad OS and middleware support, what is a subtle but critical risk when porting an x86 application making heavy use of SIMD (e.g., AVX, SSE) to Neoverse with SVE/SVE2?

1)  All x86 SIMD intrinsics are directly supported
2)  Intrinsics are not binary compatible; manual refactoring and use of
    SVE/SVE2-optimized libraries or compiler auto-vectorization is
    required for correct and performant code
3)  Only cryptographic routines are affected
4)  There is no difference

**Answer:** B

**Feedback:**  
- *Correct (B):* SIMD code must be refactored or recompiled; direct
mapping is not possible between x86 and Arm SIMD extensions.  
- *Incorrect (A):* Intrinsics are architecture-specific and require
porting.  
- *Incorrect (C):* All SIMD code, not just cryptography, is affected.  
- *Incorrect (D):* There are substantial differences between SIMD
ISAs.  
- *Section:* 9. Applications; Correlation with x86 Features

------------------------------------------------------------------------

### 9. For cloud-native, reproducible CI/CD workflows on Neoverse, what specific architectural property of Arm cloud instances enables *bitwise identical* software deployments across dev/test/prod, and why is this sometimes harder on x86?

1)  All Arm instances run proprietary kernels
2)  The standardized SystemReady hardware/firmware and ACPI/UEFI
    interface ensure a consistent software environment; x86 instances
    may differ in firmware or virtualization behavior
3)  Arm always runs slower, allowing time for verification
4)  Only the hardware, not software, matters

**Answer:** B

**Feedback:**  
- *Correct (B):* Arm’s certification programs and cross-cloud
standardization reduce variation, a key benefit for DevOps.  
- *Incorrect (A):* Most Arm cloud instances run standard kernels.  
- *Incorrect (C):* Speed is unrelated to reproducibility.  
- *Incorrect (D):* The software stack must be stable and uniform for
true reproducibility.  
- *Section:* 8. Cloud–Native Tooling

------------------------------------------------------------------------

### 10. In what scenario might the weakly ordered memory model of Arm result in a subtle application bug *even if code works on x86*, and what specific code-level change addresses it?

1)  Unused variables in C
2)  Multi-threaded code with shared variables lacking explicit memory
    barriers; add C11/C++11 atomics or appropriate barriers
3)  Static linking
4)  All bugs are compiler bugs

**Answer:** B

**Feedback:**  
- *Correct (B):* x86’s stronger ordering can hide concurrency bugs; on
Arm, atomic or volatile constructs and barriers are critical.  
- *Incorrect (A):* This is unrelated to memory models.  
- *Incorrect (C):* Linking format does not affect concurrency
ordering.  
- *Incorrect (D):* Memory model bugs are not compiler issues—they’re
architectural.  
- *Section:* 9. Applications — Memory Model


