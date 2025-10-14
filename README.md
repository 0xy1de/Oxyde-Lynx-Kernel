# 🐾 Oxyde Lynx Kernel
### Fast • Fluid • Focused — The Heart of Oxyde Desktop

**Oxyde Lynx Kernel** is a custom-tuned Linux kernel derived from **XanMod 6.16.x**, optimized for **Aero-style compositing** and ultra-low memory usage (< 1 GB total desktop footprint).  
It powers **Oxyde Desktop** and **LinX OS**, blending modern Linux performance with the responsive, glass-smooth feel of classic macOS and early-2000s UX design.

---

## ✨ Key Features
- 🧠 **Low-Latency Scheduling** – Dynamic preemption (`PREEMPT_DYNAMIC`) and 1000 Hz timer for immediate input feedback  
- 🧊 **Memory Efficiency** – Lean configuration, optional ZRAM/ZSWAP (ZSTD), minimal debug overhead  
- ⚙️ **I/O Optimization** – Default **BFQ** (HDD) / **MQ-Deadline** (SSD/NVMe) profiles  
- 🌐 **Network Performance** – BBR v2 congestion control + optional Cake QoS  
- 🧩 **Desktop Responsiveness** – Tuned CFS autogrouping and `schedutil` governor pairing for instant GUI reaction  
- 💡 **Aesthetic Focus** – Built for smooth glass effects, blur compositing, and animation timing under **Oxyde Compositor**  
- 🔒 **Stable Core** – Based on **XanMod 6.16.x** (Linux 6.16 stable branch with XanMod latency patches)

---

## 🧱 Build Instructions
> Target: Manjaro / Arch / Debian-based systems  
> You’ll need basic build tools (`gcc`, `make`, `bc`, `libncurses-dev`, etc.)

```bash
git clone https://github.com/yourname/oxyde-lynx-kernel.git
cd oxyde-lynx-kernel

# Optional: use XanMod baseline config
cp CONFIGS/x86_64/xanmod.config .config
make olddefconfig

# Build and install
make -j"$(nproc)"
sudo make modules_install install
```

On next boot, choose **Oxyde Lynx Kernel** from your GRUB menu.

---

## 🧩 Recommended Runtime Tunings
Create `/etc/sysctl.d/99-oxyde-lynx.conf`:
```conf
vm.swappiness = 15
vm.vfs_cache_pressure = 50
vm.dirty_background_ratio = 5
vm.dirty_ratio = 15
net.core.default_qdisc = fq_codel
net.ipv4.tcp_congestion_control = bbr
```

Optional ZRAM setup (example):
```bash
modprobe zram num_devices=1
echo lz4 > /sys/block/zram0/comp_algorithm
echo 2G > /sys/block/zram0/disksize
mkswap /dev/zram0 && swapon /dev/zram0
```

---

## 🔬 Configuration Philosophy
- Eliminate bloat, keep essential modules only  
- Prioritize **latency** and **interactivity** over synthetic benchmarks  
- Maintain balance between **modern drivers** and **retro resource efficiency**  
- Stay **fully compatible** with Oxyde Compositor and LinX OS stack  

---

## 🧭 Roadmap
- [ ] 6.17 rebase for extended support  
- [ ] Real-time audio and graphics profile  
- [ ] Optional LLVM/Clang build path  
- [ ] Hybrid scheduler exploration (EEVDF / CFS tuning)  
- [ ] ARM64 target testing for low-power devices  

---

## 📜 License
This project follows the **GPL-2.0** license, consistent with the upstream Linux kernel.  
Additional configuration and branding files © 2025 Nick Chiaravalle under the **MPL-2.0** license.

---

## 🦊 Credits
- **Upstream:** [XanMod Linux](https://xanmod.org) & [Linux Kernel Developers](https://kernel.org)  
- **Project Lead:** Nick Chiaravalle  
- **Part of:** [Oxyde Desktop Environment](https://github.com/Oxyde-Desktop) / [LinX OS](https://github.com/LinX-OS)

---

> “Fast like a Lynx, light as air — where precision meets performance.”
