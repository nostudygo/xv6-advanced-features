# xv6-Advanced-Features

This repository contains a series of advanced features implemented on the **xv6 operating system** (MIT 6.S081), including:

- ✅ **Copy-on-Write (COW)**: Optimized `fork()` by sharing pages and copying only when written.
- ✅ **Lazy Allocation**: Memory is allocated only when first accessed, reducing initial memory usage.
- ✅ **Trace System Call**: Dynamically trace specific system calls using a bitmask.
- ✅ **LRU + Swap Mechanism**: Implement virtual memory with swap space to support larger virtual address spaces.

> This project is based on the RISC-V version of xv6 (from MIT 6.S081).

---

## 🛠 Features Implemented

### 1. Copy-on-Write (COW)
- Modified `fork()` to share physical pages between parent and child.
- Pages are copied only on write (page fault).
- Uses reference counting for shared pages.

### 2. Lazy Allocation
- `sbrk()` only extends virtual address space.
- Physical pages are allocated on first access via page fault handler.
- Reduces memory footprint during process startup.

### 3. Trace System Call
- Added `trace(mask)` system call to enable/disable tracing of specific syscalls.
- Logs format: `<pid>: <syscall_name> -> <retval>`
- Supports bitmask filtering (e.g., `1 << SYS_read`).

### 4. LRU + Swap (Virtual Memory)
- Implements a simple swap mechanism using disk blocks.
- Uses RISC-V PTE's A/D bits for LRU approximation.
- When physical memory is full:
  - Scans all processes to find least recently used page.
  - If dirty, writes it to swap area.
  - Updates PTE to mark as swapped-out.
- On page fault, swaps in from disk if needed.

---

## 🗂 Project Structure
