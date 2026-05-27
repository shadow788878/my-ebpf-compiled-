# CoreSystem v4.2: Scalable Shield Active

CoreSystem is an advanced, low-overhead eBPF utility designed to demonstrate process, file, and network port isolation at the Linux kernel level. By hooking into directory entry layout syscalls (`getdents64`), CoreSystem selectively filters kernel-space structures inline, modifying user-space memory buffers on the fly to seamlessly hide designated PIDs and Inodes from tracking utilities.

---

## ⚡ Key Features

* **PID Obfuscation**: In-memory removal of processes from `/proc` by intercepting system-wide directory loops.
* **Inode Cloaking**: Live filtering of targeted directories and inodes via user-space buffer manipulation.
* **Network Interface Attachment**: Integrates standard user-space structures (`libbpf`) with a `tc_network_shield` architecture for handling network infrastructure isolation.
* **Persistent State Tracking**: Utilizes global pinned BPF maps (`/sys/fs/bpf/`) to control system configuration state fluidly without unloading the kernel bytecode.

---

## 🏗️ Architecture & Internals

The framework relies on cooperative execution between a kernel-level sandbox hook and an authorized user-space operator:
