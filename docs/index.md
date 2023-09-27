# The RISC-V Instruction Set Manual
## Volume II: Privileged Architecture
### Document Version 20211203

# Preface
Bu dökümanda RISC-V Privelege mimarisi açıklanmıştır.
Versiyon : 20211203
Aşağıdaki RISC-V ISA modüllerini içerir

![image](https://user-images.githubusercontent.com/68472927/216995802-5efacdce-f22c-44e4-9da5-bbfd4f4f8734.png)

### Değişiklikler kısmı çevrilmedi
Added optional big-endian and bi-endian support.
Made priority of load/store/AMO address-misaligned exceptions implementation-defined relative to load/store/AMO page-fault and access-fault exceptions.
PMP reset values are now platform-defined.
 An additional 48 optional PMP registers have been defined.
 Slightly relaxed the atomicity requirement for A and D bit updates performed by the implementation.
 Clarify the architectural behavior of address-translation caches.
 Added Sv57 and Sv57x4 address translation modes.
 Clarified that bare S-mode need not support the SFENCE.VMA instruction.
Specified relaxed constraints for implicit reads of non-idempotent regions.
Added the Svnapot Standard Extension, along with the N bit in Sv39, Sv48, and Sv57 PTEs
Added the Svpbmt Standard Extension, along with the PBMT bits in Sv39, Sv48, and Sv57 PTEs.
Added the Svinval Standard Extension and associated instructions.
Finally, the hypervisor architecture proposal has been extensively revised.
----------------------------------------------

# Preface to Version 1.11
This is version 1.11 of the RISC-V privileged architecture. The document contains the following
versions of the RISC-V ISA modules:
![image](https://user-images.githubusercontent.com/68472927/216997984-b180641d-c6e0-4422-b10a-f42cbe8887b0.png)
versityon 1.10 üzerinde yapılan değişikler
- The virtual-memory system no longer permits supervisor mode to execute instructions from user pages, regardless of the SUM setting.
- Clarified that ASIDs are private to a hart, and added commentary about the possibility of a future global-ASID extension.
- SFENCE.VMA semantics have been clarified.
- Required all harts in a system to employ the same PTE-update scheme as each other
- Described scheme for emulating misaligned AMOs.
- Specified the behavior of the misa and xepc registers in systems with variable IALIGN.
-  Specified semantics for PMP regions coarser than four bytes.



# Chapter 1
## Introduction
Bu döküman RISC-V privelege mimarisini açıklar. Unprivlege modun yanı sıra operating system çalıştırmak ve harici cihazlarla bağlantı sağlamak için ekstra fonsiyonelliklerin eklenmesi gerekmektedir.

# 1.1 RISC-V Privileged Software Stack Terminology
![image](https://user-images.githubusercontent.com/68472927/217001227-aea9b7b6-c0ec-484d-b199-74cbbb3190c0.png)
https://github.com/riscv/riscv-glossary/blob/main/glossary.adoc


https://github.com/riscvarchive/riscv-software-list



