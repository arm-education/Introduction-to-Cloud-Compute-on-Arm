# Part 1—Introduction to Neoverse Cores 

# 1. Introduction

## 1.1 Purpose

The purpose of this resource is to introduce the Arm<sup>®</sup>
Neoverse™ range of processors for developers who wish to write software
for devices powered by Neoverse cores. Additionally, the material will
be of some use to those wishing to design and manufacture those devices,
but it doesn’t contain detailed discussion of semiconductor design
beyond the high-level understanding of architecture that is beneficial
to software developers.

Readers should gain an appreciation of the purpose and reasoning behind
major features of the Armv9 architecture and of the range of Neoverse
processors. This is intended to enable readers to make informed choices
when selecting a target platform for a particular use case, including
tool selection and software development methodology. This can also serve
as a resource for those looking to learn or teach about server
computing.

## 1.2  Scope

This text covers an introduction to the Neoverse range of processor
cores, a taxonomy of the devices currently available, major producers
and users of those devices, and tools available for developing software
for them. Although the book contains an evolutionary history of the Arm
architecture and product range, this is not primarily a history book.
Only historic features that have a bearing on current architectures will
be discussed in any detail.

## 1.3  Audience

The primary audience for this resource is software developers or those
looking to learn or teach about server computing. Much of the material
will be of interest to semiconductor designers, system integrators and
electronic engineers. However, they don’t represent the target audience
and will need to refer to further and more detailed texts to find the
knowledge they require.

## 1.4  Summary

Beginning with an introduction to Arm, its history and current market
positioning, we then outline the development of the Arm architecture
from its earliest incarnations to the latest Armv9 architecture. The
rest of the book concentrates on the range of processors that are
produced under the Neoverse brand. The approach taken is primarily
driven by the needs of software developers.

## 1.5  Currency

While all information presented is correct at time of publication—as far
as the authors can ensure—readers must bear in mind that the
semiconductor industry, including Arm, develops at an astonishing and
accelerating pace. New architectures and new devices are released
regularly, enabling new use cases and unlocking new target markets. The
reader is advised to refer to external sources for the latest
developments.

## 1.6  References and Related Reading

- Arm Architecture Reference Manual for A-profile Architecture (ARM DDI
0487K)

- Arm<sup>®</sup> Neoverse™ V3 Core Software Optimization Guide
(PJDOC–1505342170–661452)

- Arm<sup>®</sup> Neoverse™ V2 Core Technical Reference Manual (Arm
102375_0002_03_en)

- Arm<sup>®</sup> Neoverse™ N3 Core Software Optimization Guide (Arm 109637)

- Arm<sup>®</sup> Neoverse™ V2 Core Software Optimization Guide
(PJDOC–466751330–593177)

- Arm<sup>®</sup> Cortex™–A Series Programmer’s Guide (ARM DEN0013D,
4<sup>th</sup> Edition)

- Arm<sup>®</sup> Neoverse™ N2 Reference Design Technical Overview (Arm
102337_0000_04_en)

- Arm<sup>®</sup> CoreLink™ GIC–700 Generic Interrupt Controller Technical
Reference Manual, Document ID 101516_0400_12_en

- Arm<sup>®</sup> CoreLink™ MMU–700 System Memory Management Unit
Technical Reference Manual, Document ID 101542_0001_04_en

- Arm<sup>®</sup> CoreLink™ NI–700 Network‐on‐Chip Interconnect Technical
Reference Manual, Document ID: 101566_0203_10_en

- Arm<sup>®</sup> CoreLink™ CMN–700 Technical Reference Manual, Document
ID: 102308_0302_07_en

- Arm<sup>®</sup> CoreLink™ NIC–450 Network Interface Connect Technical
Overview, Document ID: 100459_0000_01_en

- Arm<sup>®</sup> DynamIQ™ Shared Unit Technical Reference Manual,
Document ID: 102547_0201_07_en

## 1.7  Glossary

A full Arm glossary can be found on Arm’s website, Document ID
105565_0200_02_en.

# 2.  Introduction to Arm

Arm<sup>®</sup> processors are found everywhere. A couple of decades
ago, the Arm ecosystem passed the milestone of producing more processors
than there are human beings on planet Earth. At the time of writing, the
numbers are truly staggering: in excess of 7 billion devices are shipped
every quarter; a cumulative total of over 300 billion devices have been
shipped since the foundation of the company in 1990; Arm has a 50% share
of all electronic devices with processors; and in excess of 90% of
smartphones use Arm microprocessors.

Arm, of course, does not achieve this on its own. Rather, it functions
as the driving force behind a huge and growing ecosystem of partner
organizations. At the heart of this partnership, Arm designs the
processors themselves, constantly pushing for higher performance, wider
scalability and flexibility, and greater power efficiency. It is this
last attribute—power efficiency—on which Arm first made its reputation.

The meteoric growth of mobile phones through the late 1990s and early
2000s was powered by the adoption of Arm processors by almost every
major manufacturer of the era. Arm’s compelling combination of
flexibility, processing power, and power efficiency made their
processors the natural choice across the industry.

With the emergence of smartphones in around 2008, Arm again caught a
rising wave of innovation and growth in the electronics industry. With
very few exceptions, all the early smartphones, MP3 players, and tablets
were based on Arm designs. Other businesses in the industry quickly
found they could rely on Arm to produce better, faster, cheaper, and
more power-efficient designs, year on year. They could then focus on
their own product development. Arm became the processor outsourcing
house for almost everyone in embedded electronics.

There were many other advantages to the growing breadth of the Arm
ecosystem. A growing pool of engineers knew, loved, and used Arm
architecture—an industry-wide ecosystem of talent, that brought
economies of scale in education, tooling, and component sharing. This
reduced costs and increased opportunities for all.

As well as the relentless drive for ever-greater power efficiency and
scalability, Arm has worked to broaden the ecosystem in every direction.
The initial markets in the deeply embedded space, centered around mobile
phones, are still hugely significant to Arm’s activities, but these have
been joined by other market segment such as automotive, machine learning
and artificial intelligence.

As you shall see later when looking at the evolution of the Arm
architecture and product range, new markets very often require new
priorities for computing. The needs of a smartphone product designer are
very different from the needs of an automotive engine controller, and
from the needs of a server-class processor in a data center. Each use
case has its own balance between cost, volume, processing capability,
power efficiency, ease of manufacture, security, reliability,
throughput, and other factors. These are some of the considerations
which drive the choice of an appropriate platform for any new product.

For further information about Arm, please check the [<u>Arm
website</u>](https://www.arm.com/resources/education).

# 3.  Development of the Arm Architecture

This chapter covers the evolution of the Arm<sup>®</sup> architecture
from its earliest days through to the introduction of the Armv9
architecture. Armv9—the architecture implemented in Neoverse™
products—is the subject of the subsequent chapter, so if the history is
of little interest to you, you may wish to skip straight there.

The history of the development of the Arm architecture and the
accompanying range of products is, in many ways, a history of the
development of electronic (specifically computing) engineering across
the last forty years.

At this point though, you must note the difference between
“architecture” and “processor”.

The “architecture” is the contract between software and hardware. It
defines how the hardware behaves when processing sequences of
instructions, how it handles exceptions and error conditions, how it
interfaces with memory, how caches behave, and so on. A new version of
the architecture might introduce new instructions, classes of
instruction, new memory behaviors, new registers, and so on.

Processors are implementations of a particular architecture. Each
individual processor is designed to conform to a single version of the
architecture, while each architecture might be implemented in many
separate processors. So, while two processors might conform to the same
architecture, and thus be “binary-compatible”, they may differ
considerably in the way in which that functionality is implemented, the
trade-offs chosen between power consumption and compute power, the
available physical memory size, cache configuration, and bus
interconnect architecture, among many, many other possible variations in
the physical construction of the device itself.

You should keep aware of this fundamental distinction between
architecture and implementation when dealing with Arm-based compute
devices.

## 3.1  Early Days

The first Arm processor was developed by Acorn Computers—a British
manufacturer of personal computers, founded in Cambridge in 1978 by
graduates from Cambridge University. In the 1980s, Acorn enjoyed
considerable success in the U.K. education market after being adopted as
the chosen machine for a nationwide computer literacy project sponsored
by the British Broadcasting Corporation (BBC). The eponymous BBC Micro
sold over 1.5 million units in its 13-year lifetime. The machine was
based on the 6502 processor from MOS Technology, and by 1984 it became
clear that a new processor was needed for subsequent products.

The Acorn design team evaluated a number of contemporary processors
before concluding that none were suitable. They took the
decision—remarkable at the time—to design their own. Sophie Wilson
designed the instruction set, and Steve Furber designed the processor
hardware. The first Acorn RISC Machine ran code on 26th April 1985 at
Acorn’s office in Cambridge, United Kingdom. Its first use was as a
second processor for the BBC Micro. The first personal computer based on
it—the Acorn Archimedes—was launched in 1987.

The mid–1980s was not a successful period for Acorn, though, and the
company was largely broken up towards the end of the decade. The
intellectual property (IP) making up the Acorn RISC Machine was spun out
into a new company called Advanced RISC Machines. This was a joint
venture between Acorn (who provided the technology and a number of
staff), Apple (the first customer and supplier of seed finance), and
VLSI (who fabricated the first devices). The company set itself the
ambitious mission of becoming the “global processor standard”. For its
flotation on the London Stock Exchange in 1999, it renamed itself as
“Arm”.[^1]

Apple invested in Arm in order to gain access to the processor for its
Apple Newton PDA. While this product was not successful in the
marketplace, it was an important milestone for Arm as a separate company
with its own destiny independent of Acorn.

Arm realized that it couldn’t compete with existing, established
semiconductor manufacturers, and instead quickly formulated its own
strategy of licensing the IP for its designs to partner companies, which
produced chips based around the processors. Early licensees included
Sanyo, Sharp, Texas Instruments, and Plessey.

The early Arm processors—Arm2 through Arm6—were moderately successful.
But when Texas Instruments adopted the Arm7TDMI<sup>®</sup> processor
for production of a System-on-Chip to be used in Nokia’s mobile phones,
it catapulted Arm to the forefront of the industry, a position which it
has occupied ever since.

## 3.2  Rapid Evolution

Acorn Computers bequeathed the Arm3 processor to Advanced RISC Machines,
when it was founded in 1990. This processor was far simpler and smaller
than the contemporary 80286 and 80386 processors in most desktops, with
a much lower transistor count. However, it also offered higher
performance and was able to do this at lower power consumption.[^2]

Early work culminated in the Arm610, which was used by Apple in 1992 for
their Newton PDA, and in 1994 by Acorn in their RiscPC desktop machine.
In 1993, Arm made a profit for the first time.

A steady trickle of licensees followed, including Samsung, Texas
Instruments, Plessey, and Sony. The Arm7TDMI, however, released in 1994,
was Arm’s first major success. It embodied several key innovations,
which established Arm’s products in the marketplace. In the name, ‘D’
and ‘I’ indicate on-chip debug capabilities that made it possible to
debug a core embedded within a silicon chip, without needing access to
the internal bus connections. This allowed developers to debug without
an external emulator. The ‘M’ indicates a fast multiplier circuit
(earlier versions did not have dedicated hardware for multiplication, so
this represented a significant additional capability). The ‘T’ indicates
that the device supports the Thumb<sup>®</sup> instruction set.

The Thumb instruction set is the most significant early development in
the Arm architecture, and it is worth examining it a little more
closely. While capable of very high performance and power efficiency,
earlier Arm processors suffered in deeply embedded use cases due to
their need for a 32-bit data bus, which was expensive and complicated to
integrate in small, low-cost devices where 16-bit buses and 16-bit
memory devices are a significant advantage. Since all Arm instructions
are 32 bits long, instruction fetches operate at half speed in a 16-bit
memory system, which seriously decreases performance. In addition, code
density is relatively poor due to the large size of instructions.

Arm’s solution was to devise a subset of the instruction set, re-coded
in 16-bit instructions. To simplify the implementation, there was no
separate Thumb decoder; instead, Thumb instructions were translated to
equivalent Arm instructions, which were then executed by the original
Arm decoder and execution unit. The Thumb decompression stage occupied a
previously unused half cycle in the pipeline, so it had no direct impact
on instruction throughput. Benchmarks showed that the Thumb instruction
set gave a 35% improvement in code density and performance in 16-bit
memory—close to Arm instructions in 32-bit memory.

The Arm7TDMI was licensed by Texas Instruments to be incorporated into
the first single-chip mobile phone solution. This was provided to Nokia,
and first appeared in the Nokia 6110. Within a very short period, Arm
captured over 98% of the mobile phone market. In 2009, the Arm7TDMI was
still one of the most widely-used Arm cores—a testament to its
versatility, cost–effectiveness, and high efficiency. More importantly,
it provided Arm with a platform for explosive growth across many other
markets.

The Arm9™ processor family, introduced in 1998, marked a significant
implementation decision to move to a Harvard bus architecture, with
completely separate data and instruction memory systems. The resulting
increase in memory bandwidth allows for a higher performance pipeline
and greater throughput. Through its lifetime, the Arm9 family introduced
extended instructions for Digital Signal Processing (DSP) applications,
Java acceleration, and floating-point capability. It was the first
family of Arm cores that were delivered to licensees as fully
synthesizable Hardware Description Language (HDL). This allowed the
licensee much greater freedom in configuring and implementing the core,
for a wider variety of use cases. Earlier cores were delivered as GDSII
files, targeted to a specific fabrication process, meaning that every
core needed to be manually re-synthesized by Arm for each target
process.

Arm9 processors were the first to be designed specifically to execute
code and fetch data from caches, and their execution pipelines reflect
this choice. Some variants (notably the ARM966), however, were optimized
for hard real-time use cases (such as machinery control and hard disk
drive software) in which predictability of execution time sometimes
takes preference over raw speed. These cores use Tightly Coupled Memory
(TCM), SRAM, which is connected directly to the core and is accessible
with no wait states.

Some Arm9 processors (e.g. ARM926) employ both caches and TCM for
flexibility.

During this period, Arm made a significant change to its technology
licensing model. Traditionally, and this is still largely the case,
Arm’s licensees pay for the right to create silicon devices based on a
specific Arm core, or family of Arm cores. They take the HDL source from
Arm, configure it as required, add their own proprietary components, and
then fabricate the end product using their preferred manufacturing
process.

An Arm “architecture license”, however, takes this one step further.
Here, the licensee purchases the right to build devices based on a
particular architecture, but without using Arm’s source code as the
intermediate step. Such licensees implement the core entirely
independently, often using their own proprietary design processes and
tools. This allows them to offer greater differentiation, compared to
completing products. However, this requires large design teams and
greater design costs.

The first such licensee was Digital, who, in 1995, bought a license to
the Armv4 architecture and developed the StrongArm range of processors.
Using Digital’s own in-house tooling and design rules, these processors
were, for some time, the fastest and most power efficient Arm-compatible
processors on the market. Exploiting the freedom offered by the
architecture license, Digital’s design team were able to make many
custom enhancements to the microarchitecture of the processor to
increase its speed. For instance, the StrongArm–110 included a dedicated
circuit to compute the destination for branch instructions. At the
expense of some extra gates, this reduced the branch latency by one
cycle (contemporary Arm implementations re-used the addition circuits in
the ALU to do this computation, taking an extra cycle to do so). The
technology eventually passed to Intel in 1997, where it became XScale,
and eventually to Marvell in 2006.

Arm10 followed, with wider 64-bit buses and more sophisticated cache
architecture.

Arm11™ again included several significant innovations, which drove the
next phase of growth: a third instruction set, Thumb–2, was designed to
provide the advantages of 16-bit Thumb and 32-bit Arm in a single
encoding; multicore capability was added with cache snooping to support
up to four cores in a single cluster; and the TrustZone<sup>®</sup>
security architecture addressed the growing need for greater security at
the hardware level.

## 3.3  Diversification

In the early 2000s, it became obvious that a single architecture could
no longer cope with the enormous breadth of use cases for Arm
processors. For example, the processor requirements of a deeply embedded
microcontroller are very different from those of a smart television. In
response, Arm introduced Armv7™—a set of “architecture profiles”. While
all based on a common source architecture, these profiles enabled
significantly different products across a wide range of price and
performance points. These profiles are all marketed under the
Arm<sup>®</sup> Cortex<sup>®</sup> brand.

As well as the different capabilities offered by the architecture
profiling, implementations can vary widely. Licensees make these choices
during the synthesis and integration process based on factors such as
functional safety, multicore requirements, security, DSP and Multimedia
capability, cryptography, and compartmentalization.

### 3.3.1  Cortex–A for Application Class Processors

Cortex–A comprises implementations of the Armv7–A, Armv8–A and Armv9–A
architecture profiles. These remain the pinnacle of performance and
capability in the Arm product range. Key features include
high-performance processor cores with sophisticated branch prediction,
complex and efficient cache architectures, highly-optimized capability
for DSP, machine learning (ML) and artificial intelligence (AI)
applications. Some of these cores are marketed under the Cortex–X brand,
indicating that they prioritize performance over other considerations,
such as silicon area and power consumption.

Cortex–A cores are designed to execute code and fetch data from cached
memory systems. The structure of their execution pipelines reflects this
choice. In most cases, caching behavior is prescribed in the
architecture, while cache size is a choice the licensee makes during
implementation.

Armv8–A introduced a 64-bit operating state for the processor,
supporting a completely new, 64-bit instruction set known as A64. It
introduced a new exception model, and new operating modes aimed at
supporting multiple simultaneous applications, operating systems and
hypervisors.

All Cortex–A cores have the option to support at least two instruction
sets: Arm (an evolution of the original Arm instruction set); Thumb–2;
and, since Armv8, A64.

Although they are optional features in the architecture, the Neon™
extension (for Multimedia and DSP) and VFP extension (for vector
floating point) are key features of Cortex–A cores. Armv8 introduced a
further set of extensions to accelerate cryptography.

Armv8.2–A introduced Simultaneous Multi-Threading (SMT), which was first
implemented in the Neoverse™ E1. It also introduced the Scalable Vector
Extension (SVE), which was specifically developed for variable-length
vectorization of high-performance workloads.

Armv8.3–A provided a number of enhancements, including pointer
authentication and complex number capability.

Armv8.5–A became the baseline for Armv9–A, introducing Memory Tagging
Extension (MTE) and Branch Target Indicators (BTI) to combat illegal
memory accesses and arbitrary code execution.

### 3.3.2  Cortex–R for Hard Real-Time Processors

The ‘R’ profile architectures are specifically targeted at applications
needing hard real-time response. Modifications to the pipeline,
exception model, and memory system are aimed at predictable and fast
responses to exceptions, and deterministic instruction throughput. They
may also implement hardware division.

These cores are found in applications such as machine controllers,
automotive management, and high-speed modems.

From Armv8–R, these processors have the option of supporting the A64
64-bit instruction set.

### 3.3.3  Cortex–M for Microcontrollers

The M profile is significantly different from the other two profiles and
is aimed specifically at deeply embedded microcontrollers. These cores
implement only the Thumb–2 instruction set, are programmable entirely in
high-level languages such as C and C++, and deploy a significantly
different exception model based on existing microcontroller
architectures.

Since Armv8–M, Cortex–M has optional support for a security architecture
known as TrustZone for Armv8–M security architecture. Although the brand
name is similar, the implementation is significantly different to the
TrustZone security architecture found on A and R profile cores. It also
supports the Helium vector processing instruction set extension.

## 3.4  Current Drivers of Architectural Change

The latest Arm architectures are driven, as ever, by the changing and
evolving needs of the electronics industry. While the mobile phone
sector is still clearly important to Arm, in recent years, there has
been significant application in other markets, including networking,
data center, automotive, and safety-critical devices.

While performance and power efficiency are still highly important, there
is an increasing need for better and more robust security, specific
requirements for safety-critical devices, and very high-performance data
center and networking use cases. The majority of current innovation in
the architecture is focused on the A–profile cores, aiming to provide
the highest possible performance, particularly for data center, machine
learning, and artificial intelligence workloads.

## 3.5  Other Products and Activities

Like any processor architecture, developing a product requires more than
just manufacturing or buying the processor device itself. Development
tooling, source management, operating systems, middleware, and firmware
must either be developed in-house, or sourced from Arm or third parties.

From the earliest days, Arm has produced standard tools solutions that
are either sold commercially or made available via contributions to Free
and Open-Source Software (FOSS) projects. At the beginning, Arm was the
only source of its architecture devices, so it needed also to produce
and sell its own range of tools (compiler, assembler, linker, librarian,
debugger, etc.) as no other supplier was available.

Texas Instruments—one of the first licensees—wrote its own tooling
solutions. But an increasing number of third-party suppliers partnered
with Arm to produce competitive alternatives. Arm’s own tools are still
available and are valuable to licensees as the first to support new
architectures.

The tooling situation for cloud-based development is necessarily
different and will be explained in detail in subsequent chapters.

# 4.  Armv9 Overview

Armv9 represents the current state-of-the-art Arm architecture for
high–performance computing applications. It has been announced in
increments, starting with Armv9.0–A in 2021. At the time of print, the
latest version is Armv9.6–A, which was announced in 2024. Armv9 aims to
address the needs of High-Performance Compute (HPC), cloud computing,
hardware acceleration for machine learning and other artificial
intelligence tasks, high data throughput computing, networking, and
Confidential Computing.

Each version contains a combination of mandatory and optional features.
Some features, while optional, may only be implemented in combination
with specific subsets of other features. Features that are optional in
one version of the architecture may become mandatory in later versions.

All versions are incremental—each version includes the mandatory
features of all prior versions.[^3] Meanwhile, Armv8–A has continued to
develop in parallel with Armv9–A. They are closely linked, and the
features implemented at each iteration are typically very similar.

In the descriptions that follow, only limited detail is provided for any
features that are only of interest to silicon designers or are not
exposed directly to software developers other than through defined
tooling interfaces or firmware.

In all cases, further detail is in the Arm Architecture Reference
Manual, though be aware that this document is written for silicon
developers and architects and is of limited use for software developers
due to the level of detail which it necessarily includes.

Before any detailed look at Armv9–A, it is important to understand some
fundamental concepts and terminology regarding the structure and
taxonomy of the architecture. §4.1 below provides a brief introduction
to exceptions, operating modes and states, instruction sets, and
security states and should be read before continuing.

## 4.1  Exceptions, Modes, States and Instruction Sets

Some level of awareness of the internals of the Arm architecture is
necessary for any meaningful discussion about Arm processors. This
section provides a very brief overview of some key terms and concepts.
As ever, more detailed information is available on the Arm website for
those with a deeper curiosity.

The discussion that follows does not attempt to address the 26-bit
modes, which are of only historical interest, nor the Armv7–M
architecture supported by the Cortex–M microcontrollers, which is
significantly different.

### 4.1.1  Exceptions and Operating Modes

In the Arm architecture, exceptions and operating modes are closely
linked. In architecture Armv7—and all earlier versions of the
architecture—each exception type is handled using a specific operating
mode. These modes have separate exception vectors and a private subset
of the main register set. This simplifies the nesting of exceptions of
different types and reduces the amount of context an exception handler
needs to save on entry and restore on exit.

Some exceptions are linked to external interrupts—for example, IRQ is
the standard external hardware interrupt, and FIQ is an external
hardware interrupt of higher priority. Some exceptions are linked to
error conditions, such as memory access aborts. Other exceptions are
linked to software interrupts caused by execution of an exception
instruction, such as SWI.

Armv7 supports a number of operating modes. Except for User mode, these
are all “privileged”, meaning that they have access to system resources
that have been protected from unprivileged access. To provide a degree
of protection, the privileged modes are generally reserved for the
operating system. The Armv7 modes are:

- FIQ, entered on detection of an FIQ hardware interrupt

- IRQ, entered on detection of an IRQ hardware interrupt

- Abort, entered on detection of a data memory access abort

- System, a privileged mode that is not entered via an exception

- SVC, entered on reset and on execution of a Software Interrupt (SWI)
instruction

- User, the only unprivileged mode, used to execute user code

When in a privileged mode, software can freely switch modes by directly
modifying the Current Program Status Register (CPSR). When in User mode,
a mode change can only be caused by an exception.

At first glance, System mode may seem anomalous since it is a privileged
mode, but it is not entered via an exception. System mode was a
relatively late addition to the Arm architecture, introduced to simplify
some issues which can occur when nesting exceptions.

Armv9–A adds another layer to this, with four “exception levels”—or EL,
listed here in increasing order of privilege:

- EL0, the lowest level of privilege, usually used for execution of user
applications

- EL1, typically used for execution of a rich operating system, such as
Linux

- EL2, which can be used for hypervisors

- EL3, the highest level of privilege, typically reserved for firmware and
security gateway code

A typical usage model for these exception levels is shown in Figure 1.

<img src="./media/image1.png" style="width:5.75in;height:3.98958in" />

Figure 1 – Exception levels

Movement between ELs occurs when taking, or returning from, an
exception. The general rule is that on taking an exception, the EL can
only stay the same or go up; on returning from an exception, it can only
stay the same or go down.[^4]

Note that the architecture defines these four ELs but does not mandate
the use of each level. The model in Figure 1 is, however, common and
typical. Also, while support of EL0 and EL1 is mandatory in any
implementation, EL2 and EL3 are optional. In practice, these levels are
usually implemented, since EL2 supports the virtualization features
required by most hypervisors, and EL3 is the only EL which can change
security state.

### 4.1.2  Execution States and Instruction Sets

Armv8–A and Armv9–A processors support two execution states: AArch32, a
32-bit execution state; and AArch64, a 64-bit execution state. In
general, the execution state defines the width of the general–purpose
register set, and also the available instruction sets.

In Armv8–A, either or both execution states may be supported at each
exception level. Armv9 –A requires that AArch64 is supported at all ELs,
while AArch32 may be optionally supported only at EL0.

Execution state can only change when the exception level changes, and,
in a similar fashion to exception levels, the architecture requires that
when moving to a higher EL, the execution state may either stay the same
or change to AArch64. On moving to a lower EL, it can either stay the
same or change to AArch64. The rules on changing exception level and
execution state have a number of implications:

- If AArch32 is not implemented at a particular EL, then it cannot be
implemented at any higher levels.

- AArch32 software at any particular EL can only host AArch32 software at
any lower levels.

- An AArch64 operating system executing at EL1 can host both AArch32 and
AArch64 software executing at EL0.

- An AArch64 hypervisor executing at EL2 can host both AArch32 and AArch64
software executing at EL1.

<img src="./media/image2.png" style="width:6.26806in;height:1.62847in"
alt="A close-up of a screen Description automatically generated" />

Figure 2– Exception levels and Execution States

In AArch32:

- Operation is backwards-compatible with Armv7–A and previous
architectures.

- The A32 and T32 instruction sets are available.[^5]

- The 32–bit Armv7–A register set is supported.

In AArch64:

- Only the A64 instruction set is available.

- The general-purpose register set is expanded, both in width and in
number, compared to Armv7–A and earlier architectures.

A32 is the direct descendant of the original instruction set used by the
earliest Arm processors. In A32, all instructions are 32 bits wide and
are aligned on 32-bit address boundaries in memory.

T32 evolved from the Thumb instruction set introduced in the
Arm7TDMI<sup>®</sup> (architecture Armv4T). For more detail on the
origins of the Thumb instruction set, see §3.2 above. In the original
Thumb instruction set, all instructions are 16 bits wide and are aligned
on even address boundaries. These instructions form a 16-bit encoded
subset of the Arm instruction set, and each instruction has a direct Arm
equivalent.[^6]

The original Thumb instruction set was significantly expanded, initially
in the Arm1156–T2 processor, by addition of some 32-bit instructions,
yielding a mixed-length instruction set originally known as Thumb–2.
This instruction set has evolved into what is now called T32.

A64 is an entirely new instruction set introduced in Armv8–A, and
carried forward into Armv9–A.

Within AArch32 state, the A32 and T32 instruction sets each have an
associated “state”—Arm state for A32, and Thumb state for T32. These are
indicated by the value of the T bit within the CPSR. A change of state
can only be caused by a branch or return instruction, or on entry to, or
return from, an exception.

### 4.1.3  Security States

Most Cortex–A processors support two security states: Secure and
Non-Secure.[^7] Certain processor features are architecturally
classified as Secure and can only be accessed by software executing in
Secure state. Secure state information is also propagated outside the
processor into external components such as the memory interface, caches,
memory management units, and other peripherals. This allows system
designers to partition the system into sets of Secure and Non-Secure
components.

When executing in Secure state, software can access both Secure and
Non-Secure components and features; when executing in Non-Secure state,
Secure items cannot be accessed and attempts to do so will usually
result in an exception.

This architecture allows the implementation of secure subsystems within
the system. This might be, for example, a secure payment or DRM
subsystem executing in Secure state and using some secure features,
alongside an operating system such as Linux or Android, executing in
Non-Secure state. As long as the mechanism for changing security state
is strongly protected, this prevents Non-Secure software from accessing
or observing Secure software and hardware. In an Armv8–A or Armv9–A
system, the only route into Secure state is through a Secure Monitor,
which executes in EL3. An example system configuration is shown in
Figure 3.

<img src="./media/image3.png" style="width:5.75in;height:2.36458in" />

Figure 3 – Exception Levels, Security States and Execution States

Armv9–A extends the security model with the Realm Management Extension
(RME). RME adds two new Security states: Root and Realm. In Root state,
which is only available in EL3, the processor can access the entire
physical address space. In Realm state, the processor can only access
Non-Secure and “Realm” addresses. Real memory accesses are policed by a
separate piece of software called the Realm Manager. Together with
specific RME hardware features, this provides robust
compartmentalization and greatly enhances security. Figure 4 shows an
example configuration when RME is implemented.

<img src="./media/image4.png" style="width:5.75in;height:2.69792in" />

Figure 4 – RME Security States

## 4.2  Armv9.0–A

The Armv9.0–A architecture was announced in 2021, baselined on
Armv8.5–A.

The main drivers for the Armv9 architecture are increased security and
improved vector processing. The major architecture features involved
are:

- Confidential Computer Architecture (CCA)

- Transactional Memory Extension (TME)

- Scalable Vector Extensions V2 (SVE2)

CCA is a major innovation in device security, driven by the
fast-evolving needs of the industry. It was developed in collaboration
with university research partners. CCA provides a compartmentalized
architecture in which processes can execute in “realms”, which are
isolated from each other. As well as hardware support, a standard
firmware architecture is also specified. CCA is a combination of a
number of architecture extensions, including Realm Management Extension
(RME), Dynamic TrustZone<sup>®</sup> Technology, Real Management Monitor
(RMM), and standard CCA firmware.

TME provides for Hardware Transactional Memory (HTM), which allows
sequences of instructions to be executed by the processor atomically.
This greatly simplifies and enhances the execution of multi–threaded
software on systems that consist of many independent processing
elements. TME builds upon a number of architecture extensions, including
Hardware Transactional Memory (HTM) and Transactional Lock Elision
(TLE).

There are also a number of optional extensions, some of which are
entirely new to the Arm architecture, while others build upon features
from prior architecture versions. These include:

- Armv9 Cryptographic Extensions

- Embedded Trace Extension (ETE)

- Trace Buffer Extension (TBE)

- Scalable Vector Extension V2 (SVE2)

The optional SVE2 extension is an evolution of The SVE vector processing
architecture introduced in Armv8. Extensions to the earlier iteration of
SVE allow for better fine-grained Data Level Parallelism (DLP) making it
easier for compilers to vectorize key algorithms. Support is also
introduced to accelerate key algorithms employed by the widely used
Advanced Encryption Standard (AES).

## 4.3  Armv9.1–A

Armv9.1–A was announced in September 2019 and builds on both Armv9–0–A
and Armv8.6–A. All mandatory features from those two earlier
architectures are also mandatory in Armv9.1–A.

New features introduced include:

- additional floating-point matrix multiply instructions (GEMM);

- extensions to the Embedded Trace Extension introduced in Armv9.0–A; and

- Memory Partitioning and Monitoring (MPAM), which allows the system to
monitor and restrict the memory bandwidth used by individual processes,
in order to manage and mitigate the effect on performance of other
processes.

## 4.4  Armv9.2–A

Armv9.2–A, baselined on Armv8.7–A, was announced in September 2020, and
includes some minor instruction set enhancements, and an extension to
Realm Management. Main changes include:

- Root & Realm security states and physical address spaces;

- Granule Protection Check mechanism;

- enhanced PCIe hot plug;

- atomic 64–byte load/store to accelerators;

- further extensions to ETE to support Realm Management (RME);

- Scalable Matrix Extension (SME) (Optional—allows tiled storage of
vectors in registers);

- Realm Management Extension (RME) (Optional); and

- Branch–Record recording (Optional—captures execution path history).

## 4.5  Armv9.3–A

Armv9.3–A, baselined on Armv8.8–A, was announced in September 2021.
Additions include:

- Branch Recording in EL3;

- “Non–maskable” (NMI) and “less-maskable” interrupts (LMI) for NMI for
AArch64;

- memcpy and memset instructions;

- hinted conditional branches (the ability to include hints with branch
instructions, which helps the branch prediction logic by indicating that
a particular branch is consistent and is unlikely to change direction);

- Scalable Matrix Extensions v2 (Optional), which introduces the ability
to re-address two-dimensional tiles as groups of one–dimensional
vectors; and

- Memory Encryption Contexts (MEC) (Optional)—an extension to RME that
provides additional contexts for memory encryption linked to existing
realms.

## 4.6  Armv9.4–A

Armv9.4–A, baselined on Armv8.9–A, was announced in September 2022.
Additions include:

- improved security against attacks that use branch history to infer and
manipulate execution;

- VMSA enhancements including 128–bit translation tables, system
registers, and atomic 128–bit instructions (Optional);

- SME2 and SVE2.1 (Optional), which add a number of extra instructions to
SME and SVE2 to improve matrix and vector operations; and

- Guarded Control Stack (Optional)—a separate memory area for the storage
of exception returns and branch returns, protected from modification.

## 4.7  Armv9.5–A

Armv9.5–A (October 2023) introduces:

- 8–bit Floating Point (FP8) support added to SME2, SVE2 and Neon™.

## 4.8  Armv9.6–A

Armv9.6–A (October 2024) introduces:

- MPAM Domains for improved support of shared memory in multi-chiplet and
chip systems; and

- Granular Data Isolation for Confidential Compute.

# 5.  The Neoverse Cores

So far, you have read about the development of two distinct threads in
the Arm<sup>®</sup> product range. Firstly, the evolution of the
architecture—the contract between hardware and software that defines the
behavior of devices compatible with Arm architecture. Secondly, the
implementation of a growing range of processor cores based on each
variant of the architecture. These two factors, independent yet related,
are important when understanding the rationale behind each Arm device.

The architecture of a particular device does not dictate what it will be
used for. For example, not all Cortex–A devices are used in mobile
phones, although a great number are. Similarly, not all Armv9–A
processors are used in infrastructure applications, though many of them
are very suitable for this. It is the combination of architecture and
implementation that determines whether it is suitable for a particular
use case.

The Neoverse devices conform to a mixture of architectures. Early cores
were built to Armv8–A, and later cores to Armv9–A, but every
implementation choice was made deliberately to make them suitable for
use in infrastructure applications.

Each Neoverse™ device is different. These differences arise partly from
the architecture, but also from choices made by whoever implements the
device, and the particular manufacturing process used in their
production. Understanding this is important when evaluating or selecting
a device.

It is also important to understand this when reading, in the next
chapter, the list of currently available Neoverse devices. They are
wonderfully diverse, and this diversity is one of the strengths of the
Arm product family.

## 5.1  Architecture, Implementation and Manufacturing

Much of the base functionality of a particular device is defined in the
architecture. While some of it may be optional, it is essentially
immutable. Other behavior is determined by whoever implements or
manufactures the device, and they have significant freedom here.

Some sources make the distinction between architectural,
microarchitectural, and implementational behavior.

### 5.1.1  Architecturally-Defined Behavior

In the preceding sections, you have looked at some of the behaviors that
are mandated by the architecture itself. The consistency across the
product range, enforced by the requirements of the architecture, has
been a key factor in the success of the Arm architecture in the
marketplace. In essence, as you have already seen, the architecture
defines the behavior of the hardware when the hardware is presented with
an instruction or a stream of instructions. The consistent behavior of
all Arm devices conforming to a particular architecture version is
crucial. It ensures consistent software behavior across all
implementations, which is key in establishing a wide and vibrant
ecosystem.

Although the architecture defines the required behavior precisely, it
permits a degree of freedom in many aspects of the final device. For
instance, the architecture defines whether caches are permissible, what
their structure may be, and how they respond to management operations,
but the architecture doesn’t specify their size. That decision, along
with many others, is left to whoever implements the device.

In addition, many architectural features are specified as “optional”.
These relate to features that may or may not be implemented in the
production device, at the discretion of the implementer. However, if
these features are included, the architecture defines precisely how they
must behave. On the other hand, if an “optional” feature is not
implemented, the architecture defines the corresponding behavior in
their absence.

The architecture also defines mechanisms by which software developers
can interrogate the system to determine which optional features are
implemented and with which implementation parameters.

There are several architecture licensees operating in this market space,
and the behavior of their products depends on both the architecture and
on the specific implementation deployed by the licensee. In many cases,
that implementation might be proprietary.

### 5.1.2  Implementation Decisions—Microarchitecture

The process of “implementation” involves taking the HDL source code for
the hardware from Arm and transforming that into a description of a
processing element that can be fabricated into a working, physical
device. This is a highly complex multi-stage process. Significant
choices are made along the way that affect the behavior and capability
of the production device.

Those choices might include:

- whether certain optional architectural features are implemented;

- the size and scope of processor and associated logic, such as caches,
buses, and interconnect architecture;

- the number and organization of processing elements; and

- the length and structure of the processor pipeline.

Clearly, these features have a considerable effect on the performance
and behavior of the production device.

In particular, the instruction throughput is not determined by the
architecture but by factors such as the pipeline structure. Complex
pipelines could implement instruction–level parallelism in the hardware,
allow prediction and speculative execution, or accelerate the operation
of some logical and mathematical operations. These decisions have a
great effect on the performance of the production device, but the way
that the device responds to an instruction stream must conform to the
architecture.

### 5.1.3  Manufacturing Variation

The process of taking configured HDL, synthesizing it to a netlist,
physically producing the resultant silicon, and packaging this into a
finished device is one of the marvels of modern manufacturing
technology. The enormous complexity of the devices involved and the
unimaginably small features that they manipulate on silicon substrates
is truly breathtaking.

The precise manufacturing process used has a significant effect on the
characteristics of the device. Choices are made to achieve different
goals such as processing power, clock speed, power consumption, silicon
area, and cost. The primary decision is the “feature size”—the basic
geometric size of the transistors, wires, and gates which constitute the
device—but many other choices contribute to significant variation in the
resulting product.

## 5.2  Neoverse Overview

The Neoverse cores from Arm are specifically designed and configured for
use in cloud computing environments. But each cloud computing
environment has different requirements, so the Neoverse cores are
subdivided into three main ranges: ‘V’, ‘N’, and ‘E’. These three
variants recognize and address the trade-offs between price,
performance, and cost, to serve the differing requirements of cloud,
edge, and infrastructure deployment.

Neoverse V is designed for the highest performance and throughput. These
are designed for general–purpose computing and datacenters performing
machine learning and artificial intelligence tasks. The V range is
designed to scale easily to multi-core systems, while maintaining a
focus on total cost of ownership (TCO) through an emphasis on power
efficiency and cost-effective manufacturing.

Neoverse N is positioned for applications connecting the cloud to the
edge. These deliver high performance with low power requirements and
high bandwidth flexible interconnect.

Neoverse E is best suited for deployment at the network edge, where high
data throughput is key, employing simultaneous multi-threading (SMT) for
high efficiency.

All are built to Armv8–A and Armv9–A architectures, with the newer cores
incorporating the latest Confidential Compute Architecture to allow
provision of secure datapaths from the edge of the network through to
the datacenter.

The table in 5.9 summarizes some of the more important features provided
by each Neoverse core.

## 5.3  Neoverse V–Series

Neoverse V is the performance-first flagship for Neoverse, offering the
highest performance with the fewest compromises in the implementation.
As such, cores in the Neoverse V–Series are targeted at high-performance
computing in the cloud and acceleration for machine learning and
artificial intelligence tasks.

### 5.3.1  Neoverse V1

The Arm Neoverse V1 core, based on Armv8.5–A, was the first Arm core to
include Scalable Vector Extension support, providing 2× 256b SVE
pipelines and twice the floating-point performance capability of the
earlier Neoverse N1.

### 5.3.2  Neoverse V2

The Arm Neoverse V2 was the first Neoverse core based on Armv9
architecture. It has significantly larger caches than Neoverse V1, and
an enhanced pipeline design, providing approximately double the
performance on cloud and machine learning workloads.

CPUs based on Neoverse V2 include AWS Graviton4, Google Axion, and
NVIDIA Grace.

### 5.3.3  Neoverse V3 and Neoverse V3–AE

Neoverse V3 is currently the highest–performance core provided by Arm.
Based on architecture Armv9.2–A, it implements the latest CCA security
features. An increased L2 cache enables increased performance. It is
targeted at High-Performance Computing (HPC), machine learning,
artificial intelligence, and general-purpose compute in a cloud
application.

The decision process that led to the Neoverse V3 also considered Total
Cost of Ownership (TCO) as an important design factor.

Arm Neoverse V3–AE is a variant of Neoverse V3 that implements security
and safety enhancements to enable deployment in environments—such as
automotive—where Functional Safety certification is required.

## 5.4  Neoverse N

### 5.4.1.  Neoverse N1

The Neoverse N1 is engineered for high scalability, making it
particularly suited for the infrastructure between the cloud and edge.
The bus and connectivity architecture allows multi-core clusters to be
implemented together in configurations of up to 16 cores per chip.
Multi-chip packaging solutions allow up to 128 cores per socket, with
CCIX[^8] connectivity, in hyperscale applications.

Neoverse N1 and Neoverse E1 share a common software architecture which
allows for seamless heterogeneous systems encompassing both the edge and
the cloud.

### 5.4.2  Neoverse N2

Neoverse N2 increases scalar performance over Neoverse N1 by 40%. Built
on Armv9.0–A it includes enhancements to improve scalability,
performance and security.

### 5.4.3  Neoverse N3

Arm Neoverse N3 is the highest-performance core in the Neoverse N range,
yielding approximately three times the performance of Neoverse N2 for
machine learning workloads. The advanced design also improves power
efficiency (measured in MIPS per watt) by 20%, improving efficiency on
multi-core deployments.

## 5.5  Neoverse E1

The Neoverse E1 processor is built to Armv8.2–A with emphasis on power
efficiency and data throughput. This makes it particularly well suited
for data transport at the edge. It is the first, and currently the only,
Arm processor to implement simultaneous multi-threading (SMT), which
allows instruction level parallelism (ILP) at the hardware level. The
ability to execute two software threads concurrently yields better
aggregate throughput.

Compared to the earlier Cortex–A53, The Neoverse E1 delivers over double
the compute performance, nearly three times higher throughput
performance, and more than double the power efficiency.

## 5.6  Neoverse Compute Subsystems

The processor is not the only ingredient when implementing a device
suitable for deployment in the data center and allied infrastructure.

In multiprocessor systems handling very large datasets, several factors
become increasingly important: the ability to address large regions of
memory; the speed at which large amounts of data can be moved around the
device between on-chip memory, off-chip storage, and the cache; and the
ability for multiple processors to share data structures and code. These
are not just functions of the processor itself but also of the on-chip
interconnect fabric.

As this fabric becomes increasingly critical to the performance of the
device, it becomes increasingly complex to design and more sensitive to
small changes in configuration and implementation. To mitigate this, Arm
has recently put considerable effort into designing on-chip interconnect
and other system components, such as System MMU, cache, and DMA
controllers. Many partners use these components when configuring and
implementing their devices.

However, as systems become more complex, the engineering cost of putting
them together becomes more significant. Arm is able to mitigate that
with its range of Compute SubSystems (CSS), which are ready-built and
verified by Arm.

Note that while subsystems are available for other Arm cores (see
Corstone™, for example), this text concentrates only on those that
include Neoverse processors. These details are relevant to silicon
designers but not necessarily directly relevant to software developers,
so these details are included here only for completeness.

### 5.6.1  Neoverse CSS V3

The CSS V3 platform is configured and verified for high-performance
cloud, HPC, artificial intelligence and machine learning workloads. It
supports up to 64 Neoverse V3 cores, and includes a customizable memory
subsystem and allows AI accelerators to be connected easily. The system
supports up to 12 channels of (LP)DDR5 memory, up to 64-lane PCIe or CXL
I/O, and high-speed die-to-die connections.

### 5.6.2  Neoverse CSS N3

This platform is based around Neoverse N3 and is targeted for
networking, 5G, and infrastructure edge deployment.

CSS N3 supports between 8 and 32 Neoverse N3 cores per die, and includes
on-chip and off-chip interfaces for (LP)DDR5 memory, up to 32–lane PCIe
or CXL I/O, and high-speed die-to-die connections.

### 5.6.3  Neoverse CSS N2

Neoverse CSS–N2 supports up to 64 Neoverse N2 cores, and is targeted for
an advanced 5 nm manufacturing process. Neoverse CSS N2 CSS interfaces
for (LP)DDR5 memory, PCIe and CXL I/O, plus SBSA certification and a
platform software model.

<table>
<colgroup>
<col style="width: 16%" />
<col style="width: 11%" />
<col style="width: 11%" />
<col style="width: 11%" />
<col style="width: 11%" />
<col style="width: 11%" />
<col style="width: 11%" />
<col style="width: 11%" />
</colgroup>
<tbody>
<tr>
<td></td>
<td>V1</td>
<td>V2</td>
<td>V3</td>
<td>N1</td>
<td>N2</td>
<td>N3</td>
<td>E1</td>
</tr>
<tr>
<td>Architecture</td>
<td>v8.6–A</td>
<td>v9.0–A</td>
<td>v9.2–A</td>
<td>v8.5–A</td>
<td>v9.0–A</td>
<td>v9.2–A</td>
<td>v8.5–A</td>
</tr>
<tr>
<td>ISA<a href="#fn1" class="footnote-ref" id="fnref1"
role="doc-noteref"><sup>1</sup></a></td>
<td>A64<br />
A32/T32</td>
<td>A64<br />
A32/T32</td>
<td>A64 only</td>
<td>A64<br />
A32/T32</td>
<td>A64<br />
A32/T32</td>
<td>A64 only</td>
<td>A64 only</td>
</tr>
<tr>
<td>SVE</td>
<td>Y</td>
<td>V2+AES</td>
<td>V2+AES</td>
<td>N</td>
<td>Y</td>
<td>Y</td>
<td>N</td>
</tr>
<tr>
<td>Crypto</td>
<td>Y</td>
<td>Y</td>
<td></td>
<td>Optional</td>
<td>Optional</td>
<td>Optional</td>
<td>Optional</td>
</tr>
<tr>
<td>MPAM</td>
<td>Y</td>
<td></td>
<td></td>
<td></td>
<td>Y</td>
<td>Y</td>
<td></td>
</tr>
<tr>
<td>Pointer Authentication</td>
<td>Y</td>
<td></td>
<td></td>
<td></td>
<td>Y</td>
<td></td>
<td></td>
</tr>
<tr>
<td>Cluster</td>
<td>Direct–connect</td>
<td>Direct–connect</td>
<td>Direct–connect</td>
<td>Up to 4 CPUs</td>
<td>Direct–connect</td>
<td>Direct–connect</td>
<td>Up to 8 CPUs</td>
</tr>
<tr>
<td>Physical Address<a href="#fn2" class="footnote-ref" id="fnref2"
role="doc-noteref"><sup>2</sup></a></td>
<td>48–bit</td>
<td>48–bit</td>
<td>48–bit</td>
<td>48–bit</td>
<td>48–bit</td>
<td>48–bit</td>
<td>44–bit</td>
</tr>
<tr>
<td><p>L1 I Cache</p>
<p>L1 D Cache</p></td>
<td><p>64 kB</p>
<p>64 kB</p></td>
<td><p>64 kB</p>
<p>64 kB</p></td>
<td><p>64 kB</p>
<p>64 kB</p></td>
<td><p>64 kB</p>
<p>64 kB</p></td>
<td><p>64 kB</p>
<p>64 kB</p></td>
<td><p>32 kB</p>
<p>64 kB</p></td>
<td><p>32–64 kB</p>
<p>32–64 kB</p></td>
</tr>
<tr>
<td>L2 Cache</td>
<td>1 MB or 512 kB</td>
<td>1 MB or 2 MB</td>
<td>2 MB or 3 MB</td>
<td>256 kB–1 MB</td>
<td>512 kB–1 MB</td>
<td>128 kB–2 MB</td>
<td>Optional<br />
64–256 kB</td>
</tr>
<tr>
<td>L3 Cache</td>
<td></td>
<td></td>
<td></td>
<td>Optional<br />
512 kB–4 MB</td>
<td></td>
<td></td>
<td>Optional<br />
512 kB–4 MB</td>
</tr>
<tr>
<td>Security</td>
<td>TrustZone<sup>®</sup></td>
<td>CCA</td>
<td>CCA</td>
<td>TrustZone<sup>®</sup></td>
<td>TrustZone<sup>®</sup></td>
<td>CCA</td>
<td>TrustZone<sup>®</sup></td>
</tr>
<tr>
<td>MTE</td>
<td></td>
<td>Y</td>
<td>Y</td>
<td></td>
<td></td>
<td>Y</td>
<td></td>
</tr>
<tr>
<td>RME</td>
<td></td>
<td></td>
<td>Y</td>
<td></td>
<td></td>
<td>Y</td>
<td></td>
</tr>
<tr>
<td>BRBE</td>
<td></td>
<td></td>
<td>Y</td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr>
<td>RAS</td>
<td></td>
<td></td>
<td>Y</td>
<td></td>
<td>Y</td>
<td>Y</td>
<td>Y</td>
</tr>
</tbody>
</table>
<section id="footnotes" class="footnotes footnotes-end-of-document"
role="doc-endnotes">
<hr />
<ol>
<li id="fn1"><p><sup>ISA = Instruction Set Architecture. Where support
for the A32 and T32 instruction sets is shown, this is only at EL0 in
all cases.</sup><a href="#fnref1" class="footnote-back"
role="doc-backlink">↩︎</a></p></li>
<li id="fn2"><p><sup>This refers to the physical width of the address
bus in bits.</sup><a href="#fnref2" class="footnote-back"
role="doc-backlink">↩︎</a></p></li>
</ol>
</section>

## 5.7  Feature Summary

The table shows a summary of features for all the current Neoverse cores
that are most relevant to software developers. It is not an exhaustive
list—please refer to Arm’s website for up-to-date details.

### 5.7.1  Correlation with x86 Features

The predominant alternative architecture in use in the data center is
x86, primarily in devices supplied by Intel and AMD. In a similar way to
the Arm architecture, the x86 architecture has a number of capability
extensions that drive platform choice. When evaluating a potential Arm
solution, it is useful to identify the broad correlation between these
features across the architectures.

The table below is not an exhaustive list of extensions in either
architecture, but concentrates on those which are visible to, and of
interest to, software developers. For instance, features associated with
virtualization would only be of interest to developers and vendors of
hypervisors. Features for accelerating cryptographic operations would be
of interest only to cryptographic libraries.

<table>
<colgroup>
<col style="width: 21%" />
<col style="width: 28%" />
<col style="width: 25%" />
<col style="width: 24%" />
</colgroup>
<thead>
<tr>
<th>Extension</th>
<th>Description</th>
<th>Use Cases</th>
<th>Arm Equivalent<a href="#fn1" class="footnote-ref" id="fnref1"
role="doc-noteref"><sup>1</sup></a></th>
</tr>
</thead>
<tbody>
<tr>
<td><p>MultiMedia eXtension</p>
<p>MMX (1996)</p></td>
<td>SIMD<a href="#fn2" class="footnote-ref" id="fnref2"
role="doc-noteref"><sup>2</sup></a> instructions to enhance multimedia
performance</td>
<td>Image and audio processing</td>
<td><strong>NEON (Armv7–A)</strong></td>
</tr>
<tr>
<td><p>Streaming SIMD Extensions</p>
<p>SSE (1999)<br />
SSE2 (2001)<br />
SSE3 (2004)</p></td>
<td>SIMD instructions to improve performance of 3D graphics and
scientific simulations</td>
<td>3D graphics, scientific simulations</td>
<td><strong>NEON (Armv7–A)</strong></td>
</tr>
<tr>
<td><p>Advanced Vector eXtensions</p>
<p>AVX (2011)<br />
AVX2 (2013)<br />
AVX–512 (2016)</p></td>
<td>Extended SIMD instructions to support high–performance computing and
vector<a href="#fn3" class="footnote-ref" id="fnref3"
role="doc-noteref"><sup>3</sup></a> processing</td>
<td>Machine learning, scientific computing</td>
<td><p><strong>Scalable Vector Extension</strong></p>
<p><strong>SVE (Armv8.2–A)</strong></p>
<p><strong>SVE2 (Armv9–A)</strong></p></td>
</tr>
<tr>
<td><p>Advanced Encryption Standard New Instructions</p>
<p>AES–NI (2008)</p></td>
<td>Accelerates AES encryption and decryption operations in
hardware</td>
<td>Secure data encryption and decryption</td>
<td><p><strong>Cryptography Extensions</strong></p>
<p><strong>(Armv8–A)</strong></p></td>
</tr>
<tr>
<td><p>AMD Virtualization</p>
<p>AMD–V (2006)</p>
<p>Intel Virtualization Technology</p>
<p>Intel VT–x (2006)</p></td>
<td>Enables hardware–assisted virtualization<a href="#fn4"
class="footnote-ref" id="fnref4" role="doc-noteref"><sup>4</sup></a> for
running multiple operating systems</td>
<td>Virtual machines, cloud computing</td>
<td><p><strong>ARM Virtualization Extensions</strong></p>
<p><strong>(Armv8–A)</strong></p></td>
</tr>
<tr>
<td><p>Advanced Matrix eXtensions</p>
<p>AMX (2021)</p></td>
<td>Accelerates matrix operations for artificial intelligence and
machine learning workloads</td>
<td>Artificial intelligence, machine learning, high–performance
computing</td>
<td><p><strong>Scalable Matrix Extension</strong></p>
<p><strong>SME (Armv9.2–A)</strong></p></td>
</tr>
</tbody>
</table>
<section id="footnotes" class="footnotes footnotes-end-of-document"
role="doc-endnotes">
<hr />
<ol>
<li id="fn1"><p><sup>Exact equivalence is not implied here. The
suggested Arm extension is the closest equivalent, which may provide
similar capability through a different mechanism.</sup><a href="#fnref1"
class="footnote-back" role="doc-backlink">↩︎</a></p></li>
<li id="fn2"><p><sup>Single Instruction Multiple Data—instructions that
are capable of operating simultaneously on multiple data items.</sup><a
href="#fnref2" class="footnote-back" role="doc-backlink">↩︎</a></p></li>
<li id="fn3"><p><sup>A vector is a data structure holding multiple data
items—usually of the same type—stored in a contiguous area of
memory.</sup><a href="#fnref3" class="footnote-back"
role="doc-backlink">↩︎</a></p></li>
<li id="fn4"><p><sup>Virtualization is a technology which allows
multiple operating systems and multiple applications to co–exist on a
single processor, secured and isolated from each other.</sup><a
href="#fnref4" class="footnote-back" role="doc-backlink">↩︎</a></p></li>
</ol>
</section>

# 6.  Available Implementations

The Neoverse™ range of cores has been licensed by many of Arm’s
partners, ranging from established players in the high–performance
computing (HPC) and cloud space, to start-ups looking to innovate in the
technology industry. These licensees take Arm’s designs and build
differentiated devices for their respective target markets.

There are two principal routes to access any particular Neoverse
hardware platform in order to develop and execute software applications.

Many Neoverse-based devices are available to purchase on the open
market, either as bare chips or fitted to a development board. Depending
on the manufacturer or supplier, these will come with a varying level of
software support. This may be just boot code, firmware, and operating
systems, or it may include standard or proprietary application software.
The choice of platform will be influenced by the intended end use for
the system.

However, many developers choose to access cloud-hosted platforms. This
has many advantages, especially that physical hardware is not required.
Without the need to own and maintain in-house hardware, it is easier to
upgrade to later and higher-performance platforms if the need arises.

As with so much about developing on Arm, the choice is yours, and there
is a huge variety of choices.

This chapter first lists the silicon implementations of Neoverse cores
that are currently available, then the available cloud instances
deployed on Arm silicon. Many of the silicon devices listed are
available directly to the developer via cloud-hosted systems deployed by
major cloud vendors. Some of them, though, are developed for proprietary
use and might not be available to purchase on the open market.

The reader should be aware that this list of licensees, developers and
providers is constantly and rapidly changing, as more licensees enter
the market and existing licensees enhance their product offering. The
list is also not exhaustive, because there may be licensees who have
started development but not yet made their activities public.

Although there is a sometimes bewildering array of platforms available,
there is also a degree of standardization, which allows for an
increasing degree of interoperability between platforms and software
components.

## 6.1  SystemReady

One consequence of the extensive flexibility that Arm’s licensees have
in turning processor designs into finished devices is the wide diversity
of the resulting platforms. But this could easily result in a very
fragmented software market.

To combat this, Arm introduced the SystemReady program. SystemReady
defines firmware and hardware standards to enable a consistent
cross-platform baseline for software developers, equipment
manufacturers, and vendors. Choosing a SystemReady-certified platform
should enable a wider choice of software.

SystemReady has been developed over a number of years in partnership
with the industry and is currently supported by over 45 partners.
Initially aimed at the server market, SystemReady now covers a much
broader range of platforms, including SystemReady LS for hyperscalers,
SystemReady ES for embedded systems, SystemReady IR for embedded Linux,
and SystemReady SR for servers and workstations. All of these build on
an underlying set of system specifications, which cover boot code,
system components, and hardware features. This provides a stable,
standardized platform for operating systems, allowing a degree of
interchangeability and a “just works” out-of-box experience.

For Neoverse platforms, the relevant bands are SystemReady LS and
SystemReady SR.

SystemReady is managed by Arm, in collaboration with its partners.
Certifications are issued by Arm to compliant platforms.

## 6.2  Silicon Implementations of Neoverse Cores

This section only presents an overview. For detailed and up-to-date
specifications for all the listed products, please refer to the
manufacturer’s website.

### 6.2.1  Ampere

Ampere was founded in Santa Clara, California, in 2017, with the goal of
developing Arm-based server processors. Its early products were based on
the X–Gene processors from Applied Micro (Ampere acquired the processor
design team from Applied Micro in 2017). Later products have used Ampere
Altra—a semi-custom Neoverse N1, built to Armv8.2–A. However, the latest
products use Ampere’s own in–house AmpereOne core. The AmpereOne product
line, built to Armv8.6–A, scales to 256 cores per chip.

Ampere’s processors are deployed in the cloud by Oracle, Google,
Microsoft, HPE, and others.

### 6.2.2  Annapurna Labs

Annapurna Labs was founded in Israel in 2011. Since 2015, it has been a
wholly-owned subsidiary of AWS. Its main product line, Graviton, is now
at version 4. Early versions were built on Cortex–A72 cores from Arm;
later versions have been built on Neoverse N1 and lately Neoverse V1 and
Neoverse V2. The latter implements Armv9.0–A and incorporates the latest
advances in security.

Graviton cores are deployed in the cloud by AWS. Graviton4 is a 96-core
Neoverse V2 device made available in a number of AWS EC2 instances in
the cloud.

### 6.2.3  Google

Google’s Axion processors are based on Neoverse V2, implementing
Armv9.0–A. Announced in early 2024, Axion–based servers are
SystemReady-compliant, and are available via a number of Google Cloud
services, including Google Compute Engine, DataProc, DataFlow, Cloud
Batch, and Google Kubernetes Engine.

### 6.2.4  Marvell

Marvell acquired Cavium in 2018, inheriting the ThunderX and Octeon
processor lines. Early Octeon processors implemented the MIPS64
architecture, switching to Arm with the introduction of ThunderX in
2014.

Octeon TX2 is deployed in a range of high–performance infrastructure
processors, based on a multi-core Cortex–A72 implementation.

Octeon 10 is a family of DPUs[^9] targeted at dataplane acceleration and
high-speed packet processing for 5G wireless infrastructure. Octeon 10
is built around a multi-core Neoverse N2 architecture with 8–24 cores.

### 6.2.5  Microsoft

Microsoft’s Azure Compute Platform cloud service provides solutions
based on Ampere Altra and on Microsoft’s in-house Cobalt 100 processor.
Cobalt 100 is built using the Arm Neoverse CSS N2, facilitating
migration between this and other SystemReady-compliant platforms.

Arm–based instances are deployed in the following families:

- B–Family (general-purpose compute on Ampere Altra)

- D–Family (general-purpose compute on Cobalt 100)

- E–Family (memory-intensive workloads on Cobalt 100 or Ampere Altra)

### 6.2.6  NVIDIA

NVIDIA announced the Grace CPU in 2021, targeted at high-performance
compute and AI workloads in the datacenter.

Grace incorporates 72 Neoverse V2 cores and implemented Armv9.0A. The
Grace CPU is available in several implementations including: 

- NVIDIA Grace C1 (single-die, 72 Neoverse V2 cores), targeting
traditional datacenter workloads 

- NVIDIA Grace CPU Superchip (two-die, 144 Neoverse V2 cores) targeting
HPC workloads 

- NVIDIA Grace–Hopper and Grace–Blackwell Superchips, designed for
high-performance on AI training and inference workloads 

## 6.3  Cloud Implementations

This section presents only overview information. For detailed and
up-to-date specifications for all the listed products, please refer to
the provider’s website.

Across much of the cloud ecosystem, the standard unit of configuration
and pricing is the “virtual CPU”, often abbreviated to vCPU. The
majority of vendors use this unit in their descriptions. Arm Neoverse
processors are single-threaded, currently with Neoverse E1 being the
only exception, so each virtual CPU corresponds to a single physical
CPU. Multi-threaded cores from providers such as AMD or Intel may
implement multiple vCPUs on a single physical core. Oracle (see below)
employs a slightly different nomenclature.

The vendors listed are distributed across the world. Some operate only
in particular geographies, and some may have limited offerings in
certain locations. As usual, check with each vendor’s website for
up-to-date availability information.

### 6.3.1  Google Cloud

Google Cloud makes Arm instances available in a number of ways, all
through the General-purpose Machine Family within Google Cloud Compute
Engine.

The Tau T2A series is powered by 64-core Ampere Altra processors (based
on Neoverse N1) and is Google Cloud’s most cost-effective
general–purpose compute range, suitable for low-traffic web servers and
virtual desktops.

The C4A series is powered by Google’s in-house designed Axion processor,
based on Neoverse V2 and is suitable for high-performance
general-purpose compute, high–traffic web servers, and multi-media
streaming.

**Based on Ampere Altra**

**t2a–standard** – general–purpose compute, 1–48 vCPUs, 4 GB per CPU

**Based on Google Axion**

**c4a–standard**—general-purpose compute, 1–72 vCPUs, 4 GB per CPU

**c4a–highcpu**—compute-optimized, 1–72 vCPUs, 2 GB per CPU

**c4a–highmem**—memory-optimized, 1–72 vCPUs, 8 GB per CPU

### 6.3.2  Microsoft Azure Compute Platform

Arm processors power a number of virtual machines in the Compute
Platform family. These include:

**Bpsv2**—cost–effective general-purpose compute, Ampere Altra, 2–16
vCPUs, up to 4 GB per CPU (low–traffic web servers, small databases,
develop and test platforms)

**Dpsv6**—high-performance general-purpose workloads, Cobalt 100, 2–96
vCPUs, up to 4 GB per CPU, also available with local disk storage

**Dpsv5**—non-memory-intensive workloads, Ampere Altra, 2–64 vCPUs, 2 GB
per CPU, also available with local disk storage

**Epsv5**—memory-intensive enterprise workloads, Ampere Altra, 2–32
vCPUs, up to 8 GB per CPU, also available with local disk storage

### 6.3.3.  Oracle

Oracle Cloud Infrastructure (OCI) offers a combination of configurable
Virtual Machine (VM) instances and Bare Metal (BM) instances. These are
supported on two classes of Arm platform, both implemented on Ampere
processors:

**Standard.A1**—based on Altra

**Standard.A2**—based on AmpereOne

OCI makes available Oracle’s full developer stack, including Oracle
Linux, Java, and MySQL, on either of the two Arm platforms. Irrespective
of which platform you choose for your development, Oracle’s method of
calculating core count is slightly different from most other vendors. In
place of the widely used vCPU unit, Oracle use the term “Oracle CPU”
(OCPU), which always equates to a single physical processor, which may
support more than one execution thread. For non-Arm instances, which
support multi-threading, one OCPU equates to one physical core, usually
supporting two execution threads (other vendors may refer to this as
*two* vCPUs). The Oracle Arm A1 instances support one physical core and
one execution thread per OCPU; the Oracle Arm A2 instances support two
physical cores and two execution threads per OCPU.

Oracle refers to the various configurations of virtual machines as
“shapes”. The following Arm shapes are supported:

**VM.Standard.A1.Flex**—1–80 OCPUs (OCPU=1 core, 1 thread), 1–64 GB per
OCPU

**VM.Standard.A2.Flex**—1–78 OCPUs (OCPU=2 cores, 2 threads), 1–64 GB
per OCPU

**BM.Standard.A1**—Bare metal Ampere Altra Q80–30, 3.0 GHz (OCPU=1 core,
1 thread)

### 6.3.4  Amazon Web Services

All Amazon Web Services (AWS) Arm instances are based on the Graviton
cores developed by Annapurna Labs, and are made available via the Amazon
Elastic Compute Cloud (EC2). The Graviton–based Arm instances are
highlighted as a cost-effective choice in terms of performance per
dollar. While not based on Neoverse, it is worth noting that AWS also
makes available instances for Apple Mac hardware, powered by
Arm-compatible Apple silicon (such as the Apple M1 and M2).

All the Arm instances use the Amazon Nitro lightweight hypervisor for
improved security and performance. Most are available in bare-metal form
as well as with various configurations of memory, local and remote
storage, networking bandwidth, etc.

As expected, there is a wide range of configuration options, optimized
for various categories of workload, including:

**General Purpose**

**M8g**—Graviton4, highest-performance general–purpose compute, 1–192
vCPUs, up to 4 GB per core

**M7g**—Graviton3, general-purpose compute, 1–64 vCPUs, 4 GB per core

**M6g**—Graviton2, balanced compute, memory and networking for a range
of workloads, 1–64 vCPUs, 4 GB per core

**T4g**—Graviton2, burstable general-purpose workloads, 2–8 vCPUs, up to
4GB per core

**Compute Optimized**

**C8g**—Graviton4, high-performance compute–bound workloads, 1–192
vCPUs, 2 GB per core

**C7g**—Graviton3, compute-intensive workloads, 1–64 vCPUs, 1–2 GB per
core

**C7gn**—Graviton3E, high-performance packet–processing, 1–64 vCPUs, 1–2
GB per core

**C6g**—Graviton2, cost-effective performance, 1–64 vCPUs, 2–4 GB per
core

**C6gn**—Graviton2, high throughput networking, 1–64 vCPUs, 2 GB per
core

**Memory Optimized**

**R8g**—Graviton4, high-performance, 1–192 vCPUs, 8 GB per core

**R7g** —Graviton3, memory-intensive workloads, 1–64 vCPUs, 8 GB per
core

**R6g**—Graviton2, cost-effective high-performance, 1–64 vCPUs, 8 GB per
core

**X8g**—Graviton4, best price-performance, 1–192 vCPUs, 16 GB per core

**X2gd**—Graviton2, lowest cost per GB, 1–64 vCPUs, 16 GB per core

**Storage Optimized**

**I4g**—Graviton2, best price per TB storage, 2–64 vCPUs, 8 GB per core

**Im4gn**—Graviton2, best price-performance, 2–64 vCPUs, 8 GB per core

**Is4gen**—Graviton2, best SSD density, 1–32 vCPUs, 6 GB per core

**HPC Optimized**

**Hpc7g**—Graviton3E, compute-intensive HPC, 16–64 vCPUs, 128 GB total

### 6.3.5  Alibaba Cloud

Alibaba Cloud’s Elastic Compute Service (ECS) provides a number of Arm
instances. Some are based on the Ampere Altra processor, while others
employ a variety of processors from Chinese vendors—some of which are
not commercially available to purchase. Most of the Chinese instances
are only available in China. All advertise high efficiency and
cost-effectiveness.

**Based on Yitian 710 (Armv9.0–A, developed in–house and not
commercially available)**

**g8y**—general-purpose compute, 1–128 vCPUs, 4 GB per core

**c8y**—compute-optimized, 1–128 vCPUs, 2 GB per core

**r8y**—memory-optimized, 1–128 vCPUs, 8 GB per core

**Based on Ampere Altra**

**g6r**—general-purpose compute, 1–64 vCPUs, 4 GB per core

**c6r**—compute-optimized, 1–64 vCPUs, 2 GB per core

**ebmgn6ia.20xlarge**—fixed-configuration, bare-metal instance, 80 CPUs,
256 GB

**Based on Kunpeng920 (Armv8.2–A, manufactured by HiSilicon)**

**s5–kp**—shared instances, 2–64 vCPUs, 1–8 GB per core

**g5s–kp**—dedicated instances, 2–56 vCPUs, 1–8 GB per core

**g5m–kp**—dedicated instances, 2–88 vCPUs, 1–8 GB per core

**g5x–kp**—dedicated instances, 2–120 vCPUs, 1–8 GB per core

**Based on FT processors (Armv8.0–A, manufactured by Phytium)**

**s5–ft–k**—FT–2000+ processor, shared instances, 2–64 vCPUs, 1–8 GB per
core

**s6–ft–k**—FT–S2500 processor, shared instances, 2–64 vCPUs, 1–8 GB per
core

**g5s–ft–k**—FT–2000+ processor, dedicated instances, 2–56 vCPUs, 1–8 GB
per core

**g6x–ft–k**—FT–S2500 processor, dedicated instances, 2–120 vCPUs, 1–8
GB per core

### 6.3.6  Equinix

Equinix provide cloud services and IT infrastructure support worldwide.
They offer bare-metal instances based on Ampere Altra processors as part
of this service.

**c3.large.arm64**—Ampere Altra, bare-metal instance, 80 cores, 256 GB
memory

### 6.3.7  Scaleway

Scaleway’s Cost–Optimized service is based on the Ampere M128–30
processor and is offered as an energy efficient and cost-effective
alternative to other instances. The Ampere M128–30 is a 128-core
processor built to Armv8.2–A.

**COP–ARM**—Ampere M128–30, bare-metal instance, 2–32 vCPUs, 8 GB per
core

### 6.3.8  Hetzner Cloud

The Hetzner cloud compute offering includes instances based on Ampere
Altra processors.

**CAX**—Ampere Altra, shared instances, 2–16 vCPUs, 2 GB per core

### 6.3.9  Tencent

Tencent’s Cloud Virtual Machine product includes a single Arm-based
instance, based on the Ampere Altra processor.

**Standard SR1**—Ampere Altra, general-purpose compute, 1–64 vCPUs, 2–4
GB per core

### 6.3.10 Gcore

The GCore Virtual Machine product makes instances available supporting
either Linux or Windows, based on the architecture Armv8.2–A Ampere
Altra Max processor.

**a1–Standard**—optimized for cloud workloads, 1–32 vCPUs, 2–4 GB per
core

**a1–cpu**—high-performance cloud workloads, 2–32 vCPUs, 1 GB per core

### 6.3.11. GleSYS

GleSYS’s Dedicated Server product includes the following dedicated Arm
instances, based on Ampere processors.

**Small.arm64**—Ampere Altra Q80–26, 80 vCPUs, 64 GB memory

**Medium.arm64**—Ampere Altra M96–28, 96 vCPUs, 256 GB memory

**Small.arm64**—Ampere Altra Max M128–30, 128 vCPUs, 1 TB memory

# 7.  Market Positioning and Competitive Analysis

The Neoverse™ cores represent a new market position for Arm<sup>®</sup>
technology.

As you have seen in the context of Arm’s history, the early commercial
success of Arm was based on achieving very high volumes. Royalty rates
were deliberately set low, so large volumes were necessary to sustain
sufficient income for the company. This model worked very well for the
mobile phone market—the market in which Arm first achieved significant
success. With the widespread adoption of mobile phones by the public
across many geographies, this market achieved very high volumes but
remained very price sensitive. The traditional Arm “virtues” of
cost-effectiveness, power efficiency, and flexibility of deployment led
to Arm’s success in this market. The enormous volume growth achieved by
mobile phone vendors in the 1990s and 2000s powered matching growth in
Arm’s fortunes.

Arm subsequently moved into other markets, such as digital cameras,
modems and routers, storage devices, and smart consumer devices. These
markets displayed similar economics. The devices are predominantly
powered by batteries, so the highly power efficient Arm processors were
a compelling choice. High volumes coupled with price sensitivity made
these markets ideal targets for Arm, and the company achieved great
success in many of them.

The move into the data center market, however, is markedly different.
Here, volumes are orders of magnitude smaller, while unit prices are
much higher. The key considerations are, therefore, quite different.

Power efficiency, unit cost, and processing power are all still
important, but for different reasons and with different priority.
Additional factors—such as per-core performance and scalability—become
more important.

## 7.1  Cost–Effective Performance

The primary requirement for data center compute devices is sufficient
processing power. The x86 devices, which have dominated this market for
considerable time, are clearly capable of sustained high performance. To
be seen as a viable alternative, Arm needed to deploy processors capable
of running similar workloads. The Neoverse processors were designed
specifically to achieve this. Modeling showed, for instance, that
coherent instruction caches increased performance significantly in
multi-processor systems such as the typical systems in a data center. In
addition, high-bandwidth on-chip and off-chip interconnect is vital for
moving the very large amounts of data involved in typical data center
workloads. In order to work with very large datasets, the ability to
address large amounts of memory is also important.

The Neoverse cores were specifically designed to these considerations.
Benchmarks—both by Arm, and by independent vendors—have shown that
Neoverse processors can compete with alternative platforms while
remaining cost-effective and consuming less power.

## 7.2  Sustainability

In earlier markets, the need to conserve battery life drove ever greater
power efficiency in Arm processors. A wide range of sleep, deep-sleep,
and hibernation power modes allowed the processors to enter and leave
power-saving modes quickly and efficiently. In the data center, power
consumption matters for a different reason: huge numbers of processors
are deployed in close proximity, needing sustained high performance for
long periods of time, so heat dissipation and total system power
consumption become critical.

There are several ways of dealing with heat dissipation, including the
use of active cooling systems, and a reduction in the power consumption
of individual devices. The cooling systems deployed in a typical data
center are complex and expensive, and themselves consume significant
power. It is therefore helpful to concentrate on reducing the power
consumption of the devices themselves. While this reduces the cost of
running them, it also allows deployment of simpler and most
cost-effective cooling solutions. This reduces both the build cost and
running cost of a typical data center.

In today’s environmentally conscious world, the reduction of total
energy consumption is an increasingly important design goal, making Arm
processors a more attractive solution. Their energy efficiency can help
offset the rising energy demands of data centers driven by the growing
use of compute-intensive artificial intelligence and machine learning
workloads.

## 7.3  Scalability

Scalability—the ability to keep performance approximately proportional
to the number of cores—is a key requirement for data center operators.
Arm addresses this, and allows its customers to address this, in
multiple ways.

Recall that Arm provides designs for processors and their associated
silicon infrastructure. Arm’s partners can deploy these in many
different sizes and configurations. The number of cores and how they are
interconnected provides huge flexibility in the capability of the
finished device. This allows Arm’s partners to provide devices targeted
at a very wide range of deployments—from single-processor to
many-processor. As you have seen, devices are currently available with
up to 256 cores in a single chip. This allows partners to target a wide
range of price and capability points across the market. Many of these
devices are plug- or pin-compatible, allowing smaller chips to be
replaced with larger ones as demand increases.

The scalability enabled by these design choices also allows devices to
be targeted at deployment from the data center to the edge of the
network, retaining architectural and software compatibility across the
range.

## 7.4  Total Cost of Ownership (TCO)

TCO is an aggregate of several factors: the initial cost to build
individual devices and complete data centers; power and other running
costs for the data center as a whole—including the need for cooling
systems; and costs associated with deploying software applications.

Arm-based systems allow reductions in all these individual costs,
enabling a data center solution that is both cheaper to build and
cheaper to run.

## 7.5  Ecosystem Advantages

One of the great strengths of Arm has always been its commitment to
working closely with as many partners as possible to build a broad and
deep ecosystem of software and tooling support. The Arm ecosystem has
been regarded for some time now as the largest around a single
architecture the industry has ever seen.

The data center industry has long been based on x86 architecture
platforms and the huge body of standard software available for them.
Traditionally, it has been regarded as expensive to port necessary
software components—including firmware, operating systems, middleware,
and applications—to any new platform. Arm and its partners have worked
hard in recent years to ensure that the majority of necessary components
are supported on Arm platforms and have good performance compared to
competing solutions. The porting costs are now minimal, and the size of
the ecosystem is growing all the time, leading to the prospect of better
and cheaper support in the future.

[^1]: <sup>This was changed to “Arm” as part of a rebranding exercise in
    2017.</sup>

[^2]: <sup>Arm2 at 8MHz achieved 4DMIPS, nearly twice the 2.15DMIPS of
    the 16MHz i386DX (Source: Real World Technology). The chip consisted
    of 28000 transistors, vs the 275000 in the 80386. It was also 7x
    faster than the 7MHz 68000 used in the Amiga 1000 and the Macintosh,
    and 50% faster than the 16.6MHz 68020 in the Macintosh 2 and Sun
    3.</sup>

[^3]: <sup>There are a small number of instances where features have
    been removed as part of an architectural update. These usually
    follow a significant period during which the feature concerned is
    marked as deprecated to ensure that it is no longer in use.</sup>

[^4]: <sup>The EL can also change on entry to or exit from Debug state
    but the details of this need not concern us here.</sup>

[^5]: <sup>See below for more information on instruction sets.</sup>

[^6]: <sup>This leads to a simple hardware implementation in which each
    Thumb instruction is translated to an Arm equivalent when fetched
    from instruction memory, and these translated instructions are then
    executed by a single (Arm) decode and execution unit.</sup>

[^7]: <sup>Historically, Non–Secure state has been referred to as
    “Normal world”. You may find this term in older documentation.</sup>

[^8]: <sup>Cache Coherent Interconnect for Accelerators (CCIX) is an
    interconnect standard which allows accelerators to be connected in a
    manner which maintains and leverages cache coherency between
    separate processing elements.</sup>

[^9]: <sup>A Data Processing Unit (DPU) is a programmable processing
    element which is optimized for high–speed processing and
    transmission of data.</sup>
