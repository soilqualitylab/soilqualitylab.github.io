# **100 Module Plan: Developing Minimalist CloudKernel for AI/ML Acceleration**

The proliferation of artificial intelligence and machine learning (AI/ML) has placed unprecedented demands on computing infrastructure. While hardware accelerators like GPUs have become the cornerstone of AI/ML computation, the operating systems that manage them remain largely general-purpose. Traditional OS kernels, designed for multitasking and fairness in interactive environments, introduce overheads—such as context switching, complex scheduling, and broad system call interfaces—that are often unnecessary for the dedicated, high-throughput workloads characteristic of AI/ML training and inference.1 This creates an opportunity for a paradigm shift: the development of a specialized, minimalist kernel architected from first principles to serve a single purpose—hosting AI/ML containers with maximum efficiency.

This document outlines an exhaustive, year-long, 100-module course designed for advanced systems engineers and researchers. The curriculum guides the student through the complete, from-scratch development of such a kernel. The objective is not merely to build an operating system, but to create a highly optimized, vertically integrated software stack. This includes a bare-metal kernel written in Rust, deep integration with NVIDIA CUDA and AMD ROCm GPU hardware at the driver level, a bespoke compiler toolchain based on modern MLIR infrastructure, and a container runtime tailored for AI/ML applications. Each module is designed to require 10-15 hours of intensive, hands-on effort, progressing from foundational bare-metal programming to the deployment of a custom kernel in a cloud environment. The final product will be a testament to low-level systems engineering: a kernel that sheds the legacy of general-purpose computing to provide a lean, powerful, and transparent foundation for the next generation of intelligent systems.

---

## **Part I: Foundations of Low-Level Systems and Kernel Bootstrapping (Modules 1-12)**

This foundational part establishes the philosophical and technical groundwork for the entire course. It moves from the "why" of building a minimalist kernel to the "how" of writing the very first lines of code that will execute on bare metal. The initial modules are dedicated to architectural decisions, toolchain setup, and understanding the hardware platform, culminating in a bootable, "hello world" kernel.

### **Section 1.1: The Minimalist Kernel Philosophy: Unikernels vs. Microkernels vs. Monolithic (Modules 1-3)**

The course begins by deconstructing the architectural trade-offs of different kernel designs to justify the selection of a specialized model for AI/ML workloads. Monolithic kernels, like Linux, integrate all services into a single address space for performance but suffer from complexity and a large attack surface. Microkernels prioritize isolation and modularity by moving services into user space, often at the cost of performance due to increased inter-process communication.

This course will pursue a unikernel-inspired, library-OS model. Unikernels are specialized, single-address-space machine images constructed by linking application code with only the necessary kernel libraries, resulting in extremely small, fast-booting, and efficient virtual machines.2 Projects like Unikraft and Nanos demonstrate this philosophy, offering POSIX- and Linux-compatible interfaces to ease application porting.4 However, these projects also highlight the primary challenge of our endeavor: integrating complex, proprietary device drivers. The effort to support NVIDIA GPUs in the Nanos unikernel, for instance, required a painstaking re-implementation of numerous Linux kernel internal features, including waitqueues, radix trees, custom

mmap callbacks, and synchronization primitives.5 This reveals an architectural paradox central to this course: while the core kernel can be minimalist, the GPU driver subsystem it must host is inherently monolithic and complex. Therefore, the kernel we build will be a "bimodal" system—a minimal core OS co-located with a highly complex driver subsystem that necessitates a significant, Linux-like ABI. This is not a failure of the minimalist philosophy but a pragmatic acknowledgment of the realities of supporting high-performance, proprietary hardware.

Furthermore, we will examine forward-looking concepts like "AI-aware" kernels, which propose integrating deep learning models directly into the kernel as Loadable Kernel Modules (LKMs) for ultra-low-latency processing.1 While our immediate goal is to efficiently

*host* AI containers, these advanced concepts will inform our design, encouraging an architecture that minimizes the user-kernel boundary wherever possible.

**Module Breakdown:**

* **Module 1: Kernel Architectures.** Analysis of monolithic, microkernel, and unikernel designs. A case study on the performance and security characteristics of each.  
* **Module 2: The Library OS Model for AI/ML.** Justifying the choice of a unikernel-inspired architecture. A deep dive into the Nanos GPU driver porting effort as a case study on the challenges of driver compatibility.5  
* **Module 3: The AI-Native Kernel Concept.** Exploring academic research on integrating AI directly into the kernel space.1 Defining the scope of our project as a high-performance host, with an eye toward future AI-native optimizations.

### **Section 1.2: Bare-Metal Development with Rust: no\_std, Core Primitives, and Unsafe Code (Modules 4-6)**

Rust is selected as the implementation language for its unique combination of performance, comparable to C/C++, and strong compile-time safety guarantees that eliminate entire classes of bugs like dangling pointers and data races.8 A key feature for OS development is Rust's standard library structure, which is split into

core and alloc. The core library contains platform-independent primitives and can be used in a "freestanding" (\#\!\[no\_std\]) environment without an underlying OS, which is precisely our starting point.9

This section focuses on the practicalities of bare-metal Rust. While the ownership model provides safety, kernel development inherently requires unsafe operations: direct memory-mapped I/O, manipulation of page tables, and handling raw pointers for DMA. A naive approach would wrap large sections of the kernel in unsafe blocks, negating Rust's benefits. The correct approach, and a central pedagogical theme of this course, is to master the art of building *safe abstractions over unsafe operations*. We will study patterns where minimal, well-documented unsafe code is encapsulated within a module that exposes a completely safe public API. This pattern is crucial for building a robust and maintainable kernel.

The curriculum will follow the initial steps laid out in the "Writing an OS in Rust" blog series, beginning with the creation of a freestanding binary.10 Students will set up the development environment using

rustup to manage toolchains and cargo as the build system and package manager.11 We will configure a custom cross-compilation target and survey essential libraries from the Rust OSDev ecosystem, such as the

x86\_64 crate for direct access to CPU instructions and registers, and the spin crate for basic synchronization primitives.9

**Module Breakdown:**

* **Module 4: The Rust Programming Model for Systems.** Introduction to ownership, borrowing, and lifetimes. Setting up a no\_std project.  
* **Module 5: Encapsulating Unsafe Code.** Best practices for using the unsafe keyword. Building safe abstractions for hardware interaction, such as a safe VGA text buffer writer.10  
* **Module 6: The Rust OSDev Ecosystem.** Toolchain setup for cross-compilation. Introduction to cargo, xargo, and key crates like x86\_64, bootloader, and spin.9

### **Section 1.3: The x86\_64 Architecture: Boot Process, Memory Models, and CPU Modes (Modules 7-9)**

A deep, non-negotiable dive into the fundamentals of the x86\_64 architecture is essential before writing any kernel code. This section covers the complete boot sequence, from power-on to the point where a bootloader hands off control to a kernel. We will examine the transition of the CPU through its various operating modes: starting in 16-bit Real Mode, transitioning to 32-bit Protected Mode, and finally entering 64-bit Long Mode, which is where our kernel will operate.

Key architectural concepts such as memory segmentation and the crucial role of paging for virtual memory will be introduced. We will study the Global Descriptor Table (GDT) and the structure of multi-level page tables. The primary hands-on platform for this section will be the QEMU emulator, which provides a flexible and debuggable environment for testing our kernel without risk to the host machine.12 Students will learn the basic QEMU command-line options for booting a kernel image, providing an initial RAM disk (

initrd), and passing kernel command-line arguments, such as console=ttyS0 to redirect console output to the terminal.12 This practical experience with QEMU provides the necessary context for understanding why bootloader tools and specific image formats are required.

**Module Breakdown:**

* **Module 7: The x86\_64 Boot Sequence.** From BIOS/UEFI to the bootloader. Understanding the roles of the MBR, VBR, and the GRUB bootloader.  
* **Module 8: CPU Operating Modes and Segmentation.** Real Mode, Protected Mode, and Long Mode. Setting up a Global Descriptor Table (GDT).  
* **Module 9: Introduction to Paging.** The concept of virtual memory. The structure of 4-level page tables on x86\_64. The role of the CR3 register.

### **Section 1.4: Bootstrapping the Kernel: From Bootloader to the main Function (Modules 10-12)**

This section bridges the gap between the low-level, assembly-language world of the bootloader and the high-level Rust code of our kernel. Students will write the kernel's initial entry point in assembly, responsible for setting up a temporary stack and loading the GDT. This assembly code will then perform the crucial task of calling the first function written in Rust.

Once in Rust, we will parse the boot information passed by the bootloader, which typically includes a memory map detailing usable and reserved physical memory regions. This information is vital for initializing our memory manager in the next part. The final goal of this section is to create a bootable disk image that QEMU can execute, which successfully transitions into our Rust code and prints a "Hello, world\!" message to the VGA buffer or serial console.10

Debugging is introduced as a core practice from the very beginning. We will leverage QEMU's built-in GDB server, using the \-s and \-S flags to halt the virtual machine at startup and allow a GDB client to connect.12 This enables single-stepping through the earliest assembly and Rust instructions, providing invaluable insight into the boot process and a powerful tool for troubleshooting.

**Module Breakdown:**

* **Module 10: The Kernel Entry Point.** Writing the initial assembly code to set up a stack and transition to Long Mode.  
* **Module 11: The First Rust Code.** Calling a Rust function from assembly. Parsing bootloader information (e.g., Multiboot2 or Limine protocol).  
* **Module 12: Creating a Bootable Image and Debugging.** Using the bootloader crate to create a bootable disk image. A hands-on lab on debugging the boot process with QEMU and GDB.12

---

## **Part II: Core Kernel Subsystems (Modules 13-30)**

With the kernel successfully booting, this part focuses on constructing the essential subsystems that form the backbone of any modern operating system: memory management, scheduling, and interrupt handling. The design and implementation of these components will be guided by the principle of minimalism, tailored specifically for the single-purpose, high-performance demands of an AI/ML workload.

### **Section 2.1: Physical and Virtual Memory Management (Modules 13-18)**

This section covers the implementation of a complete memory management subsystem from the ground up. We will begin by creating a physical frame allocator, which is responsible for tracking the usage of physical memory frames. Students will implement a bitmap-based allocator using the memory map provided by the bootloader.

Next, we will build the virtual memory manager, which involves creating and manipulating the x86\_64 multi-level page tables. A critical focus of this implementation will be first-class support for **HugePages** (2MB and 1GB pages). For AI/ML workloads that operate on gigabytes of contiguous tensor data, the standard 4KB page size is a significant performance bottleneck. A large tensor can require hundreds of thousands of Translation Lookaside Buffer (TLB) entries, leading to frequent and costly TLB misses and page walks.14 By using 2MB HugePages, the number of required TLB entries can be reduced by a factor of 512, dramatically improving memory access performance. Consequently, our kernel's memory manager will be architected with a "fast path" for HugePage allocations, treating them as the default for large requests rather than an exotic optimization.

Finally, we will implement a kernel heap allocator, following the patterns established in the os.phil-opp.com series.10 This will enable dynamic memory allocation within the kernel itself, using the

alloc crate, which is essential for managing kernel data structures whose size is not known at compile time.

**Module Breakdown:**

* **Module 13: Physical Memory Management.** Implementing a frame allocator using a bitmap to manage the physical memory discovered at boot.  
* **Module 14: Paging and Virtual Address Spaces.** Implementing the data structures for 4-level page tables. Creating a new, clean page table for the kernel.  
* **Module 15: Mapping Physical to Virtual Memory.** Writing functions to map physical frames to virtual pages and translate virtual addresses to physical addresses.  
* **Module 16: HugePage Support.** Extending the page table manager to support 2MB pages. Modifying the frame allocator to efficiently find contiguous blocks of physical memory.  
* **Module 17: Kernel Heap Allocator.** Implementing the GlobalAlloc trait. Creating a heap region in virtual memory and backing it with physical frames.  
* **Module 18: Advanced Allocator Designs.** Exploring and implementing more sophisticated heap allocators, such as a linked-list allocator or a fixed-size block allocator.

### **Section 2.2: The Scheduler and Concurrency (Modules 19-24)**

This section focuses on designing and implementing a scheduler and concurrency primitives. The target workload—a single, long-running AI/ML container—does not require the complexity of a preemptive, multi-user, fairness-oriented scheduler found in general-purpose operating systems like Linux. Instead, we can build a much simpler and more efficient scheduler tailored to our needs.

We will begin by implementing a basic cooperative scheduler, where tasks voluntarily yield control of the CPU. This model is sufficient for managing the main application thread, potential background threads for I/O, and dedicated threads for submitting commands to the GPU. The modern async/await feature in Rust will be introduced as a powerful and elegant way to implement cooperative multitasking, allowing for the creation of asynchronous tasks and a simple executor to run them.10

We will then implement the foundational components for kernel-level concurrency, including context switching and kernel threads (kthreads). This will be complemented by the implementation of essential synchronization primitives, such as spinlocks and mutexes, using the spin crate and atomic CPU instructions to ensure safe access to shared data structures in a multi-core environment.9

**Module Breakdown:**

* **Module 19: Introduction to Scheduling.** Concepts of cooperative vs. preemptive multitasking. Designing a simple round-robin scheduler.  
* **Module 20: Context Switching.** Saving and restoring CPU state (registers, instruction pointer, stack pointer). Writing the context switch function in assembly.  
* **Module 21: Kernel Threads.** Implementing a kthread API to create and manage kernel-level threads of execution.  
* **Module 22: Synchronization Primitives.** Implementing spinlocks and mutexes for mutual exclusion.  
* **Module 23: Cooperative Multitasking with async/await.** Deep dive into Rust's Future trait and the state machine transformation.  
* **Module 24: Building a Kernel Executor.** Implementing a basic executor to poll and run asynchronous tasks within the kernel.

### **Section 2.3: Interrupt and Exception Handling (Modules 25-27)**

A robust interrupt and exception handling mechanism is critical for any stable operating system. This section covers the creation of an Interrupt Descriptor Table (IDT), which is the CPU's mechanism for dispatching interrupts and exceptions to their corresponding handler functions.

Students will write handlers for critical CPU exceptions, such as page faults and double faults. The page fault handler, in particular, is a cornerstone of the memory management system and will be essential for later implementing advanced features like demand paging and GPU Unified Memory. Handling double faults correctly is vital to prevent a system reset caused by a fatal triple fault.10

We will also implement support for hardware interrupts. This involves programming the legacy Programmable Interrupt Controller (PIC) or the modern Advanced Programmable Interrupt Controller (APIC) to receive signals from external hardware devices. As practical examples, we will configure a programmable interval timer (PIT or HPET) to generate periodic timer interrupts, which can be used as a basis for preemptive scheduling later, and handle interrupts from a PS/2 keyboard controller to receive user input.

**Module Breakdown:**

* **Module 25: CPU Exceptions.** Setting up the IDT. Implementing handlers for common exceptions like breakpoint and invalid opcode.  
* **Module 26: Page Faults and Double Faults.** Writing a sophisticated page fault handler. Implementing an Interrupt Stack Table (IST) to handle double faults safely.10  
* **Module 27: Hardware Interrupts.** Programming the PIC/APIC. Handling timer and keyboard interrupts.

### **Section 2.4: System Calls and A Rudimentary Filesystem (Modules 28-30)**

This section establishes the boundary between the kernel and the user-space application it will host. We will implement a basic system call interface using the syscall and sysret instructions on x86\_64. This allows the application, running in a lower privilege level (Ring 3), to request services from the kernel (running in Ring 0).

Drawing inspiration from the POSIX-compatibility layers of unikernels 4, our goal is not to replicate the entire Linux syscall API. Instead, we will implement only the minimal subset of syscalls strictly necessary for our target AI/ML runtime. This will include fundamental calls for memory management (

mmap), file operations (open, read, write), and basic process control.

To support these file operations, we will create a minimal, in-memory filesystem, similar to a Linux initramfs. This filesystem will be bundled into the kernel image at build time and will contain the AI/ML application binary, its dependencies, and any necessary configuration files. This approach avoids the complexity of implementing a full block device driver and on-disk filesystem, adhering to our minimalist design philosophy.

**Module Breakdown:**

* **Module 28: The System Call Interface.** Using the syscall/sysret instructions. Designing a system call table and dispatch mechanism.  
* **Module 29: Implementing Core System Calls.** Hands-on implementation of a minimal set of POSIX-like syscalls (mmap, open, read, etc.).  
* **Module 30: Initial RAM Disk (initramfs).** Creating a CPIO archive containing the application filesystem. Modifying the kernel to mount and read from this in-memory filesystem at boot.

---

## **Part III: The GPU Subsystem: A Deep Dive into NVIDIA CUDA (Modules 31-45)**

This part is a cornerstone of the course, shifting focus from general OS principles to the highly specialized domain of GPU acceleration. We will dissect the NVIDIA CUDA software stack and build the kernel components necessary to communicate with an NVIDIA GPU. This endeavor involves creating a custom, minimal driver that interfaces with NVIDIA's existing OS-agnostic components, effectively replacing the Linux-specific portions of the official driver.

### **Section 3.1: Deconstructing the CUDA Stack: Runtime vs. Driver API (Modules 31-33)**

The course begins this section with a thorough analysis of the CUDA software stack architecture. A key distinction is made between the high-level CUDA Runtime API and the lower-level Driver API.16 The Runtime API (e.g.,

cudaMalloc, cudaLaunchKernel) offers a simpler, single-source programming model, while the Driver API (e.g., cuMemAlloc, cuLaunchKernel) provides more explicit control over contexts and devices. We will trace the execution flow of a simple CUDA application, from the user-space API call down through the layers to the eventual interaction with the kernel-mode driver.

A critical component of this ecosystem is the nvcc compiler driver.17 We will study its two-phase compilation process: first, compiling CUDA C++ source code into PTX (Parallel Thread Execution), a virtual, assembly-like instruction set architecture. Second, compiling the PTX code into SASS (Shader Assembly), the architecture-specific binary code. To support forward compatibility, applications are often packaged as "fat binaries," which embed PTX code alongside binary code for several GPU architectures. The CUDA driver can then just-in-time (JIT) compile the PTX for a newer, unknown GPU, or directly load the appropriate binary if available.17 Understanding this compilation and loading process is crucial, as our kernel will ultimately be responsible for managing and loading this code onto the GPU. The canonical CUDA processing flow—copy data from host to device, CPU initiates kernel launch, GPU cores execute in parallel, copy results back—will serve as our guiding mental model.16

**Module Breakdown:**

* **Module 31: CUDA Architecture Overview.** The CUDA programming model: grids, blocks, threads. The hardware model: Streaming Multiprocessors (SMs) and CUDA cores.19  
* **Module 32: Runtime and Driver APIs.** A comparative analysis of the two APIs. Tracing API calls using standard tools.  
* **Module 33: The CUDA Compilation Toolchain.** Understanding nvcc, PTX, SASS, and the structure of fat binaries.17

### **Section 3.2: The NVIDIA Kernel-Mode Driver: Architecture and Open Modules (Modules 34-36)**

Here, we delve into the architecture of the official NVIDIA Linux driver. It is not a single entity but a collection of kernel modules, primarily nvidia.ko (the core driver), nvidia-uvm.ko (for Unified Virtual Memory), nvidia-drm.ko (for display), and nvidia-modeset.ko.20 Our focus will be on the compute-related modules.

A significant development that enables this course is NVIDIA's release of open-source kernel modules.21 We will perform a detailed analysis of this source code. The most important architectural pattern to understand is the separation between the "OS-agnostic" component and the "kernel interface layer." The OS-agnostic part contains the bulk of the driver's logic and is distributed as a pre-compiled binary object (e.g.,

nv-kernel.o\_binary). The kernel interface layer is a smaller, source-available component that acts as a shim, translating Linux kernel API calls and data structures into a form the OS-agnostic blob understands.21 This architecture provides a clear blueprint for our custom driver: our task is not to rewrite the entire driver, but to implement a

*new* kernel interface layer that connects NVIDIA's binary blob to *our* kernel's internal APIs (for memory allocation, interrupts, etc.), effectively replacing the Linux-specific shim. We will use the official build guides as a reference for understanding the compilation process and dependencies.22

**Module Breakdown:**

* **Module 34: Anatomy of the NVIDIA Linux Driver.** The roles of nvidia.ko, nvidia-uvm.ko, and other modules.  
* **Module 35: Source Code Analysis of Open Kernel Modules.** A guided tour of the open-gpu-kernel-modules repository.21  
* **Module 36: The OS-Agnostic vs. Kernel Interface Layer.** Understanding the shim architecture and its implications for porting the driver to a new kernel.

### **Section 3.3: The User-Kernel Interface: ioctl and GPU Command Submission (Modules 37-39)**

This is the heart of the driver implementation. The primary communication mechanism between the user-space CUDA libraries and the kernel-mode driver in Linux is the ioctl system call, performed on special device files like /dev/nvidiactl and /dev/nvidia0. While the specific ioctl command codes and their associated data structures are not publicly documented by NVIDIA, their functionality can be inferred from the services the driver provides and by analyzing the open-source interface layer.

These ioctls are responsible for all fundamental GPU management tasks: creating and destroying GPU contexts, managing the GPU's virtual address space, allocating and freeing device memory, mapping memory for host access, and, most importantly, submitting kernels for execution.25 The driver's responsibilities include managing the JIT compilation of PTX, scheduling the execution of kernel grids on the device's SMs, and handling the complex state of the GPU.25 By studying the functions exported by the kernel interface layer and how they are called in response to file operations, we can piece together a functional understanding of this critical boundary.

**Module Breakdown:**

* **Module 37: The ioctl System Call.** A deep dive into how ioctl works in UNIX-like systems as a generic device control interface.  
* **Module 38: Inferring the NVIDIA ioctl Interface.** Analyzing the open-source kernel interface layer to understand the structure of commands for context creation, memory allocation, and data transfer.  
* **Module 39: GPU Command Submission.** Understanding the high-level process of how a kernel launch configuration (grid/block dimensions) is packaged and sent to the kernel driver for execution.

### **Section 3.4: Kernel-Level Memory Management: UVM, Page Faults, and DMA (Modules 40-42)**

This section focuses on implementing the kernel-side logic for managing GPU memory, with a special emphasis on Unified Memory (UM). At its core, UM allows the GPU to access host memory and vice-versa within a single, unified virtual address space, simplifying programming by eliminating explicit cudaMemcpy calls.16

At a low level, this is often implemented via demand paging. When the GPU attempts to access a memory page that is not currently resident in its local VRAM, it triggers a page fault. This fault is trapped by the nvidia-uvm.ko module. The kernel driver must then handle this fault by pausing the GPU execution, allocating a page on the GPU, initiating a DMA (Direct Memory Access) transfer to copy the data from host RAM to VRAM, updating the GPU's page tables to map the virtual address to the new physical VRAM location, and finally resuming GPU execution.25

To support this, our kernel's page fault handler, developed in Part II, must be extended. It needs to be able to identify faults originating from the GPU (via the UVM driver), communicate with the NVIDIA driver components to orchestrate the page migration, and manage the underlying physical memory on both the host and device side. We will also map the concepts of different CUDA memory types—such as global, shared, and pinned memory—to the memory management primitives available in our custom kernel.26

**Module Breakdown:**

* **Module 40: GPU Memory Models.** Global, shared, constant, and texture memory. The concept of pinned (page-locked) host memory for faster DMA.27  
* **Module 41: Unified Memory and Demand Paging.** The low-level mechanics of UM. How GPU-initiated page faults are handled by the kernel.  
* **Module 42: DMA and IOMMU.** Understanding Direct Memory Access. Configuring the IOMMU (Input-Output Memory Management Unit) to allow the GPU to safely access host memory.

### **Section 3.5: Implementing a CUDA-Compatible Kernel Driver Stub (Modules 43-45)**

This is the capstone project for the NVIDIA part of the course. Students will synthesize all the knowledge gained in the preceding modules to write a loadable module for our custom kernel. This "driver stub" will be the practical realization of the new "kernel interface layer."

The project will involve several key steps:

1. Creating the necessary device nodes (/dev/nvidiactl, /dev/nvidia0) that the user-space driver expects to find.  
2. Implementing the open, close, and ioctl file operations for these device nodes.  
3. Handling a minimal but critical subset of ioctl commands. This will start with the commands required for device initialization and context creation.  
4. Implementing the ioctls for memory allocation (cuMemAlloc), which will involve calling our kernel's physical frame allocator and updating the GPU's address space.  
5. Implementing the ioctls for host-to-device data transfer (cuMemcpyHtoD), which will require setting up and managing a DMA transfer.

This project is a significant engineering challenge that directly applies the lessons learned from analyzing both the Nanos GPU driver port 5 and the architectural separation of NVIDIA's open-source modules.21 Successful completion demonstrates a deep, functional understanding of the user-kernel boundary for a complex hardware accelerator.

**Module Breakdown:**

* **Module 43: Project Setup.** Creating the module structure. Interfacing with our kernel's module loading and device management subsystems.  
* **Module 44: Implementing Initialization and Memory ioctls.** Writing the handlers for device discovery, context creation, and memory allocation.  
* **Module 45: Implementing a Simple Data Transfer.** Writing the handler for a host-to-device memory copy and verifying the data integrity on the device side using debugging tools.

---

## **Part IV: The GPU Subsystem: A Deep Dive into AMD ROCm (Modules 46-60)**

This part of the curriculum mirrors the deep dive into NVIDIA CUDA but focuses on the AMD ROCm (Radeon Open Compute) platform. The key difference and pedagogical advantage of studying ROCm is its open-source nature. Unlike the CUDA stack, where parts of the driver are a "black box," the entire ROCm stack, from the user-space runtime down to the kernel driver, is open source.29 This allows for a more direct and less inferential study of the driver architecture, providing an invaluable counterpoint to the NVIDIA ecosystem.

### **Table: Comparative Analysis of CUDA and ROCm Kernel-Level Interfaces**

To frame the upcoming modules, it is essential to establish a high-level comparison between the two GPU ecosystems. This strategic overview highlights the architectural differences that will directly impact our kernel development process.

| Feature | NVIDIA CUDA Approach | AMD ROCm Approach | Implications for Custom Kernel |
| :---- | :---- | :---- | :---- |
| **Driver Licensing** | Proprietary core with open-source kernel interface layers.21 | Fully open source (FOSS) under permissive licenses (MIT, etc.).29 | ROCm allows for direct code porting and adaptation; CUDA requires interfacing with binary blobs. |
| **User/Kernel Interface** | Undocumented ioctl commands on /dev/nvidia\* nodes.25 | Documented ioctl interface via kfd\_ioctl.h (for compute) and DRM/amdgpu interfaces.31 | ROCm development is API-driven and transparent; CUDA development requires more reverse engineering and inference. |
| **Memory Management** | Unified Virtual Memory (UVM) is a custom, fault-based system implemented in nvidia-uvm.ko.16 | Leverages standard Linux Heterogeneous Memory Management (HMM) and HSA architecture.33 | Porting ROCm memory management involves implementing HMM-like features; CUDA requires handling specific UVM-related faults. |
| **Compilation Target** | PTX (Parallel Thread Execution), a stable virtual ISA, provides forward compatibility.17 | GCN/CDNA ISA, a hardware-specific instruction set. HIP provides a source-level compatibility layer.29 | Kernel does not need to be aware of PTX, but for ROCm, it handles hardware-specific code objects directly. |
| **Driver Modularity** | Multiple modules (nvidia.ko, nvidia-uvm.ko, etc.) with distinct roles.20 | A single, monolithic DRM driver (amdgpu.ko) handles graphics, display, and compute.29 | Interfacing with ROCm means interacting with a single, large driver module's compute-specific subset (KFD). |

### **Section 4.1: The ROCm Open-Source Stack: ROCk, ROCt, ROCr, and HIP (Modules 46-48)**

This section provides a comprehensive overview of the entire ROCm software stack, emphasizing its modular, open-source composition, which is often compared to the UNIX philosophy of small, interoperable tools.29 We will trace the relationships between the key components:

* **HIP (Heterogeneous-computing Interface for Portability):** A C++ runtime API and kernel language that allows developers to write portable applications that can run on both AMD and NVIDIA GPUs. It acts as a crucial compatibility layer, often by source-to-source translation of CUDA code via tools like HIPIFY.29  
* **ROCr (ROC Runtime):** The user-space runtime library that implements the HSA (Heterogeneous System Architecture) runtime API. It is responsible for discovering devices, managing memory, and launching compute kernels.29  
* **ROCt (ROC Thunk):** A user-space library that acts as the "thunk" layer, translating ROCr API calls into the specific ioctl commands required by the kernel-mode driver.29  
* **ROCk (Kernel Driver):** This is not a separate driver but rather the compute-specific functionality within the upstream Linux amdgpu kernel module.29

Understanding this layered architecture is key to seeing how a high-level call in a HIP application is progressively lowered until it becomes a command submitted to the kernel.

**Module Breakdown:**

* **Module 46: ROCm Architecture and Philosophy.** The HSA foundation. The roles of the various ROC libraries.29  
* **Module 47: The HIP Programming Model.** Writing and compiling HIP applications. The role of the hipcc compiler wrapper.  
* **Module 48: Source-to-Source Translation.** A practical lab using the HIPIFY tool to convert a simple CUDA application to HIP.29

### **Section 4.2: The amdgpu Kernel Driver: KFD, ioctls, and Command Queues (Modules 49-52)**

This section is a deep dive into the amdgpu Linux kernel module, which is a comprehensive Direct Rendering Manager (DRM) driver responsible for all aspects of AMD GPU operation. For our purposes, we will focus on the **KFD (Kernel Fusion Driver)** interface, which is the component of amdgpu dedicated to handling compute workloads.

Unlike the opaque NVIDIA interface, the KFD interface is a public, stable API defined in the kfd\_ioctl.h header file, which is part of the Linux kernel source.31 This section will be a line-by-line analysis of this header. Students will learn the specific

ioctl commands and their associated data structures for fundamental operations:

* Querying device properties and version information.  
* Creating and destroying process address spaces.  
* Allocating and managing memory (both VRAM and system memory accessible to the GPU).  
* Creating and destroying hardware command queues.  
* Submitting jobs (command packets) to a queue.  
* Managing events and synchronization.

We will also examine the extensive list of module parameters that the amdgpu driver exposes via sysfs, which allow for fine-grained tuning and debugging of everything from memory sizes (vramlimit, vm\_size) to scheduler timeouts (lockup\_timeout) and power management (dpm).38

**Module Breakdown:**

* **Module 49: The Linux DRM and KFD Subsystems.** An overview of the Direct Rendering Manager framework and KFD's role within it.  
* **Module 50: The kfd\_ioctl.h API (Part 1).** A detailed study of the ioctls for device and process management.  
* **Module 51: The kfd\_ioctl.h API (Part 2).** A detailed study of the ioctls for memory and event management.  
* **Module 52: The kfd\_ioctl.h API (Part 3).** A detailed study of the ioctls for queue creation and job submission.

### **Section 4.3: Kernel-Level Heterogeneous Memory Management (HMM) (Modules 53-56)**

Here, we will study AMD's approach to unified memory, which contrasts with NVIDIA's custom UVM solution. AMD's implementation is designed to integrate more closely with standard Linux kernel features, specifically **HMM (Heterogeneous Memory Management)**. HMM allows a device driver to mirror a process's page tables, enabling the device (the GPU) to directly access the process's memory and trigger page faults on non-resident pages, which the kernel can then handle.34

We will analyze the different levels of unified memory support available in ROCm, from basic unified virtual addressing (where CPU and GPU share an address space but require explicit data copies) to true, demand-paged HMM where memory pages are automatically migrated between host and device on-fault.33 We will trace how a user-space call like

hipMallocManaged interacts with the underlying KFD memory management ioctls to allocate memory that is visible to both the CPU and GPU, and how the kernel's page fault handler is involved in orchestrating migrations.

**Module Breakdown:**

* **Module 53: Introduction to Linux HMM.** The core concepts of HMM and its role in CPU-device memory coherence.  
* **Module 54: ROCm Unified Memory.** How hipMallocManaged works. The distinction between fine-grained and coarse-grained coherence.33  
* **Module 55: Demand Paging on AMD GPUs.** Tracing a GPU-initiated page fault through the amdgpu driver and the kernel's MMU notifier subsystem.  
* **Module 56: Memory Allocation Strategies.** Analyzing the amdgpu driver's internal memory manager and how it handles VRAM and GTT (Graphics Translation Table) memory.

### **Section 4.4: GPU Scheduling and Command Processor Interaction (Modules 57-58)**

This section focuses on the mechanics of job submission. We will examine how the amdgpu driver's scheduler takes command packets from user space and submits them to the GPU's hardware command processors. A key concept here is the **AQL (Architected Queuing Language)** packet format, which provides a standardized way for the host to enqueue work for the GPU.36

User-space runtimes like ROCr create command queues in VRAM, which are structured as ring buffers. The application writes AQL packets into this queue, and then informs the kernel (via an ioctl) that new work is available by updating a write pointer. The kernel then instructs the GPU's command processor to fetch and execute these packets from the ring buffer. We will study the amdgpu\_cs (Command Submission) ioctl and its role in this process, and the interrupt mechanisms used by the GPU to signal job completion back to the kernel.41

**Module Breakdown:**

* **Module 57: Hardware Command Queues and Ring Buffers.** The architecture of user-space accessible command queues.  
* **Module 58: The AQL Packet Format and Command Submission.** Dissecting the structure of AQL packets. Tracing the amdgpu\_cs ioctl from user space to hardware submission.

### **Section 4.5: Implementing a ROCm-Compatible Kernel Driver Stub (Modules 59-60)**

As the capstone project for the AMD section, students will implement a driver module for our custom kernel that provides the KFD ioctl interface. Because the entire ROCm stack is open source and the KFD API is public, this project will be fundamentally different from the NVIDIA one. The task is less about reverse engineering and more about careful porting and adaptation.

Students will use the kfd\_ioctl.h header as a formal specification. The project will involve implementing the kernel-side handlers for the core KFD ioctls, such as those for queue creation, memory allocation, and mapping. The internal logic of these handlers will call upon the respective subsystems of our custom kernel (e.g., the memory manager, scheduler). This project requires a deep understanding of both the KFD API and our kernel's internal architecture, and successful completion will result in a driver capable of initializing an AMD GPU and managing its basic resources from our custom OS.

**Module Breakdown:**

* **Module 59: Project Setup.** Defining the ioctl dispatch table in our kernel. Mapping KFD data structures to our kernel's native types.  
* **Module 60: Implementing Core KFD ioctls.** Writing the handlers for KFD\_IOC\_CREATE\_QUEUE and KFD\_IOC\_ALLOC\_MEMORY\_OF\_GPU. Testing the implementation by writing a simple user-space program that calls these ioctls.

---

## **Part V: The Toolchain: Compilers and Build Systems (Modules 61-70)**

Having built the core kernel and the GPU driver interfaces, this part shifts focus from the operating system itself to the essential tools required to build and optimize applications for it. A specialized kernel deserves a specialized toolchain. The goal of this section is to move beyond using off-the-shelf compilers and instead create a custom, domain-specific compiler toolchain using modern, modular infrastructure.

### **Section 5.1: Introduction to Compiler Infrastructure: LLVM and MLIR (Modules 61-63)**

This section introduces the foundational technologies for our custom toolchain: LLVM and MLIR (Multi-Level Intermediate Representation). LLVM is a collection of modular and reusable compiler and toolchain technologies, famous for its well-defined Intermediate Representation (LLVM IR), which serves as a universal language for optimizers and backends.42

MLIR is a newer project within the LLVM ecosystem that provides a novel infrastructure for building compilers. Its key innovation is the concept of a "multi-level" IR, which can represent code at various levels of abstraction within a single framework.43 This is exceptionally well-suited for AI/ML, as it can model everything from a high-level TensorFlow or PyTorch computation graph down to low-level, hardware-specific instructions. MLIR is not a single IR, but a framework for creating new IRs, known as "dialects".42 This extensibility is what allows us to build a compiler that is perfectly tailored to our custom kernel. We will explore MLIR's design philosophy as a "compiler construction kit" that aims to reduce the cost of building domain-specific compilers and improve compilation for heterogeneous hardware.44

**Module Breakdown:**

* **Module 61: The LLVM Project.** Architecture of LLVM. The role of LLVM IR. The separation of frontend, middle-end (optimizer), and backend (code generator).  
* **Module 62: Introduction to MLIR.** The motivation for a multi-level IR. Core concepts: Operations, Attributes, Types, and Regions.43  
* **Module 63: MLIR Dialects.** Understanding the dialect as a mechanism for extensibility. A survey of existing dialects (e.g., func, affine, scf, gpu).

### **Section 5.2: Designing an MLIR Dialect for Kernel-Level AI Operations (Modules 64-66)**

This is a hands-on section where students will apply the concepts of MLIR to design and implement their own custom dialect. This dialect will serve as the high-level interface for our compiler, defining custom operations that map directly to the unique primitives and system calls provided by our minimalist kernel.

For example, we might define operations like:

* aikernel.gpu.submit\_commands: An operation that takes a buffer of GPU commands and lowers to the specific system call that submits work to our custom GPU driver.  
* aikernel.mem.alloc\_pinned: An operation to allocate page-locked host memory, which lowers to the corresponding memory management syscall in our kernel.

The implementation process will heavily utilize TableGen, a declarative language used by LLVM and MLIR to define records that can be processed by a backend to generate large amounts of C++ boilerplate code.45 By defining our operations, types, and attributes in

TableGen, we can automatically generate the C++ classes and verification logic, significantly accelerating the development of our dialect.

**Module Breakdown:**

* **Module 64: Dialect Design Principles.** Defining the semantics of our custom operations. Structuring the dialect for progressive lowering.  
* **Module 65: Implementing a Dialect with TableGen.** Writing .td files to define operations, attributes, and interfaces.  
* **Module 66: Building and Testing the Custom Dialect.** Integrating the new dialect into an MLIR-based tool. Writing test cases using mlir-opt and FileCheck.

### **Section 5.3: Lowering MLIR to LLVM IR and Target-Specific Code (Modules 67-68)**

A dialect on its own is just a representation. To be useful, it must be transformable into something that can eventually be executed. This section focuses on writing the compiler passes that perform this "lowering." Lowering is the process of progressively transforming operations from a higher-level, more abstract dialect into operations in a lower-level dialect.

Students will write C++ passes that match on operations from our custom aikernel dialect and replace them with equivalent semantics expressed in standard MLIR dialects. For example, a high-level GPU submission operation might be lowered into a sequence of standard function calls that implement the system call ABI of our kernel. This process continues until the entire program is represented in dialects that have a direct lowering path to LLVM IR. Once in LLVM IR, we can leverage LLVM's mature ecosystem of optimizers and code generators to produce highly optimized x86\_64 machine code for the host-side application. This demonstrates the full power of MLIR's multi-level pipeline: representing domain-specific concepts at a high level and systematically compiling them down to efficient, low-level code.44

**Module Breakdown:**

* **Module 67: Writing MLIR Transformation Passes.** The structure of a rewrite pass. Using the Declarative Rewrite Rule (DRR) framework.  
* **Module 68: Lowering to LLVM IR.** The MLIR LLVM dialect as the bridge to the LLVM ecosystem. Generating the final executable object file.

### **Section 5.4: Integrating the Rust Compiler (Modules 69-70)**

The final step in building our toolchain is to ensure it interoperates smoothly with Rust, our kernel's implementation language. While the compiler passes are written in C++, the end user (the application developer) will be writing Rust. This requires creating a seamless bridge between the two ecosystems.

We will use tools like bindgen or cxx to automatically generate safe Rust wrappers around the C++ APIs of our custom MLIR-based compiler. This will allow Rust code to invoke the compiler programmatically. Furthermore, we will leverage Cargo's powerful build script functionality (build.rs). The build script will be configured to run our custom compiler on specific source files (e.g., files defining the AI model's computation graph) during the application's build process, and then link the resulting object files into the final Rust binary. This deep integration makes the custom toolchain a natural part of the standard Rust development workflow.8

**Module Breakdown:**

* **Module 69: Bridging C++ and Rust.** Using bindgen to create safe FFI (Foreign Function Interface) bindings for the compiler's C++ API.  
* **Module 70: Cargo Build Scripts and Integration.** Writing a build.rs script to invoke the custom compiler. Linking the generated object files into a Rust application.

---

## **Part VI: Containerization and AI/ML Workload Support (Modules 71-80)**

This part brings all the preceding work together, focusing on the ultimate goal: running a containerized AI/ML application on top of our custom kernel. We will implement the necessary container primitives, create the runtime interface to support a real AI/ML framework, and explore unique optimizations that are only possible because we control the entire software stack.

### **Section 6.1: Implementing Container Primitives (Modules 71-73)**

The term "container" in the context of a general-purpose OS like Linux refers to a combination of kernel features: namespaces for isolation (PID, network, mount, etc.) and cgroups for resource control. For our single-application, single-tenant unikernel, this level of complexity is unnecessary. Our implementation of "container primitives" will be far simpler and tailored to our specific use case.

The primary goal is to provide a filesystem boundary for the application. We will implement a chroot-like mechanism that confines the application's view of the filesystem to the initramfs we created earlier. This prevents the application from accessing any kernel-internal structures or devices that are not explicitly exposed. We will also implement a rudimentary form of resource limiting, akin to a simplified cgroup, to control the maximum amount of memory the application can allocate. This provides a basic level of containment and security without the overhead of full namespace virtualization.

**Module Breakdown:**

* **Module 71: Filesystem Isolation.** Implementing a chroot-style environment for the application process.  
* **Module 72: Resource Management.** Designing and implementing a simple resource controller to limit the application's memory usage.  
* **Module 73: Loading and Running an ELF Binary.** Writing the kernel code to parse an ELF executable from the initramfs, load its segments into virtual memory, set up its stack, and transfer control to its entry point in user mode.

### **Section 6.2: The AI/ML Runtime Interface (Modules 74-76)**

This section focuses on creating the "glue" layer that allows a standard AI/ML framework, such as PyTorch or TensorFlow, to execute on our custom kernel. The goal is not to recompile the entire framework, but to intercept its calls to the underlying GPU driver libraries (like libcuda.so or librocm.so) and redirect them to our kernel's custom system call interface.

This can be achieved by creating a shared library that implements the public API of the CUDA or ROCm runtime and preloading it into the application's environment. When the application calls a function like cudaMalloc, our library's implementation will be invoked. Instead of communicating with the standard NVIDIA driver, it will execute our custom system call, which in turn invokes our kernel's memory manager. This shim layer effectively translates the standard AI framework's requests into the language of our minimalist kernel. This requires a deep understanding of how these frameworks manage GPU memory, track device state, and launch kernels, often through tools like PyTorch's memory snapshot visualizer.46

**Module Breakdown:**

* **Module 74: The CUDA/ROCm User-Mode Driver API.** A deep dive into the functions exported by libcuda.so and their purpose.  
* **Module 75: Building a Shim Library.** Creating a shared library that implements a subset of the CUDA Driver API.  
* **Module 76: Intercepting and Redirecting API Calls.** Using LD\_PRELOAD to load our shim library. Translating API calls into our kernel's system calls.

### **Section 6.3: Optimizing for AI: Direct GPU Scheduling and Memory Pinning (Modules 77-78)**

Now that we control the entire stack, from the application's API call down to the kernel's interaction with the hardware, we can implement powerful, cross-layer optimizations that would be difficult or impossible in a general-purpose OS.

One such optimization is **direct GPU scheduling**. In a traditional model, every kernel launch requires a system call, which involves a costly context switch into the kernel. We can design a more efficient mechanism where the user-space runtime and the kernel's GPU driver share a region of memory that acts as a command buffer or ring buffer. The runtime can write kernel launch commands directly into this shared memory region and then use a single, lightweight system call (or even an atomic memory operation) to notify the kernel that new work is available. The kernel driver, which is already polling or waiting on an interrupt, can then consume these commands directly, bypassing the overhead of the ioctl path for every launch.

This approach is inspired by the ideas of bringing computation closer to the kernel, as proposed in research on AI-native kernels 1, but applied pragmatically to the user-kernel communication boundary.

**Module Breakdown:**

* **Module 77: Shared-Memory Command Submission.** Designing a ring buffer in shared memory for user-kernel communication. Implementing the kernel and user-space logic to manage it.  
* **Module 78: Optimizing Memory Transfers.** Implementing highly efficient memory pinning via our custom mmap syscall to prepare host memory for zero-copy DMA transfers.

### **Section 6.4: Packaging the Kernel: Minimalist "Distroless" Container Images (Modules 79-80)**

The final step in preparing our application is to package it for deployment in a way that aligns with our minimalist philosophy. This means creating the smallest possible container image that contains only the application binary and its absolute essential runtime dependencies.

We will employ **multi-stage Docker builds** as a best practice.47 The first stage, the "build stage," will use a full development environment containing our custom MLIR-based toolchain and the Rust compiler. This stage will compile the application. The second stage, the "final stage," will start from a truly minimal base image, such as

scratch or a "distroless" image provided by Google.49 We will then use the

COPY \--from=\<build\_stage\> instruction to copy *only* the compiled application binary and our custom GPU runtime shim library from the build stage into the final image.52

This technique ensures that no compilers, build tools, package managers, shells, or other unnecessary utilities are present in the final production image. The result is a container image that is typically an order of magnitude smaller than a traditional one, which reduces storage costs, speeds up deployment, and significantly minimizes the potential attack surface.50

**Module Breakdown:**

* **Module 79: Multi-Stage Docker Builds.** The syntax and benefits of multi-stage builds. Creating a Dockerfile for our AI application.  
* **Module 80: Distroless and Scratch Images.** Understanding distroless concepts. Creating a final container image from scratch containing only our application binary and its essential shared libraries.

---

## **Part VII: Testing, Profiling, and Deployment (Modules 81-100)**

The final part of the course is dedicated to ensuring the kernel is robust, performant, and deployable in a real-world cloud environment. This involves building a comprehensive testing framework, integrating advanced, low-overhead profiling capabilities, systematically benchmarking and tuning performance, and mastering the process of deploying a custom OS to major cloud providers.

### **Section 7.1: A Kernel Testing Framework with QEMU and GDB (Modules 81-85)**

A robust testing strategy is non-negotiable for kernel development. We will build a comprehensive testing suite that combines unit tests for individual modules and integration tests that run the entire kernel within the QEMU emulator.

We will leverage Rust's support for custom test frameworks, which allows us to define how tests are discovered and executed.10 This enables us to write test functions directly within our

no\_std kernel code. For integration tests, cargo test will be configured to compile the kernel, package it into a bootable image, and run it under QEMU. QEMU can be configured with a special device that allows the guest OS to signal a success or failure code back to the host upon completion, which integrates seamlessly with the test runner.54

The QEMU testing environment will be our primary tool for development and debugging.55 We will make extensive use of GDB, connecting to the QEMU GDB server to debug panics, step through code, and inspect memory.12 This rigorous, automated testing framework is essential for maintaining code quality and catching regressions as the kernel's complexity grows.

**Module Breakdown:**

* **Module 81: Unit Testing in no\_std.** Setting up a unit testing framework for kernel modules.  
* **Module 82: Integration Testing with QEMU.** Configuring cargo test to run the kernel in QEMU.  
* **Module 83: Reporting Test Results.** Using QEMU's isa-test-device or qemu\_exit mechanism to communicate test outcomes to the host.  
* **Module 84: Advanced GDB Debugging.** Using GDB scripts provided by the kernel source for advanced debugging tasks, such as inspecting page tables or scheduler state.12  
* **Module 85: Building a Continuous Integration (CI) Pipeline.** Setting up a CI workflow (e.g., using GitHub Actions) to automatically build and test the kernel on every commit.

### **Section 7.2: Advanced Profiling with eBPF (Modules 86-90)**

Traditional profiling tools like Nsight are invaluable for deep, offline analysis but often introduce significant performance overhead, making them unsuitable for continuous monitoring in production environments.56 To address this, we will integrate a modern, low-overhead profiling framework into our kernel, inspired by Linux's revolutionary eBPF (Extended Berkeley Packet Filter) technology.

eBPF allows safe, sandboxed programs to be attached to hooks within the kernel, enabling powerful and programmable tracing with minimal performance impact.56 We will implement a simplified version of this concept in our kernel. This will involve defining stable tracepoints at critical locations in our code, such as system call entry/exit points, scheduler decisions, and, most importantly, the entry and exit points of our GPU driver

ioctl handlers. We can then attach small, safe "probe" programs to these tracepoints to gather detailed performance data, such as the frequency and latency of kernel launches or memory transfers.

This approach provides a form of zero-instrumentation observability, allowing us to understand the behavior of an AI application's interaction with the GPU in real-time, without modifying the application's code.56 By building this capability into the kernel from day one, we are creating a system that is designed to be transparent and debuggable in production, a significant advantage over treating the OS as an opaque black box.

**Module Breakdown:**

* **Module 86: Introduction to eBPF.** The architecture and principles of eBPF on Linux.  
* **Module 87: Designing a Kernel Tracing Framework.** Defining tracepoints and a simple, safe in-kernel virtual machine for running probes.  
* **Module 88: Probing the GPU Driver.** Adding tracepoints to our custom CUDA and ROCm driver stubs to monitor memory allocations, data transfers, and kernel launches.58  
* **Module 89: Collecting and Exporting Telemetry.** Writing the user-space tooling to load probes and collect data from the kernel via ring buffers.  
* **Module 90: Visualizing Performance Data.** Exporting the collected data to standard observability tools like Prometheus and Grafana.59

### **Section 7.3: Benchmarking and Performance Tuning (Modules 91-95)**

With a robust testing and profiling framework in place, this section focuses on systematic performance analysis and optimization. We will run a suite of standard AI/ML benchmarks, starting with micro-benchmarks like matrix multiplication (GEMM) and progressing to small but complete models like a simple transformer for inference.

Using the eBPF-inspired profiling tools we built, we will analyze the performance of these benchmarks on our kernel. We will identify bottlenecks by measuring the latency and frequency of critical operations. This data-driven approach will guide our tuning efforts. For example, we might discover that our scheduler is causing unnecessary delays, that our memory allocator is leading to fragmentation under load, or that the GPU command submission pipeline has higher-than-expected overhead. Students will then systematically tune these subsystems, measure the impact of their changes, and iterate until performance goals are met.

**Module Breakdown:**

* **Module 91: Selecting and Implementing Benchmarks.** Porting standard ML benchmarks (e.g., from mlperf) to run on our kernel.  
* **Module 92: Bottleneck Analysis.** Using our custom profiler to identify performance hotspots in the kernel and driver.  
* **Module 93: Tuning the Scheduler.** Experimenting with different scheduling policies and time slices.  
* **Module 94: Optimizing the Memory Manager.** Tuning the HugePage allocation strategy and heap allocator performance.  
* **Module 95: End-to-End Performance Analysis.** Comparing the final performance of our custom kernel against a standard Linux kernel running the same workload in a container.

### **Section 7.4: Deploying the Custom Kernel and Container Runtime to Cloud Infrastructure (Modules 96-100)**

The final project of the course is to deploy the complete, custom-built system to a major cloud provider like Amazon Web Services (AWS) or Microsoft Azure. This demonstrates the end-to-end viability of the kernel and provides invaluable experience with real-world deployment challenges.

The process involves taking our bootable kernel image and initramfs and packaging them into a custom machine image (e.g., an Amazon Machine Image or AMI). This requires understanding the cloud provider's specific procedures for using user-provided kernels.60 A key step is configuring the bootloader (typically GRUB) within the image to load our custom kernel instead of the provider's default Linux kernel.62 We must also ensure that our

initramfs contains the necessary drivers for the cloud environment's virtualized hardware, especially for networking (e.g., the ENA driver on AWS) and storage (e.g., the NVMe driver for EBS volumes), to ensure the instance can boot and be accessed remotely.

Once the custom image is created, we will launch a GPU-enabled virtual instance from it. The final test is to deploy and run our containerized AI/ML application on this instance, verifying that it can successfully initialize the GPU via our custom driver and execute a workload. This capstone project validates the entire year's work, from the first line of boot code to a fully functional, specialized AI/ML operating system running in the cloud.

**Module Breakdown:**

* **Module 96: Cloud Virtualization and Drivers.** Understanding the virtualized hardware environment of cloud providers (networking, storage).  
* **Module 97: Building a Custom Amazon Machine Image (AMI).** The process of bundling our kernel and initramfs and registering a new AMI.60  
* **Module 98: Configuring the GRUB Bootloader.** Modifying the grub.cfg to chain-load our custom kernel and provide the correct command-line arguments.  
* **Module 99: Deploying to Microsoft Azure.** A parallel module covering the process for creating and deploying a custom image on Azure.63  
* **Module 100: Final Project: End-to-End Cloud Deployment.** Launching a GPU instance with our custom kernel, deploying the AI container, running a benchmark, and verifying the results.

#### **Works cited**

1. Composable OS Kernel Architectures for Autonomous Intelligence \- arXiv, accessed August 16, 2025, [https://arxiv.org/html/2508.00604v1](https://arxiv.org/html/2508.00604v1)  
2. r/UniKernel \- Reddit, accessed August 16, 2025, [https://www.reddit.com/r/UniKernel/](https://www.reddit.com/r/UniKernel/)  
3. Introducing Unikraft \- Lightweight Virtualization Using Unikernels \- KubeSimplify blog, accessed August 16, 2025, [https://blog.kubesimplify.com/introducing-unikraft-lightweight-virtualization-using-unikernels](https://blog.kubesimplify.com/introducing-unikraft-lightweight-virtualization-using-unikernels)  
4. Compatibility \- Unikraft, accessed August 16, 2025, [https://unikraft.org/docs/concepts/compatibility](https://unikraft.org/docs/concepts/compatibility)  
5. GPU-accelerated Computing with Nanos Unikernels \- NanoVMs, accessed August 16, 2025, [https://nanovms.com/dev/tutorials/gpu-accelerated-computing-nanos-unikernels](https://nanovms.com/dev/tutorials/gpu-accelerated-computing-nanos-unikernels)  
6. Composable OS Kernel Architectures for Autonomous ... \- arXiv, accessed August 16, 2025, [https://arxiv.org/pdf/2508.00604](https://arxiv.org/pdf/2508.00604)  
7. Composable OS Kernel Architectures for Autonomous Intelligence | AI Research Paper Details \- AIModels.fyi, accessed August 16, 2025, [https://aimodels.fyi/papers/arxiv/composable-os-kernel-architectures-autonomous-intelligence](https://aimodels.fyi/papers/arxiv/composable-os-kernel-architectures-autonomous-intelligence)  
8. Rust Programming Language, accessed August 16, 2025, [https://www.rust-lang.org/](https://www.rust-lang.org/)  
9. Rust \- OSDev Wiki, accessed August 16, 2025, [https://wiki.osdev.org/Rust](https://wiki.osdev.org/Rust)  
10. Writing an OS in Rust, accessed August 16, 2025, [https://os.phil-opp.com/](https://os.phil-opp.com/)  
11. Getting started \- Rust Programming Language, accessed August 16, 2025, [https://www.rust-lang.org/learn/get-started](https://www.rust-lang.org/learn/get-started)  
12. Booting a Custom Linux Kernel in QEMU and Debugging It With GDB, accessed August 16, 2025, [https://nickdesaulniers.github.io/blog/2018/10/24/booting-a-custom-linux-kernel-in-qemu-and-debugging-it-with-gdb/](https://nickdesaulniers.github.io/blog/2018/10/24/booting-a-custom-linux-kernel-in-qemu-and-debugging-it-with-gdb/)  
13. How to build the Linux kernel and test changes locally in qemu \- GitHub Gist, accessed August 16, 2025, [https://gist.github.com/ncmiller/d61348b27cb17debd2a6c20966409e86](https://gist.github.com/ncmiller/d61348b27cb17debd2a6c20966409e86)  
14. Configuring HugePages for Enhanced Linux Server Performance \- WafaTech Blogs, accessed August 16, 2025, [https://wafatech.sa/blog/linux/linux-security/configuring-hugepages-for-enhanced-linux-server-performance/](https://wafatech.sa/blog/linux/linux-security/configuring-hugepages-for-enhanced-linux-server-performance/)  
15. xmap: Transparent, Hugepage-Driven Heap Extension over Fast Storage Devices \- EuroSys 2024, accessed August 16, 2025, [https://2024.eurosys.org/posters/eurosys24posters-paper21.pdf](https://2024.eurosys.org/posters/eurosys24posters-paper21.pdf)  
16. CUDA \- Wikipedia, accessed August 16, 2025, [https://en.wikipedia.org/wiki/CUDA](https://en.wikipedia.org/wiki/CUDA)  
17. NVIDIA CUDA Compiler Driver Process | by ztex, Tony, Liu | Medium, accessed August 16, 2025, [https://ztex.medium.com/nvidia-cuda-compiler-driver-process-cuda-kernel-deployment-from-code-to-gpu-execution-f94fdc41c8fe](https://ztex.medium.com/nvidia-cuda-compiler-driver-process-cuda-kernel-deployment-from-code-to-gpu-execution-f94fdc41c8fe)  
18. Nvidia CUDA in 100 Seconds \- YouTube, accessed August 16, 2025, [https://www.youtube.com/watch?v=pPStdjuYzSI](https://www.youtube.com/watch?v=pPStdjuYzSI)  
19. Exploring CUDA Architecture: A Deep Dive \- Metric Coders, accessed August 16, 2025, [https://www.metriccoders.com/post/exploring-cuda-architecture-a-deep-dive](https://www.metriccoders.com/post/exploring-cuda-architecture-a-deep-dive)  
20. How do you build out-of-tree modules, e.g., nvidia modules for customized kernel?, accessed August 16, 2025, [https://discussion.fedoraproject.org/t/how-do-you-build-out-of-tree-modules-e-g-nvidia-modules-for-customized-kernel/77295](https://discussion.fedoraproject.org/t/how-do-you-build-out-of-tree-modules-e-g-nvidia-modules-for-customized-kernel/77295)  
21. NVIDIA/open-gpu-kernel-modules: NVIDIA Linux open ... \- GitHub, accessed August 16, 2025, [https://github.com/NVIDIA/open-gpu-kernel-modules](https://github.com/NVIDIA/open-gpu-kernel-modules)  
22. NVIDIA Jetson Linux Developer Guide : Kernel Customization, accessed August 16, 2025, [https://docs.nvidia.com/jetson/l4t/Tegra%20Linux%20Driver%20Package%20Development%20Guide/kernel\_custom.html](https://docs.nvidia.com/jetson/l4t/Tegra%20Linux%20Driver%20Package%20Development%20Guide/kernel_custom.html)  
23. Compiling the Kernel (Kernel 5.10) | NVIDIA Docs \- NVIDIA Developer, accessed August 16, 2025, [https://developer.nvidia.com/docs/drive/drive-os/6.0.8/public/drive-os-linux-sdk/common/topics/sys\_programming/compiling\_the\_kernel\_linux.html](https://developer.nvidia.com/docs/drive/drive-os/6.0.8/public/drive-os-linux-sdk/common/topics/sys_programming/compiling_the_kernel_linux.html)  
24. Compiling the Kernel (Kernel 5.15) | NVIDIA Docs \- NVIDIA Developer, accessed August 16, 2025, [https://developer.nvidia.com/docs/drive/drive-os/6.0.7/public/drive-os-linux-sdk/common/topics/sys\_programming/compiling-the-kernel-kernel-515.html](https://developer.nvidia.com/docs/drive/drive-os/6.0.7/public/drive-os-linux-sdk/common/topics/sys_programming/compiling-the-kernel-kernel-515.html)  
25. What does the nVIDIA CUDA driver do exactly? \- Stack Overflow, accessed August 16, 2025, [https://stackoverflow.com/questions/9764591/what-does-the-nvidia-cuda-driver-do-exactly](https://stackoverflow.com/questions/9764591/what-does-the-nvidia-cuda-driver-do-exactly)  
26. CUDA Series: Memory and Allocation | by Dmitrij Tichonov \- Medium, accessed August 16, 2025, [https://medium.com/@dmitrijtichonov/cuda-series-memory-and-allocation-fce29c965d37](https://medium.com/@dmitrijtichonov/cuda-series-memory-and-allocation-fce29c965d37)  
27. Understanding CUDA Memory Usage: A Practical Guide | by Hey Amit \- Medium, accessed August 16, 2025, [https://medium.com/@heyamit10/understanding-cuda-memory-usage-a-practical-guide-6dbb85d4da5a](https://medium.com/@heyamit10/understanding-cuda-memory-usage-a-practical-guide-6dbb85d4da5a)  
28. Memory management \- Numba, accessed August 16, 2025, [https://numba.pydata.org/numba-doc/dev/cuda/memory.html](https://numba.pydata.org/numba-doc/dev/cuda/memory.html)  
29. ROCm \- Wikipedia, accessed August 16, 2025, [https://en.wikipedia.org/wiki/ROCm](https://en.wikipedia.org/wiki/ROCm)  
30. AMD ROCm™ Software \- GitHub Home, accessed August 16, 2025, [https://github.com/ROCm/ROCm](https://github.com/ROCm/ROCm)  
31. Support and limitations — ROCdbgapi 0.77.2 Documentation, accessed August 16, 2025, [https://rocm.docs.amd.com/projects/ROCdbgapi/en/docs-6.4.2/reference/known-issues.html](https://rocm.docs.amd.com/projects/ROCdbgapi/en/docs-6.4.2/reference/known-issues.html)  
32. git.kernel.dk Git \- include/uapi/linux/kfd\_ioctl.h \- kernel.dk, accessed August 16, 2025, [https://git.kernel.dk/?p=linux-2.6-block.git;a=blobdiff;f=include/uapi/linux/kfd\_ioctl.h;fp=include/uapi/linux/kfd\_ioctl.h;h=32913d674d38bb0434bacc18c5d04a45dcb64360;hp=2da5c3ad71bd0f7448e97dc4c9f24eba0f8ed603;hb=4f98cf2baf9faee5b6f2f7889dad7c0f7686a787;hpb=ba3c87fffb79311f54464288c66421d19c2c1234](https://git.kernel.dk/?p=linux-2.6-block.git;a%3Dblobdiff;f%3Dinclude/uapi/linux/kfd_ioctl.h;fp%3Dinclude/uapi/linux/kfd_ioctl.h;h%3D32913d674d38bb0434bacc18c5d04a45dcb64360;hp%3D2da5c3ad71bd0f7448e97dc4c9f24eba0f8ed603;hb%3D4f98cf2baf9faee5b6f2f7889dad7c0f7686a787;hpb%3Dba3c87fffb79311f54464288c66421d19c2c1234)  
33. Unified memory management — HIP 7.1.0 Documentation, accessed August 16, 2025, [https://rocm.docs.amd.com/projects/HIP/en/docs-develop/how-to/hip\_runtime\_api/memory\_management/unified\_memory.html](https://rocm.docs.amd.com/projects/HIP/en/docs-develop/how-to/hip_runtime_api/memory_management/unified_memory.html)  
34. HMM is, I believe, a Linux feature. AMD added HMM support in ROCm 5.0 according \- Hacker News, accessed August 16, 2025, [https://news.ycombinator.com/item?id=37309442](https://news.ycombinator.com/item?id=37309442)  
35. AMD ROCm™ installation \- AMD GPUOpen, accessed August 16, 2025, [https://gpuopen.com/learn/amd-lab-notes/amd-lab-notes-rocm-installation-readme/](https://gpuopen.com/learn/amd-lab-notes/amd-lab-notes-rocm-installation-readme/)  
36. AMDKFD Kernel Driver \- LWN.net, accessed August 16, 2025, [https://lwn.net/Articles/619581/](https://lwn.net/Articles/619581/)  
37. src/dev/hsa/kfd\_ioctl.h · lab\_4\_solution · Simon Jakob Feldtkeller / ProSec Lab \- NOC GitLab, accessed August 16, 2025, [https://git.noc.ruhr-uni-bochum.de/feldts4p/prosec-lab/-/blob/lab\_4\_solution/src/dev/hsa/kfd\_ioctl.h?ref\_type=heads](https://git.noc.ruhr-uni-bochum.de/feldts4p/prosec-lab/-/blob/lab_4_solution/src/dev/hsa/kfd_ioctl.h?ref_type=heads)  
38. drm/amdgpu AMDgpu driver — The Linux Kernel documentation, accessed August 16, 2025, [https://www.kernel.org/doc/html/v4.20/gpu/amdgpu.html](https://www.kernel.org/doc/html/v4.20/gpu/amdgpu.html)  
39. drm/amdgpu AMDgpu driver — The Linux Kernel documentation, accessed August 16, 2025, [https://www.kernel.org/doc/html/v5.9/gpu/amdgpu.html](https://www.kernel.org/doc/html/v5.9/gpu/amdgpu.html)  
40. drm/amdgpu AMDgpu driver — The Linux Kernel 5.10.0-rc1+ documentation, accessed August 16, 2025, [https://www.infradead.org/\~mchehab/kernel\_docs/gpu/amdgpu.html](https://www.infradead.org/~mchehab/kernel_docs/gpu/amdgpu.html)  
41. amdgpu/amdgpu\_cs.c \- chromiumos/third\_party/libdrm \- Git at Google, accessed August 16, 2025, [https://chromium.googlesource.com/chromiumos/third\_party/libdrm/+/refs/heads/master/amdgpu/amdgpu\_cs.c](https://chromium.googlesource.com/chromiumos/third_party/libdrm/+/refs/heads/master/amdgpu/amdgpu_cs.c)  
42. Understanding LLVM v/s MLIR: A Comprehensive Comparison Overview | by Prince Jain, accessed August 16, 2025, [https://medium.com/@princejain\_77044/understanding-llvm-v-s-mlir-a-comprehensive-comparison-overview-9afc0214adc1](https://medium.com/@princejain_77044/understanding-llvm-v-s-mlir-a-comprehensive-comparison-overview-9afc0214adc1)  
43. MLIR (software) \- Wikipedia, accessed August 16, 2025, [https://en.wikipedia.org/wiki/MLIR\_(software)](https://en.wikipedia.org/wiki/MLIR_\(software\))  
44. MLIR, accessed August 16, 2025, [https://mlir.llvm.org/](https://mlir.llvm.org/)  
45. MLIR: A Compiler Infrastructure for the End of Moore's Law | Hacker News, accessed August 16, 2025, [https://news.ycombinator.com/item?id=22429107](https://news.ycombinator.com/item?id=22429107)  
46. Understanding CUDA Memory Usage — PyTorch 2.7 documentation, accessed August 16, 2025, [https://pytorch.org/docs/stable/torch\_cuda\_memory.html](https://pytorch.org/docs/stable/torch_cuda_memory.html)  
47. Multi-stage builds | Docker Docs, accessed August 16, 2025, [https://docs.docker.com/get-started/docker-concepts/building-images/multi-stage-builds/](https://docs.docker.com/get-started/docker-concepts/building-images/multi-stage-builds/)  
48. Multi-stage | Docker Docs, accessed August 16, 2025, [https://docs.docker.com/build/building/multi-stage/](https://docs.docker.com/build/building/multi-stage/)  
49. Base images \- Docker Docs, accessed August 16, 2025, [https://docs.docker.com/build/building/base-images/](https://docs.docker.com/build/building/base-images/)  
50. Distroless Docker Images: A Guide to Security, Size and Optimization \- BellSoft, accessed August 16, 2025, [https://bell-sw.com/blog/distroless-containers-for-security-and-size/](https://bell-sw.com/blog/distroless-containers-for-security-and-size/)  
51. Is Your Container Image Really Distroless? \- Docker, accessed August 16, 2025, [https://www.docker.com/blog/is-your-container-image-really-distroless/](https://www.docker.com/blog/is-your-container-image-really-distroless/)  
52. How to Build Slim and Fast Docker Images with Multi-Stage Builds \- freeCodeCamp, accessed August 16, 2025, [https://www.freecodecamp.org/news/build-slim-fast-docker-images-with-multi-stage-builds/](https://www.freecodecamp.org/news/build-slim-fast-docker-images-with-multi-stage-builds/)  
53. Using official Python base images and packaging into distroless later on \#1543 \- GitHub, accessed August 16, 2025, [https://github.com/GoogleContainerTools/distroless/issues/1543](https://github.com/GoogleContainerTools/distroless/issues/1543)  
54. Building a testing platform for my kernel? : r/osdev \- Reddit, accessed August 16, 2025, [https://www.reddit.com/r/osdev/comments/t6cnt9/building\_a\_testing\_platform\_for\_my\_kernel/](https://www.reddit.com/r/osdev/comments/t6cnt9/building_a_testing_platform_for_my_kernel/)  
55. Testing in QEMU, accessed August 16, 2025, [https://www.qemu.org/docs/master/devel/testing/main.html](https://www.qemu.org/docs/master/devel/testing/main.html)  
56. Snooping on your GPU: Using eBPF to Build Zero-instrumentation ..., accessed August 16, 2025, [https://dev.to/ethgraham/snooping-on-your-gpu-using-ebpf-to-build-zero-instrumentation-cuda-monitoring-2hh1](https://dev.to/ethgraham/snooping-on-your-gpu-using-ebpf-to-build-zero-instrumentation-cuda-monitoring-2hh1)  
57. The Silent Revolution: eBPF Is Hacking Your GPU (For Good) | by kcl17 | Jul, 2025 \- Medium, accessed August 16, 2025, [https://medium.com/@kcl17/the-silent-revolution-ebpf-is-hacking-your-gpu-for-good-b986ff11e3a2](https://medium.com/@kcl17/the-silent-revolution-ebpf-is-hacking-your-gpu-for-good-b986ff11e3a2)  
58. Inside CUDA: Building eBPF uprobes for GPU Monitoring | by kcl17 | Jul, 2025 \- Medium, accessed August 16, 2025, [https://medium.com/@kcl17/inside-cuda-building-ebpf-uprobes-for-gpu-monitoring-449519b236ed](https://medium.com/@kcl17/inside-cuda-building-ebpf-uprobes-for-gpu-monitoring-449519b236ed)  
59. Auto-instrumentation for GPU performance using eBPF \- DevConf.CZ 2025 \- YouTube, accessed August 16, 2025, [https://www.youtube.com/watch?v=gGe9QvSpSf8](https://www.youtube.com/watch?v=gGe9QvSpSf8)  
60. User provided kernels \- Amazon Linux 2 \- AWS Documentation, accessed August 16, 2025, [https://docs.aws.amazon.com/linux/al2/ug/UserProvidedKernels.html](https://docs.aws.amazon.com/linux/al2/ug/UserProvidedKernels.html)  
61. Use Your Own Kernel with Amazon EC2 | AWS News Blog, accessed August 16, 2025, [https://aws.amazon.com/blogs/aws/use-your-own-kernel-with-amazon-ec2/](https://aws.amazon.com/blogs/aws/use-your-own-kernel-with-amazon-ec2/)  
62. How to rebuild Amazon Linux kernel in Amazon Linux \- Artem Butusov Blog, accessed August 16, 2025, [https://www.artembutusov.com/how-to-rebuild-amazon-linux-kernel-in-amazon-linux/](https://www.artembutusov.com/how-to-rebuild-amazon-linux-kernel-in-amazon-linux/)  
63. How to Deploy Semantic Kernel to Azure in Minutes \- Microsoft Developer Blogs, accessed August 16, 2025, [https://devblogs.microsoft.com/semantic-kernel/how-to-deploy-semantic-kernel-to-azure-in-minutes/](https://devblogs.microsoft.com/semantic-kernel/how-to-deploy-semantic-kernel-to-azure-in-minutes/)