# nsola.github.io
<h1> What is an operating system? </h1>
Most computer users have had some experience with an operating system, but it is difficult to pin down precisely what 
an operating system is. Part of the problem is that operating systems perform two basically unrelated functions, 
extending the machine and managing resources, and depending on who is doing the talking, you hear mostly about one
function or the other. Let us now look at both. 
Computers use low-level software called an operating system (O/S) to help people operate the physical machines.
An O/S enables running application software (called "programs") as well as building new programs. Operating system 
software runs not just on laptop computers but also on cell phones, network routers and other so-called embedded devices.
What are the roles of operating system?
The two main roles are extended machine or as an resource manager
the function of the operating system is to present the user with the equivalent of an extended machine or virtual machine 
that is easier to program than the underlying hardware. How the operating system achieves this goal is a long story, which
we will study in detail throughout this book. To summarize it in a nutshell, the operating system provides a variety of 
services that programs can obtain using special instructions called system calls.
The concept of the operating system as primarily providing its users with a convenient interface is a top-down view. An 
alternative, bottom-up, view holds that the operating system is there to manage all the pieces of a complex system
Createmultiplevirtualmachinesthateachusercan control all to themselves
– IBM 360/370 ...
• Monolithickernel:Linux
– One kernel provides all services.
– New paradigms are harder to implement
– May not be optimal for any one application
• Microkernel:Mach
– Microkernel provides minimal service
– Application servers provide OS functionality
• Nanokernel:OSisimplementedasapplicationlevel libraries
<h1>What is kernel?</h1>
The kernel is the central module of an operating system (OS). It is the part of the operating system that loads first, and it
remains in main memory. Because it stays in memory, it is important for the kernel to be as small as possible while still
providing all the essential services required by other parts of the operating system and applications. The the kernel code 
is usually loaded into a protected area of memory to prevent it from being overwritten by programs or other parts of the
operating system.
Typically, the kernel is responsible for memory management, process and task management, and disk management. The kernel
connects the system hardware to the application software. Every operating system has a kernel. For example the Linux kernel 
is used numerous operating systems including Linux, FreeBSD, Android and others.
 What types of Kernals do you know (architectures)?
1 Monolithic Kernels
Earlier in this type of kernel architecture, all the basic system services like process and memory management, interrupt
handling etc were packaged into a single module in kernel space. This type of architecture led to some serious drawbacks like 
1) Size of kernel, which was huge. 2) Poor maintainability, which means bug fixing or addition of new features resulted in 
recompilation of the whole kernel which could consume hours
In a modern day approach to monolithic architecture, the kernel consists of different modules which can be dynamically loaded 
and un-loaded. This modular approach allows easy extension of OS's capabilities. With this approach, maintainability of kernel
became very easy as only the concerned module needs to be loaded and unloaded every time there is a change or bug fix in a
particular module. So, there is no need to bring down and recompile the whole kernel for a smallest bit of change. Also, 
stripping of kernel for various platforms (say for embedded devices etc) became very easy as we can easily unload the module
that we do not want.
Linux follows the monolithic modular approach
2 Microkernels
This architecture majorly caters to the problem of ever growing size of kernel code which we could not control in the monolithic
approach. This architecture allows some basic services like device driver management, protocol stack, file system etc to run in
user space. This reduces the kernel code size and also increases the security and stability of OS as we have the bare minimum code 
running in kernel. So, if suppose a basic service like network service crashes due to buffer overflow, then only the networking
service's memory would be corrupted, leaving the rest of the system still functional.
In this architecture, all the basic OS services which are made part of user space are made to run as servers which are used by other
programs in the system through inter process communication (IPC). eg: we have servers for device drivers, network protocol stacks,
file systems, graphics, etc. Microkernel servers are essentially daemon programs like any others, except that the kernel grants some 
of them privileges to interact with parts of physical memory that are otherwise off limits to most programs. This allows some servers,
particularly device drivers, to interact directly with hardware. These servers are started at the system start-up.
What is an OS abstraction? What kind of Common OS abstractions do you know
An operating system abstraction layer (OSAL) provides an application programming interface (API) to an abstract operating system making
it easier and quicker to develop code for multiple software or hardware platforms.
OS abstraction layers deal with presenting an abstraction of the common system functionality that is offered by any Operating system by 
the means of providing meaningful and easy to use Wrapper functions that in turn encapsulate the system functions offered by the OS to
which the code needs porting. A well designed OSAL provides implementations of an API for several real-time operating systems 
(such as vxWorks, eCos, RTLinux, RTEMS). Implementations may also be provided for non real-time operating systems, allowing the abstracted
software to be developed and tested in a developer friendly desktop environment.
The OSAL consists of a set of interfaces (abstract classes) that provide all the required operating system services for the application, 
including:
Tasking services
Synchronization services
Message queues
Communication port
Timer service
These abstract interfaces need an implementation, which is a set of concrete classes that inherit from the abstract interfaces and 
provide an implementation for the pure, virtual operations defined in the interface. The OSAL enables you to encapsulate any RTOS by 
changing the implementation of the relevant framework classes (but not their interface) to meet the requirements of the given RTOS.

<h1>What is a system call?</h1>
When a program in user mode requires access to RAM or a hardware resource, it must ask the kernel to provide access to that resource. 
This is done via something called a system call.

When a program makes a system call, the mode is switched from user mode to kernel mode. This is called a context switch.

Then the kernel provides the resource which the program requested. After that, another context switch happens which results in change 
of mode from kernel mode back to user mode.

Generally, system calls are made by the user level programs in the following situations:

Creating, opening, closing and deleting files in the file system.
Creating and managing new processes.
Creating a connection in the network, sending and receiving packets.
Requesting access to a hardware device, like a mouse or a printer.
In a typical UNIX system, there are around 300 system calls. Some of them which are important ones in this context, are described below.
A system call is accomplished in Linux on x86 (i.e., Intel-compatible) processors by calling the interrupt 0x80 (i.e., int 0x80) together with the register values. A register is a very small amount of high speed memory inside of the CPU. int 0x80 is the assembly language instruction that is used to invoke system calls in Linux on x86 processors. The calling of this instruction is preceded by the storing in the process register of the system call number (i.e., the integer assigned to each system call) for that system call and any arguments (i.e., input data) for it.

<h1>How do system calls are handled by the CPU?</h1>
  The library functions
     typically invoke an instruction that changes the process execution mode
     to kernel mode and causes the kernel to start executing code for system
     calls.  The instruction that causes the mode change is often referred to
     as an "operating system trap" which is a software generated interrupt.
     The library routines execute in user mode, but the system call interface
     is a special case of an interrupt handler.  The library functions pass
     the kernel a unique number per system call in a machine dependent way --
     either as a parameter to the operating system trap, in a particular
     register, or on the stack -- and the kernel thus determines the specific
     system call the user is invoking.  In handling the operating system
     trap, the kernel looks up the system call number in a table to find the
     address of the appropriate kernel routine that is the entry point for
     the system call and to find the number of parameters the system call
     expects. 
 The kernel calculates the (user) address of the first
     parameter to the system call by adding (or subtracting, depending on the
     direction of stack growth) an offset to the user stack pointer,
     corresponding to the number of the parameters to the system call.
     Finally, it copies the user parameters to the "u area" and call the
     appropriate system call routine.  After executing the code for the
     system call, the kernel determines whether there was an error.  If so,
     it adjusts register locations in the saved user register context,
     typically setting the "carry" bit for the PS (processor status) register
     and copying the error number into register 0 location.  If there were no
     errors in the execution of the system call, the kernel clears the
     "carry" bit in the PS register and copies the appropriate return values
     from the system call into the locations for registers 0 and 1 in the
     saved user register context.  When the kernel returns from the operating
     system trap to user mode, it returns to the library instruction after
     the trap instruction.  The library interprets the return values from the
     kernel and returns a value to the user program.

<h1>What is process?</h1>
A process is an instance of a computer program that is being executed. It contains the program code and its current activity. Depending on the operating system (OS), a process may be made up of multiple threads of execution that execute instructions concurrently.
What is PCB?
Process Control Block (PCB, also called Task Controlling Block,[1] Entry of the Process Table,[2] Task Struct, or Switchframe) is a data structure in the operating system kernel containing the information needed to manage a particular process. The PCB is "the manifestation of a process in an operating system."
The role of the PCBs is central in process management: they are accessed and/or modified by most OS utilities, including those involved with scheduling, memory and I/O resource access and performance monitoring. It can be said that the set of the PCBs defines the current state of the operating system. Data structuring for processes is often done in terms of PCBs. For example, pointers to other PCBs inside a PCB allow the creation of those queues of processes in various scheduling states ("ready", "blocked", etc.) that we previously mentioned.

<h1>What are some common elements of any PCB’s?</h1>
In modern sophisticated multitasking systems, the PCB stores many different items of data, all needed for correct and efficient process management.[1] Though the details of these structures are obviously system-dependent, we can identify some very common parts, and classify them in three main categories:
Process identification data
Process state data
Process control data
The approach commonly followed to represent this information is to create and update status tables for each relevant entity, like memory, I/O devices, files and processes.

<h1>What is a Thread?</h1>
What threads add to the process model is to allow multiple executions to take place in the same process environment, to a large degree independent of one another. The thread has a program counter that keeps track of which instruction to execute next. It has registers, which hold its current working variables. It has a stack, which contains the execution history, with one frame for each procedure called but not yet returned from. Although a thread must execute in some process, the thread and its process are different concepts and can be treated separately. Processes are used to group resources together; threads are the entities scheduled for execution on the CPU.

How is Thread different from a process?
Both processes and threads are independent sequences of execution. The typical difference is that threads (of the same process) run in a shared memory space, while processes run in separate memory spaces.

Process
Each process provides the resources needed to execute a program. A process has a virtual address space, executable code, open handles to system objects, a security context, a unique process identifier, environment variables, a priority class, minimum and maximum working set sizes, and at least one thread of execution. Each process is started with a single thread, often called the primary thread, but can create additional threads from any of its threads.

Thread
A thread is an entity within a process that can be scheduled for execution. All threads of a process share its virtual address space and system resources. In addition, each thread maintains exception handlers, a scheduling priority, thread local storage, a unique thread identifier, and a set of structures the system will use to save the thread context until it is scheduled. The thread context includes the thread's set of machine registers, the kernel stack, a thread environment block, and a user stack in the address space of the thread's process. Threads can also have their own security context, which can be used for impersonating clients.
What is a virtual Memory?
Virtual memory is a memory management capability of an OS that uses hardware and software to allow a computer to compensate for physical memory shortages by temporarily transferring data from random access memory (RAM) to disk storage. Virtual address space is increased using active memory in RAM and inactive memory in hard disk drives (HDDs) to form contiguous addresses that hold both the application and its data.

<h1>What is a virtual memory map?</h1>
The computer's operating system, using a combination of hardware and software, maps memory addresses used by a program, called virtual addresses, into physical addresses in computer memory. Main storage, as seen by a process or task, appears as a contiguous address space or collection of contiguous segments.

What is an MMU?
A memory management unit (MMU), sometimes called paged memory management unit (PMMU), is a computer hardware unit having all memory references passed through itself, primarily performing the translation of virtual memory addresses to physical addresses. It is usually implemented as part of the central processing unit (CPU), but it also can be in the form of a separate integrated circuit.
An MMU effectively performs virtual memory management, handling at the same time memory protection, cache control, bus arbitration and, in simpler computer architectures (especially 8-bit systems), bank switching.
