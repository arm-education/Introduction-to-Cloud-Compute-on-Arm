# Part 2—The Software Stack

# 1. Diverse Use Cases Need Diverse Cores

The Neoverse™ range of cores spans a wide breadth of performance points,
capabilities, and applications. Neoverse V represents the highest
possible performance and is used for high performance compute (HPC) in
the cloud. Neoverse N trades some performance for scalability and
greater power efficiency when deployed in multi–core applications in
infrastructure. Neoverse E is optimized for data throughput and is
typically deployed towards the edge of the network—for example, in a
smart NIC. In addition, Neoverse E and Neoverse N support similar
software, allowing common applications to be run on both relatively
easily.

The Neoverse range is further expanded and diversified by a wide variety
of custom cores, designed and implemented by partners of
Arm<sup>®</sup>. These cores have different and specific balances
between performance, power efficiency, scalability, connectivity, and
cost-of-ownership.

## 1.1 Supported Software

Because there are many diverse use cases for Neoverse systems, Arm also
supports a large number of software packages. Arm maintains a list of
these on its website, here:
[https://www.arm.com/developer–hub/ecosystem–dashboard/servers–and–cloud–computing](https://www.arm.com/developer-hub/ecosystem-dashboard/servers-and-cloud-computing).
The list is constantly being updated as the number of supported packages
evolves over time.

At the time of writing, this list contains over eight hundred software
packages, including commercial software as well as free and open source
software (FOSS), across a wide range of product categories, including
operating systems, databases, HPC, security, web hosting, artificial
intelligence and machine learning, networking, storage, and more.

In the category of operating systems, there are twenty-six products
listed. Of these, twenty are FOSS—including mainstream Linux offerings
such as Red Hat, Ubuntu, SUSE, Fedora, Debian and others. The commercial
offerings include Windows, as well as enterprise–grade versions of Red
Hat and SUSE.

Of particular interest to migrating developers is the fact that the
largest category of supported packages are cloud-native development
tools.[^11] The list includes offerings from popular vendors such as
CircleCI, Apache, Azure, Daytona, Docker, GitHub, Harness, Kubernetes,
Nomad, and Oracle. Alongside this is a comprehensive set of languages
and development tools, including compilers, debuggers and profilers. The
size and coverage of this list means that the majority of developers
will be able to migrate to a Neoverse platform without changing their
tooling solution.

## 1.2 Example Platform

For the software developer seeking to deploy applications on a Neoverse
processor that is accessed via a cloud instance, the target device will
probably be based on Neoverse V or Neoverse N, implementing one of the
Armv9–A architectures. The following discussion makes this assumption.

To focus the discussion further, we will refer to a Reference Design
(RD) based on one of Arm’s Neoverse Compute Subsystems (CSS). Each CSS
is provided by Arm to its partners in order to shorten the development
time and to reduce the engineering cost, for partners to get to market
with a complete device. Importantly, this allows partners to focus their
in-house resources on customizing the device for their own specific
environment and workloads—increasing the amount of differentiation they
can offer. These CSS products also come with reference software
stacks—from boot firmware to hypervisors and Linux ports—which are made
available via a public GitHub repository.

Additionally, Fixed Virtual Platform (FVP) models are available. These
are configurable software simulation models of real hardware that allow
software to be developed, executed, tested, and validated in the absence
of a physical platform. This removes the need for access to physical
devices, and also allows software to be written for platforms that are
in development but not yet physically available.

For silicon developers, the impact of implementation configuration
choices can be tested during the development of the device. However,
please note that execution speeds on a software simulation will be
significantly slower than a corresponding hardware platform.

Specifically, we will refer to the Neoverse N2 Reference Design, which
is based on the Neoverse CSS N2 platform. The Neoverse N2 CSS is a
highly configurable design that offers significant scalability to the
licensee. It supports up to 64 Neoverse N2 processors, together with
ancillary components, cache, memory interfaces, interconnect, and
interfaces for connection to on-chip and off-chip components. The size
and configuration of many of these components is chosen during the
design and manufacturing process by the licensee.

<img src="./media/image6.png" style="width:5.75in;height:3.09375in" />

Figure 1: Neoverse CSS N2 Block Diagram

A diagram of Neoverse CSS N2 is shown in Figure 1. Components shown
include:

**Processor blocks**
In the delivered configurations of Neoverse CSS N2, each processor block
contains a single Neoverse N2 processor, together with a private L1
I–cache, a private L1 D–cache, and a private unified L2 cache. Each of
these components is connected to the rest of the system via a Dynamic
Shared Unit (DSU), which contains interface bridges, power management
logic, and debug logic. The Neoverse N2 CSS is capable of supporting 24,
32 or 64 processor blocks.

**Coherent Mesh Network Neoverse (CMN–700) interconnect**  
This is the main system interconnect infrastructure, connecting all the
system components in a mesh topology. It contains the shared system
level cache, and provides interfaces to on-chip and off-chip I/O, PCIe,
on-chip DRAM, and die-to-die connectivity.

**System Control Processor (SCP)**  
**Manageability Control Processor (MCP)**
Two Cortex<sup>®</sup>–M7 processors, which provide management and
control of the device, power monitoring of each individual processor and
of the system as a whole, the external management interface (SCMI) and
security support.

**A diagram of the Neoverse N2 Reference Design is shown in Figure 2.
The Neoverse N2 Reference Design is compliant with Arm Server Base
System Architecture version 6.0, indicating compatibility with many
standard software products.**

The Neoverse N2 Reference Design implements the Neoverse CSS N2 with the
following configuration choices:

- **32 instances of the processor block—each including a single Neoverse
  N2 processor with a 64 kB private L1 I–cache, a 64 kB private L1
  D–cache, and a 1 MB private, unified L2 cache;**

- **a third–party DDR memory controller; and**

- **32 MB System Level Cache in the interconnect.**

<img src="./media/image7.png" style="width:6.26806in;height:3.8125in"
alt="A computer screen shot of a diagram Description automatically generated" />

Figure 2 – Neoverse N2 Reference Design

For readers with an interest in system-on-chip architecture, the final
chapter in this section contains a brief overview of many of the
connectivity components listed above.

This discussion won’t cover in detail the software running on any of the
support processors (SCP and MCP), nor the (rather complex) boot process
needed to get the device from power-on to a usable state running a Linux
kernel. Further detail about these topics, and the platform itself, can
be found on Arm’s website.[^12]

# 2. Security Considerations

Note: This section describes the Confidential Compute Architecture
(CCA). This technology has been developed by Arm<sup>®</sup> in recent
years and has been released to partners in the latest processor core
designs. CCA is supported by a range of software models upon which
software can be developed and tested. Wider market adoption of this
technology requires the coalition of many partners, including regulators
and service providers.

Security has become an increasingly important design consideration in
recent years. For the cloud computing industry, it has become a
foundational issue, chiefly for these reasons:

- Cloud resources are accessible from anywhere by anyone on the
  internet.

- The same physical resources are frequently shared by multiple users.

- Resources are often dynamically allocated on demand.

- Software uploaded and executed by users is generally not vetted.

The cloud computing industry requires systems to be accessible via the
internet. This introduces the risk of unauthorized access and use. These
open systems can no longer hide behind access restrictions—no matter how
sophisticated—and instead must incorporate robust protection against
misuse by potential malefactors who may have gained some level of access
to the system itself.

In a cloud computing environment, multiple users may be sharing access
to a single physical processor—or cluster of processors—running
arbitrary software that hasn’t been vetted. It is important to isolate
users from each other adequately, so that malefactors can’t prejudice,
interfere with, or observe the activities of other users on the same
system.

To address this, modern security architectures typically rely on some
form of “compartmentalization”. This ensures that if a malefactor does
gain access to the system in some way, the compartments restrict what
they can do once inside the system. This also protects against actions
by legitimate users of the system, who may—whether deliberately or
inadvertently—execute software that is prejudicial to other system
users.

Such compartmentalization architectures usually rely on hardware support
built into the processor itself. For example, Arm’s Confidential Compute
Architecture (CCA) is supported by the latest Armv9–A cores, and
TrustZone<sup>®</sup> is supported by all application–class cores since
Armv7–A.

However, not all software can run in such a compartmentalized
environment. In particular, code that is part of the boot process must
have essentially unfettered access to the system in order to initialize
hardware components, launch device drivers, and set up the secure
environment before it passes control to a hypervisor or one or more
operating systems. The hypervisor or operating systems are then
responsible for loading and launching applications in a secure and
protected manner to provide the necessary isolation. In any case, boot
code executes before any security systems have been initialized. We
shall look at the boot sequence in more detail.

Another important principle is the need to minimize the proportion of
the system that must be “trusted”. That minimal component can then be
tested and verified to a very high degree of assurance, upon which the
rest of the security rests.

In particular, it is important to recognize that common software
components—such as the operating system and hypervisor—cannot be trusted
to the same extent. They are simply too large and complex to be robustly
verified and certified.

Referring to the system structure shown in Figure 4, notice that the
entire Linux kernel, together with any application workloads running on
it, is regarded as untrusted and executes in the Non-Secure World.
Security architectures like CCA and TrustZone remove the need to trust
the operating system or hypervisor. Going beyond the separation provided
by TrustZone, Arm CCA allows the hypervisor to exert control over any
virtual machines but removes the right of access to any code, state, or
data information used by or within that virtual machine. This allows
developers to deploy workloads securely without needing to trust the
software infrastructure supporting them.

On the Application Processor (AP), only a small body of software—the
“Secure Runtime Services”—executes in the Secure World.

On systems that support RME (see Figure 4) the majority of the drivers,
together with the code responsible for switching between the Secure and
Non-Secure Worlds, are executed in Root state. User workloads can either
execute in the Non-Secure World on top of the Linux kernel, or in
compartmentalized realms in Realm state.

The following points are worth noting:

- A workload executing in a Realm is invisible not only to other
  workloads in Realm state but also invisible to the operating system.

- The body of software executing in Root and Secure states is small,
  bounded, and can be verified prior to execution.

- User–generated workloads, running in Realms, are isolated so that they
  can neither interact with each other nor with the rest of the system.

Hardware debug features must be carefully considered and controlled,
because they require extensive access to on-chip resources and internal
information. All Arm Neoverse™ Reference Designs implement some form of
debug authentication. This requires external debuggers to identify and
authenticate before the system will provide access to internal static
and dynamic information. The debug access to AP, MCP, and SCP are
separately authenticated. Some systems, including the Arm Neoverse
Reference Designs, internally disable some debug features if the
debugger cannot successfully be authenticated.

# 3. A Typical Software Stack

The software stack that executes on the Application Processor (AP)—the
Neoverse™ processor is only one part of the story, because the AP is
only one of several processors in the system. To support the AP,
management and control tasks are often delegated to support processors.
The example shown in Figure 3 shows a typical system configuration of an
Application Processor (AP), System Control Processor (SCP), and
Manageability Control Processor (MCP).

<img src="./media/image8.png" style="width:6.26806in;height:4.43264in"
alt="A screenshot of a computer program Description automatically generated" />

Figure 3 – High–level software illustration of a Neoverse Reference
Design.

The slightly more complex, example in Figure 4 shows the configuration
when Confidential Compute Architecture (CCA) is implemented. This
requires the addition of Realm Software (executing on the AP) to manage
the Realm Control Extension hardware.

<img src="./media/image9.png" style="width:6.26806in;height:2.77639in"
alt="A screenshot of a computer software Description automatically generated" />

Figure 4 – High–level software illustration of a Neoverse Reference
Design with RME.

The AP, SCP, and MCP are physically distinct processors—although in some
systems, a separate processor executes the Runtime Security Engine
functions. Each processor executes a separate software image and
communicates with other processors using on–chip interconnect pathways.
(The details of how this communication occurs and how it is implemented
need not concern us here.)

The distribution of tasks between these components is typically as
follows:

<table>
<colgroup>
<col style="width: 22%" />
<col style="width: 18%" />
<col style="width: 58%" />
</colgroup>
<thead>
<tr>
<th rowspan="3">Application Processor (AP)</th>
<th>Non–Secure</th>
<th><p>Workloads<a href="#fn1" class="footnote-ref" id="fnref1"
role="doc-noteref"><sup>1</sup></a></p>
<p>Operating system (typically Linux)<strong><sup>Error! Unknown switch
argument.</sup></strong></p>
<p>Hypervisor (typically KVM)</p>
<p>Boot loader (typically UEFI)</p>
<p>Non–trusted firmware</p></th>
</tr>
<tr>
<th>Secure</th>
<th><p>System boot code</p>
<p>Trusted boot firmware</p>
<p>Secure run–time services (including secure devices drivers and error
handlers)</p>
<p>EL3 secure run–time services</p></th>
</tr>
<tr>
<th>Realm</th>
<th>Realm Management Software</th>
</tr>
</thead>
<tbody>
<tr>
<td>Manageability Control Processor (MCP)</td>
<td>Non–Secure</td>
<td><p>Platform management functions</p>
<p>Peripheral drivers</p>
<p>System Control &amp; Management Interface (SCMI)</p></td>
</tr>
<tr>
<td>System Control Processor (SCP)</td>
<td>Secure</td>
<td><p>Power control</p>
<p>Hardware initialization</p>
<p>System clocks</p>
<p>On–chip interconnect</p>
<p>Memory controllers</p>
<p>PCIe controllers</p></td>
</tr>
<tr>
<td>Runtime Security Engine<a href="#fn2" class="footnote-ref"
id="fnref2" role="doc-noteref"><sup>2</sup></a> (RSE)</td>
<td>Secure</td>
<td><p>Boot control</p>
<p>Provisioning state machine</p></td>
</tr>
</tbody>
</table>
<section id="footnotes" class="footnotes footnotes-end-of-document"
role="doc-endnotes">
<hr />
<ol>
<li id="fn1"><p><sup>†† There may be multiple operating systems—each
running multiple workloads—under the control of a single hypervisor
running on the Application Processor.</sup><a href="#fnref1"
class="footnote-back" role="doc-backlink">↩︎</a></p></li>
<li id="fn2"><p><sup>In some systems, the functions of the RSE are
carried by the SCP. This simplifies the hardware architecture
somewhat.</sup><a href="#fnref2" class="footnote-back"
role="doc-backlink">↩︎</a></p></li>
</ol>
</section>

In general, the SCP handles internal monitoring, management, and
control, while the MCP handles the management connection with the world
outside the device, particularly the interface with the management
application in a server environment.

The software executing on these two processors is provided by the
equipment manufacturer and can generally be regarded as immutable by end
users. It is typically based on reference software provided by
Arm<sup>®</sup>.[^13]

We now look at the boot sequence—beginning from reset and typically
ending with the launch of the operating system.

# 4. The Boot Sequence: Hardware to Operating System

As might be expected, the boot sequence in a complex, multi-processor
system is inevitably intricate. It requires a chain of secure steps,
designed to give a high level of confidence in the security of the
running system. This is often referred to as the “Root of Trust”—just
like how trees are anchored into the soil by their root system. If you
sever the roots, the tree will die; if you break the “Root of Trust”,
the security of the entire system collapses.

As protection against malicious boot software, any boot code component
that is dynamically loaded is typically supplied in an encrypted form
and must be decrypted and verified before being executed. Each stage
carries out its designated functions before downloading the subsequent
stage, verifying it, and then transferring control to it. This approach
requires a tamper-proof mechanism for storing the necessary encryption
and validation keys.

Prior to the boot process, during chip and device manufacturing, a
separate provisioning process installs the chip and device keys,
configuration data, manufacturer keys, and information.[^14] The initial
boot code (BL1_1) is built into on-chip ROM during manufacturing; the
second stage boot code (BL1_2) is programmed into one-time programmable
(OTP) memory during device provisioning. This provisioning process is a
once-only, one-way process that installs code and keys so that they are
securely stored and cannot be subsequently changed.

Following provisioning, subsequent resets will start execution from the
on-chip secure boot ROM. The first stages are under the control of the
SCP and MCP, which validate their respective initial software images.
Once the MCP and SCP have started, the SCP boots the AP. All this takes
place initially on the primary CPU on the primary chip. Once it is
complete on that processor, secondary processors and chips are then
booted.

It is important to note that the entire process proceeds, step by step,
by loading and executing validated software images. The earliest of
these images are inserted during manufacture and are immutable
thereafter. This is the foundation of the “Root of Trust” mentioned
above. Similarly, at each stage, validation is carried out using
immutable keys, which are inserted during manufacture and are unique to
the device.

In overview, the sequence, shown in Figure 5, is as follows:

1.  **MCP and SCP**

<!-- -->

1.  MCP and SCP boot from their respective boot ROMs.

2.  MCP waits until the SCP has established PLL lock.

3.  MCP and SCP load images from on-chip RAM or off–chip flash into TCM.

4.  MCP and SCP validate the loaded images.

5.  MCP and SCP jump to TCM.

6.  MCP and SCP exchange keys to establish mutual trust before
    continuing.

7.  SCP enables the Application Processor’s clock circuits.

8.  SCP powers up one core (typically CPU0).

<!-- -->

2.  **Application Processor (AP)**

<!-- -->

1.  AP boots from the BL1 image in secure ROM.

<!-- -->

9.  AP BL1 loads and validates BL2 image from Flash, and transfers
    control to it.

10. AP BL2 loads and validates BL31 image from Flash, and transfers
    control to it.

11. Successful completion of BL31 boot signaled to SCP.

12. AP BL31 configures the interrupt framework, power management
    interface, and secure partition manager.

13. AP BL32 initializes Secure Partition Manager (EL3) and returns to AP
    BL31.

14. AP BL31 transfers control to UEFI (Non–secure EL2).

15. AP UEFI transfers control to the operating system (OS).

16. OS requests power-on of secondary CPUs on primary chip.

17. OS requests power-on of CPUs on secondary chip(s).

<img src="./media/image10.png" style="width:6.26806in;height:3.29097in"
alt="A diagram of a flowchart Description automatically generated" />

Figure 5 – Boot Sequence Flow Diagram

# 5. Device and Platform Discovery

It should be apparent by now that no two Neoverse™-based platforms are
the same! While this may sound like a disadvantage, this is a
manifestation of one of the key strengths of the Arm<sup>®</sup>
ecosystem. Since Arm’s silicon partners aren’t permitted to change the
behavior of the processor itself, nor the behavior of key peripherals
and on-chip infrastructure, the way these components function is
consistent across all Arm-based platforms based on any given version of
the architecture. Arm ensures this by insisting on compliance testing
for all products developed using Arm technology.

Beyond this, the licensee can introduce any amount of differentiation in
their end product. It is this differentiation that—for Arm’s
partners—represents a considerable benefit of using Arm technology.
Freed from the cost of developing their own processor and related
intellectual property (IP), they can concentrate resources on their own
product-specific IP. For end-users, the ability to rely on consistent
behavior across a huge range of very diverse products allows much more
efficient re-use of software, and better expertise across products,
companies, and industry sectors.

However, this diversity means that if a software product is used across
several platforms, it requires a method for determining the details of
the hardware on which it is executing, so that its behavior can be
tailored accordingly. At the most obvious level, this would include
device drivers, which will necessarily differ from platform to platform.

Fortunately, the industry has standard mechanisms for dealing with this.

The firmware—provided by a combination of Arm, device manufacturer,
product developer, and software developer—abstracts away the vast
majority of hardware specificity. This, on its own, means that most
software products will “just work” on a given Arm platform.

Firmware typically uses one of two methods for adapting to the hardware:

**Device Tree**  
This is a description of the hardware platform in a standard format.
This format is widely used by Arm-based Android devices, in embedded
development, and systems using the U–Boot. It is no longer widely used
for server-class deployments.

**Advanced Configuration & Power Interface (ACPI)**  
This is essentially an abstract description of the hardware, encoded in
a set of tables that contain information about the hardware itself, as
well as software elements (such as device driver components) that are
incorporated into the system at run time. ACPI tables are less
restrictive than Device Trees.  
  
Every device manufacturer produces a set of ACPI tables for their
platform, and these are in an industry-standard format. They are
particularly used by systems based on the UEFI standard.  
  
Initially developed for x86-based systems, ACPI has supported Arm
systems since 2011.

Of the two possibilities, ACPI is more common and more capable. It is
preferred by Arm and other major vendors of processor-based platforms,
and used by all the major Linux distributions. The format is governed by
the UEFI Forum.

Application software developers don’t need any knowledge of how this
system works. They can simply rely on the majority of system software
using it and therefore being usable across a wide range of
platforms—both Arm and non-Arm.

# 6. Operating Systems & Hypervisors

(For an updated list of software packages supported on Arm, refer to:
[https://www.arm.com/developer–hub/ecosystem–dashboard/servers–and–cloud–computing](https://www.arm.com/developer-hub/ecosystem-dashboard/servers-and-cloud-computing))

The majority of applications use a standard operating system. Although
other options are possible, this operating system will likely be some
form of Linux and we shall make this assumption for the remainder of
this discussion.

The choice of Linux distribution is not necessarily influenced by the
choice of an Arm-based platform. Since the majority of mainstream
distributions are supported on Arm, and have been for some time, there
is essentially the same choice for Arm developers as there is for users
of other architectures. The same criteria apply when choosing any
particular distribution: stability, middleware support, security
considerations, compatible development tools, commercial licensing
terms, etc.

It is important to remember that the operating system is not the only
software executing on the system. It relies upon layers of supporting
software which provide the interface between the platform and the
operating system kernel.

Bear in mind, also, that the Application Processor (AP) is not the only
component in the system that executes software. It relies on support
functions carried out by the SCP and MCP, which execute separate
firmware. The SCP is responsible for low-level system management, and
the MCP is responsible for manageability functions.

To recap the more detailed discussion in §4, the supporting firmware
executing on the AP—loading and supporting the operating system
kernel—includes:

- Arm Trusted Firmware BL1  
  BL1 is contained in an on–chip ROM, fixed at time of manufacture

- Arm Trusted Firmware BL2  
  BL2 is loaded from external non-volatile storage into on-chip RAM

- Arm Trusted Firmware BL31  
  BL31 manages the Power State Coordination Interface (PSCI), Secure
  monitor framework, and Secure partition manager

- Secure runtime services BL32\|  
  BL32 is runtime software that runs under the management of the Secure
  partition manager

- Bootloader BL33  
  BL33 is the final component in the boot sequence, typically a
  UEFI-compliant bootloader providing the interface between the firmware
  and the operating system

More information about these components can be found in the [Arm
Neoverse™ N2 Reference Design Technical
Overview](https://developer.arm.com/documentation/102337/latest/).

The Arm Neoverse N2 Reference Design Linux kernel is provided to
demonstrate the platform features, and does not implement sufficient
functionality for typical use cases. The rest of this section introduces
the Linux implementations that are likely to be found in widely
available Neoverse systems. You will need to check which kernels are
available for the particular platform that you plan to use.
Alternatively, if you have already selected a particular kernel, then
you will need to choose a platform on which it is supported.

All of these software components are available from the Reference Design
Github repository.[^15]

The main choice to make at this point is whether to use a
vendor-specific Linux distribution, or to use a cross-platform
distribution. We discuss both below. The choice is driven by one or more
of the following:

- **New or ported software**
  If you are porting an application from another platform, and your
  current distribution is supported on the destination platform, you may
  wish to retain the same Linux distribution to minimize disruption when
  porting.

- **Hardware support**  
  Applications that rely on particular hardware features that are
  present in only some platforms may wish to opt for a vendor-specific
  or platform-specific distribution in order to ensure the best and most
  up-to-date support for those features.

- **Licensing terms**
  Changing distribution will almost certainly involve changing supplier
  and adopting new commercial and licensing terms. If you are already
  using a particular distribution, sticking with it may be a sensible
  choice for this reason. If you are developing a completely new
  product, then this would not apply.

- **Stability and support**  
  Many developers opt for a longstanding and well-supported distribution
  from the open marketplace, in order to benefit from the stability that
  comes with maturity, and the support that comes with a commercial
  product. The cost is obviously weighed against the benefits here.

- **Ease of use and availability**
  Most device manufacturers and cloud hosting companies make a
  particular distribution, or a selection of distributions, available
  with their product. Choosing one of these is not just the “easy”
  option—these are likely to be supported directly by the supplier and
  be better targeted to their specific platforms. In particular, they
  will often be the first to support new features. Licensing and
  commercial terms for these platforms may also be simpler as they may
  be bundled with the terms for using the platform itself.

## 6.1 Cross–Platform: SUSE, Debian, RedHat, Ubuntu

On Microsoft Azure bare-metal instances, RedHat RHEL and Suse SLES are
the options for the operating system.

# 7. Middleware

In a typical software application development environment, middleware is
the glue that connects the applications to the operating system and the
underlying hardware capabilities. For example, middleware allows
applications written in different languages to communicate with each
other and to share common underlying services. Middleware largely hides
the details of the underlying platform from applications that wish to
use the services it provides.

<img src="./media/image11.png" style="width:6.26806in;height:1.69444in"
alt="A blue and yellow background with arrows AI-generated content may be incorrect." />Middleware
may be highly integrated and specific, such as a game engine that
provides audio, video, animation, and game-play services to a gaming
application. Or it may be fundamentally distributed and general-purpose,
such as a web server providing database services to front-end
applications that may be running on a different operating system on a
physically remote system. It may be as simple as a driver for a specific
type of hardware sensor, or as complex as a real-time, secure,
distributed transaction manager for a banking system.

Middleware can be described as the plumbing that allows disparate
software components to communicate with each other, while hiding the
details of how that communication actually happens.

Below are some examples of different kinds of middleware.

- **Database**
  A database access service (such as Hadoop or MySQL) allows
  applications to query a database using a standard query language, such
  as SQL.

- **Runtime Environment**
  Many programming languages (such as Python, Ruby or Java) need to
  execute in a standard environment at runtime. This environment makes
  available a standard set of services which the language needs.

- **Networking**
  Applications rarely run in complete isolation, and almost always need
  to communicate with other applications. They may be executing on the
  same platform, or on physically distinct and possibly remote
  platforms, on different processors. A networking layer (such as NFS or
  Cloudflare) provides these connection and data transport functions
  while hiding the underlying nature of the connection.

- **Security**
  For a variety of reasons, applications often need access to secure and
  standard means of encrypting data, either for local use or for
  transmission to other applications. Security middleware (such as
  OpenSSL or Bitdefender) handles this, as well as related functions
  such as key generation and secure key exchange.

The choice of middleware components can have significant effects on the
performance and functionality of the final system. The criteria for
choosing middleware on an Arm<sup>®</sup>–based platform are essentially
the same as for any other platform.

You should consider the following factors:

- **Commercial or non–commercial licensing terms**  
  This might include rights for redistribution, modification or re–use.

- **Platform support**  
  Not all middleware components are supported on all platforms, so the
  choice will be limited by what is available on your chosen platform.

- **Cost**  
  Licensing, use and distribution costs vary greatly between suppliers.
  The selection must fit the financial business case made for the
  application.

- **Compatibility**  
  Some components are incompatible with others, or are not supported on
  some operating systems. It can be complicated to choose a selection of
  components that are all compatible.

- **Support services**
  The availability and quality of support vary greatly across the
  industry. In general, commercial offerings will come with a level of
  support; FOSS offerings may not.

- **Functionality and performance**
  You should evaluate which options meet the required features at the
  needed performance level. These factors should be addressed in the
  application requirements specification.

# 8. Cloud–Native Tooling

In cloud–native development, applications are built in the cloud, to run
in the cloud. This requires that all the development tooling and
infrastructure be available in the same target cloud environment.

It was not always this way.

In the earliest days of computing, all development, integration, test,
debugging, and deployment took place on a single machine (or a single
type of machine). Since computers were large, rare, inflexible, and
extremely expensive, it was not generally feasible to develop
applications on one machine and deploy them on another. Applications
were developed on the machine on which they were deployed (or on an
identical machine, in the case of an application developed by a vendor
for deployment to a number of clients).

The advent of minicomputers and personal microcomputers changed this
paradigm and made the process more flexible and more efficient. Using
cross-compilers, it became possible for multiple developers to write
software on their own machines before components were compiled for the
target machine. Since the development and deployment machines were
usually of very different architectures, this meant that the deployed
software could not be executed on the development machines (without some
form of emulation).

These days, compute resources are provided in the cloud, and are
flexible, accessible, scalable, and easily manageable. It is again
possible to develop, integrate, test, and deploy in a single end-to-end
environment.

As well as convenience and efficiency of development, cloud-native has
other advantages.

**Greater reuse**—it is much easier and more efficient for multiple
applications to make use of common middleware and shared resources,
since all are in the cloud.

**Compartmentalization**—individual components can be individually
containerized, being connected via shared middleware into the complete
system. This makes it easier to isolate and fix problems, and enables a
divide-and-conquer approach to system design, performance optimization,
and scalability. To fix isolated problems, only the affected components
need to be replaced, and this can be done “in place”. Additionally,
components can be individually scaled to meet capacity requirements.

**Simplified supply chain**—with components being built to execute on
the same underlying platform, using the same middleware APIs, there is
less work involved to integrate components from a diverse supply chain.

**Scalability**—development resources can be provisioned and deployed
instantaneously as required, eliminating the need to purchase and
maintain expensive development platforms.

**Reduced Development Cost**—without the need to purchase and maintain
development kit in the locations where developers are working,
development time and cost are reduced.

**High Availability and Resilience**—it is no longer the job of the
developer to maintain access to developer hardware. The cloud vendor is
responsible for making the agreed resources available, at the agreed
time, with the agreed service level. This reduces risk for developers.

**Reproducibility**—technologies such as Docker allow software to be
developed and executed within containers. These containers can then be
perfectly reproduced on the target platform. This allows software to be
tested on the local platform in an environment that perfectly matches
the target environment where the software will be executed.

Further, a modern DevOps (CI/CD) development flow relies on a high
degree of automation throughout the develop–integrate–deploy–test cycle.
Clearly, it would be simpler and more efficient if all the necessary
automation tools are available in the same development environment,
executing on the same platform.

While there are many options for suites of automation tools, many are
well supported on Arm platforms, including Git, Docker, Kubernetes,
Splunk, Nagios, Datadog, Maven, Jenkins, and many more.

# 9. Applications

There are two main routes that developers might take when seeking to
deploy an application on an Arm-based Neoverse™ platform. First,
development of a new application specifically targeted at Neoverse.
Second, porting of an existing application from another architecture.

In the case of developing from scratch for Neoverse, the preceding
discussions will help with selecting the right platform, choosing an
operating system, integrating middleware, and finding and deploying the
appropriate tooling for your development.

If you are porting from another architecture, there are some additional
considerations to bear in mind.

**Arm is a widely supported compiler target**

Development for Arm is mainstream now, and the majority of compilers and
related development tools support Arm as a target architecture. When
specifying your target platform, it is important to be as specific as
possible. There are two reasons for this.  
  
Firstly, each new version of the Arm architecture introduces new
features and enhancements—from new instructions to entirely new
capabilities such as CCA. In order to make full use of the features of
your chosen platform, you need to specify it as accurately as possible.
If you specify the basic architecture version, such as Armv9–A, you can
rely on newer features as well as the core architecture. If possible, be
even more specific and specify the exact version, e.g. “Armv9.1–A”.  
  
Second, processors that implement the same version of the architecture
(and thus execute the same instruction set with identical functionality)
may do so using differing internal microarchitectures. This may include
differences in pipeline structure, cache architecture, memory interface
speed and bandwidth, and on-chip interfaces. Without details of this
information, the compiler cannot optimize for greatest instruction
throughput, for instance, nor lay out data structures for either lowest
memory use or greatest speed of access. So, specifying the exact
processor is the best option, e.g. “Neoverse N2”.

**Nearly all mainstream libraries and components are available on Arm**

Given the wide support for Arm, your choice of libraries and middleware
is likely to be available. Therefore, consider which ones have been
optimized for your target platform, which are available on suitable
licensing and commercial terms, and which might be better supported by
your chosen cloud service provider.

**Watch out for hardware–specific software elements**

Applications originally written for other architectures may make use of
machine-specific features. The most obvious example of this would be
modules that make use of a specific instruction set via intrinsic
functions or inline assembly language. This is often done to access
instructions that the compiler cannot emit, or which it cannot utilize
efficiently. Such sections will clearly need to be either removed,
rewritten, or substituted with a suitable library.

**Be aware of the flexibility in the Arm memory model**

Arm processors, since Armv7, implement a “weakly ordered” memory model.
This is essential for highest performance, as it allows the compiler and
the machine to re-order memory accesses to maximize instruction
throughput and make the most efficient use of available memory
bandwidth. At the microarchitecture level, the processor pipeline has
significant freedom to reduce, and even eliminate, instruction
dependencies and data dependencies in the instruction stream. This is
often highly specific to the exact processor being used—hence the advice
above to specify the processor as exactly as possible.  
  
So it is important to ensure that appropriate memory areas are used for
specific purposes, For example, memory-mapped hardware devices must be
placed in Device memory; for efficient execution, executable code must
be placed in Normal memory.[^16] The correct use of the “volatile”
keyword in C is particularly important when accessing devices or shared
memory areas.  
  
It is important to ensure that any memory regions in which access order
is important (including devices, semaphores, mutexes, and shared message
buffers) are carefully and correctly classified.  
  
The issue of “atomicity” needs careful consideration if necessary.

**Don’t be caught out by differences such as arithmetic rounding and
precision**

While processors of different architectures often contain instructions
that carry out the same basic function, such as floating-point
multiplication, the exact way in which these behave in corner cases may
differ. There are, for instance, various different strategies for
arithmetic rounding: towards zero; to the nearest integer; or towards
infinity. This can lead to different results from arithmetic
calculations, especially when intermediate results are involved! For
instance, a particular instruction sequence might or might not round
intermediate results while performing an algorithm.  
  
Additionally, the precision of the variables and the functionality of
the instructions may result in different results.  
  
Read the specification carefully and test your calculations.

In reality, there are almost no major wheels which you need to
re-invent, due to the wide range of tried and tested libraries and
middleware components already available for Arm, so don’t waste time
writing or re-writing any code that is already available from an
existing source.

And, like a good software eco-warrior, always Reuse and Re-cycle!

This is where the scope of this text draws to a close and gives way to
the extent of your imagination!

# 10. System–on–chip Components

This section contains a brief overview of some of the system-on-chip
components that are included in the Neoverse<sup>™</sup> N2 Reference
Design. A detailed understanding of how these functions work, and the
reason for which they are included, is not required when working with
application-level workloads. Their initialization, configuration and
management are handled entirely by software executing either on the SCP
or within the software stack on the AP—but this may be of interest to
some readers.

## 10.1 Generic Interrupt Controller (GIC–700)

The interrupt logic is based on the Arm<sup>®</sup> Generic Interrupt
Controller (GIC–700) and supports the management and distribution of
interrupts. It handles Shared Peripheral Interrupts (SPIs),
Locality-Specific Peripheral Interrupts (LPIs), Private Peripheral
Interrupts (PPIs), Message-Signalled Interrupts (MSIs), and
Software-Generated Interrupts (SGIs).

The architecture is distributed, providing private and common interrupt
resources to all the processors in the system. The interface is fully
virtualized, allowing interrupts to be delivered to virtualized
workloads without the intervention of the hypervisor.

The distributed architecture of the GIC–700 consists of a group of
centralized components, together with a set of distributed components
that are replicated for each core (or cluster of cores) in the system.
The central components consist of a single Distributor (GICD), an
Interrupt Translation Service (ITS) to translate message-based
interrupts from external sources such as PCIe Root Complexes, and a SPI
Collator.

For each core (or cluster of cores), a GIC Cluster Interface
(GCI)—sometimes called a Redistributor—manages PPIs and SGIs. The
distributed GCIs can be powered down, along with their associated cores,
separately from the GICD. They also connect to the System Control
Processor to support wake-up signaling when powering up individual
cores.

## 10.2 System Memory Management Unit (MMU–700)

In a virtualized system, each core in the system may have its own
virtual address space, and each application running on each core may, in
turn, have its own virtual address space. All these separate virtual
address spaces need to be mapped to a single physical address space,
which is used to access shared and external components. Such a system
involves frequent context switches between the different addresses when
switching between processors and between workloads on each processor.
These switches involve considerable configuration overhead. Without some
mitigation, these would absorb a significant proportion of system
performance. A System Memory Management Unit is designed to overcome
this specific problem.

The System Memory Management Unit (MMU–700) allows fully virtualized
access to peripherals. The unit contains distributed address translation
logic, which allows peripherals to be accessed using virtual addresses
simultaneously in different contexts. This removes the need to
reconfigure the system address translation regime when switching between
virtualized workloads, and allows multiple cores to access shared
peripherals simultaneously without the need to reprogram address
translations for each context.

The MMU–700 consists of two main components: a Translation Control Unit
(TCU); and one or more Translation Buffer Units (TBUs).

The TCU controls and manages the process of address translation. The TCU
is responsible for accessing (walking) translation tables in system
memory to retrieve translation information when required. The TCU
contains internal caches for recently used translation information in
order to reduce the number of page table accesses required.

Each TBU carries out the address translations. When a TBU receives a
request for an address translation, if possible it performs the
translation using configuration cached in its internal Translation
Look–Aside Buffers (TLBs). If it does not find a matching cached
translation, it requests the TCU to retrieve one. Each TBU may be
connected to one or more external bus masters. To improve performance in
individual cases, more than one TBU may be connected to a single master.

## 10.3 Network Interconnect (NI–700)

The NI–700 Network Interconnect is a highly-configurable, high
frequency, low latency on-chip system-level interconnect, capable of
connecting across power and clock domain crossings. In the Neoverse N2
Reference Design, the NI–700 connects to the external I/O masters and
provides expansion interfaces for CMN–700.

## 10.4 Coherent Mesh Network (CMN–700)

CMN–700 is a mesh-based coherent interconnect with multi-chip support
using the CCIX standard. The mesh architecture supports high bandwidth
data transfer between system components. It supports data coherency
across the system, allowing greater and more efficient utilization of
private and shared caches.

CMN–700 is specifically designed and proportioned to meet the needs of
compute platforms used in high-end networking and enterprise compute
applications.

The basic structure deployed by CMN–700 is of a rectangular network of
Crosspoints (XPs). XPs are connected in two dimensions to other XPs in a
mesh structure. The number of XPs and the vertical and horizontal
dimensions of the mesh are configurable. In the mesh, each XP is
connected to up to six other devices: XPs in the inner part of the mesh
connect to four neighboring XPs and up to two devices; XPs on the edge
of the mesh connect to three neighboring XPs and up to three devices;
XPs at the corner of the mesh connect to two neighboring XPs and up to
four devices.

Certain nodes within the mesh may incorporate parts of the system-wide
cache. This is a “last-level” cache, and it is coherent across the mesh.

Other nodes may connect variously to I/O coherent AMBA devices,
ACE5–Lite devices, PCIe subordinates, or Coherent Multichip Link (CML)
interfaces.

CMN–700 can be configured with multiple asynchronous clock domains.

## 10.5 Network Interconnect (NIC–450)

The NIC–450 Network Interconnect is a library of components that can be
used to build a scalable and configurable network-on-chip interconnect.
At its heart is the NIC–400 interconnect, consisting of switches,
bridges and interface blocks that can be used to connect bus masters and
slaves in a cascading, switched network. It supports a variety of AMBA
protocols.

In the Neoverse N2 Reference Design, the NIC–450 connects to system
peripherals, other on-chip components, and other subsystem components.
Unlike the CMN–700, NIC–450 is not a coherent interconnect.

## 10.6 Dynamic Shared Unit (DSU)

The Dynamic Shared Unit (DSU) provides connection from a single core, or
cluster of cores, into the rest of the system. Highly configurable, it
provides an optional shared L3 system cache, snoop control and coherency
logic, power control, together with a suite of coherent and non-coherent
bus master interfaces, and debug logic.

Although the DSU is capable of hosting a number of cores in a coherent
cluster, in the Neoverse N2 Reference Design it is configured in “Direct
Connect” mode. In this mode, it hosts only a single core, and the
optional L3 cache (together with the associated snoop control and
coherency logic) is not implemented. Instead, the core is connected
directly into the on-chip interconnect, via a bridge, and to the shared,
coherent L3 cache within the CMN–700. This configuration not only
reduces on-chip area but also reduces latency for transactions between
the core and the interconnect.

The DSU also supports the Realm Management Extension (RME) security
architecture.

[^11]: <sup>“Cloud–native” refers to a development environment in which
    the development tools (compilers etc) execute on the same, or an
    identical, platform to which the developed application will be
    deployed.</sup>

[^12]: <sup>[https://neoverse–reference–design.docs.arm.com/en/latest/about/software_stack.html](https://neoverse-reference-design.docs.arm.com/en/latest/about/software_stack.html)</sup>

[^13]: <sup>While Arm provides implementations of these components as
    part of its Reference Designs, this software should not be treated
    as of “production quality”. It is intended merely as an example for
    device manufacturers.</sup>

[^14]: <sup>This is analogous to the storage of keys in external Trusted
    Platform Modules, a technique used in many system
    architectures.</sup>

[^15]: <sup>As “Reference Designs” these should be treated as examples
    rather than production–ready software. Device and platform
    manufacturers will have their own implementations of this
    functionality which will be distributed with those devices and
    platforms.</sup>

[^16]: <sup>For a discussion of the different types of memory and their
    associated properties, see Chapter B2 in the Arm Architecture
    Reference Manual for A–profile architecture (ARM DDI 0487K). The
    discussion there is highly technical!</sup>



