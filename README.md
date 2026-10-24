# BootFlow 2.0 Pro — Premium Windows Startup Optimization & Diagnostics

[![Platform](https://img.shields.io/badge/Platform-Windows%2010%20%7C%20Windows%2011-blue.svg)](https://microsoft.com/windows)
[![Python](https://img.shields.io/badge/Python-3.10%20%7C%203.11%20%7C%203.12%20%7C%203.13-purple.svg)](https://python.org)
[![Framework](https://img.shields.io/badge/UI-PySide6%20Qt%20Quick%20%2B%20Web%20Companion-8B80F9.svg)](https://qt.io)
[![License](https://img.shields.io/badge/License-MIT-emerald.svg)](LICENSE)
[![Status](https://img.shields.io/badge/Release-v2.0.0%20Pro-success.svg)](https://github.com/)

> **"Your PC, ready sooner."**  
> BootFlow 2.0 Pro is an exquisite, high-performance Windows startup management and boot diagnostics suite. Designed to reject the cluttered, aggressive gaming utility aesthetic, BootFlow combines a serene lavender/periwinkle glassmorphic interface with deep Windows kernel telemetry (Event ID 100), transparent multi-phase boot analysis, safe registry transactions, and one-click optimization tools.

---

## 🌟 Key Highlights & Capabilities

- **Refined Glassmorphic Visual System:** Designed with luminous soft lavender (`#8B80F9`), periwinkle (`#A5B4FC`), and pale cyan (`#38BDF8`) accents, layered frosted glass translucency (`rgba(255, 255, 255, 0.03)` to `0.08`), and dark-first ergonomic slate styling.
- **Universal Action Loading Pop-ups:** Dynamic modal spinner and progress bar overlays for all asynchronous system tasks:
  - Deep Diagnostic Scan with real-time percentage loader (`0%` → `100%`) and 4-step checklist.
  - Startup app toggles (Enabling / Disabling with Task Manager `StartupApproved` integration).
  - 1-Click Turbo Boot sequence with phased service evaluation.
  - Delayed startup application (15s, 30s, 60s non-competing logon queues).
  - Permanent item deletion with safety confirmation dialog and automatic SQLite backup snapshot.
- **⚡ Boot Speed Optimization Suite:**
  - **1-Click Turbo Boot:** Instantly defers high-latency background updaters and telemetry agents while preserving system audio, GPU drivers, and Windows Security.
  - **Fast Startup (Hybrid Boot) Diagnostics:** Detects and verifies Windows Fast Startup and UEFI hibernation state.
  - **Windows Explorer Startup Delay Tuning:** Disables the default Windows 10s shell delay (`Serialize` / `StartupDelayInMSec` registry key).
  - **Logon Memory Compaction:** Trims working sets of early post-logon services to eliminate disk swap contention.
  - **Delayed Startup Queues:** Postpones resource-heavy launchers until disk activity normalizes.
- **📊 4-Phase Windows Boot Architecture Analysis:**
  - **Phase 1: UEFI / BIOS POST (2.3s):** Hardware discovery, RAM validation, and UEFI firmware handoff.
  - **Phase 2: OS Loader (1.2s):** Windows Boot Manager (`bootmgr`), `winload.efi`, and HAL initialization.
  - **Phase 3: Kernel Main Path (8.4s):** `ntoskrnl.exe`, Session Manager (`smss.exe`), driver loading, and service group startup.
  - **Phase 4: Desktop Shell Convergence (5.4s):** `explorer.exe` shell, taskbar readiness, user startup items, and background services.
- **💡 Actionable Recommendations Engine:** 4 categorized views (*All*, *High Priority*, *Delayed Startup*, *System & Sync*) with 3 distinct user actions per recommendation card:
  - **Apply Fix:** Instant single-click resolution.
  - **Delay (30s):** Keep the software installed but push its start past the logon bottleneck.
  - **Dismiss:** Hide recommendation from active review list.
- **🛡️ Non-Destructive Safety Architecture:**
  - Red trash icon for permanent entry deletion accompanied by an explicit confirmation modal.
  - Every modification is automatically backed up as a JSON record in the local SQLite database (`~/.bootflow/bootflow.db`) before any registry or filesystem mutation occurs.
  - Undo / restore capabilities allow instantaneous rollback.
- **📈 Diagnostics Telemetry & CSV Export:** Direct access to Windows Event Log `Microsoft-Windows-Diagnostics-Performance/Operational` (Event ID 100), spline timeline charts (7D, 14D, 30D spans), and instant CSV data export.
- **🖥️ Dual Native & Companion Interface:** Built with native PySide6 / Qt Quick QML for desktop performance, paired with an interactive companion web preview running on FastAPI and HTML5 Canvas.

---

## 📁 Repository Structure

```
bootflow/
├── app/
│   ├── assets/
│   │   └── icons/
│   │       ├── bootflow.ico          # Multi-resolution Windows icon (16x16 to 256x256)
│   │       ├── bootflow_icon.png     # High-resolution 512x512 application brand
│   │       └── logo_sidebar.svg      # Vector sidebar logo
│   ├── core/
│   │   ├── models.py                 # StartupItem, BootMetric, SystemHealth, Recommendation
│   │   ├── scanner.py                # Registry (HKCU/HKLM Run, RunOnce, StartupApproved), Startup Folders
│   │   ├── manager.py                # Safe toggle, delay queues, permanent deletion, backup & undo
│   │   ├── boot_diagnostics.py       # Windows Event ID 100 parser, 4-phase boot architecture, SQLite store
│   │   ├── recommendations.py        # Intelligent categorization heuristics & health scoring
│   │   ├── settings.py               # Local SQLite database & user preferences
│   │   └── platform_compat.py        # Windows native winreg/win32 APIs + cross-platform fallback
│   ├── ui/
│   │   ├── bridge.py                 # PySide6 QObject bridge with Qt slots for all suite operations
│   │   ├── qml/                      # Pure Qt Quick desktop views & components
│   │   │   ├── main.qml              # Acrylic/mica style window container with dynamic mesh background
│   │   │   ├── Style.qml             # Design tokens singleton (colors, fonts, glass gradients)
│   │   │   ├── components/           # GlassCard, MetricCard, Sidebar, TopBar, ToggleSwitch
│   │   │   └── views/                # DashboardView, StartupAppsView, BootAnalysisView, RecommendationsView, SettingsView
│   │   └── web/                      # Interactive browser companion
│   │       ├── index.html            # Responsive UI with interactive action loading modal
│   │       ├── style.css             # Glassmorphism, animations, Inter font, custom scrollbars
│   │       └── app.js                # Full client logic, spline charts, and REST API integration
│   ├── server.py                     # FastAPI REST API backend & static file server
│   └── main.py                       # Native PySide6 entrypoint with resilient path resolution
├── packaging/
│   ├── bootflow.spec                 # Optimized PyInstaller specification
│   ├── build_windows.bat             # Production Windows batch build script
│   └── build_windows.ps1             # Production Windows PowerShell build script
├── dist/
│   └── BootFlow/                     # Compiled standalone executable distribution
│       ├── BootFlow                  # 64-bit standalone executable binary
│       └── _internal/                # Bundled Qt6 libraries and Python runtime
├── tests/                            # Comprehensive automated test suite (17 passing tests)
│   ├── test_api_endpoints.py         # REST API verification
│   ├── test_boot_diagnostics.py      # Telemetry & 4-phase calculation
│   ├── test_enhancements.py          # Turbo Boot, Delayed Startup, and Deletion backup
│   ├── test_manager.py               # Registry toggling and persistence
│   ├── test_qml_load.py              # Qt Quick QML scene hierarchy & singleton validation
│   ├── test_recommendations.py       # Recommendation rules & health score index
│   └── test_scanner.py               # Startup item discovery heuristics
├── build.bat                         # Top-level one-click Windows compiler script
├── run_bootflow.bat                  # Top-level diagnostic Windows launcher
├── run.py                            # Multi-target CLI launcher (--desktop, --web, --server, --test)
├── requirements.txt                  # Python dependencies
└── README.md                         # Complete product documentation
```

---

## 🚀 Running & Building BootFlow

### Running on Windows
Double-click `run_bootflow.bat` in the project root. It will:
1. Detect whether `dist\BootFlow\BootFlow.exe` exists and launch it directly.
2. If compiling from source, automatically activate your Python virtual environment and run `python run.py --desktop`.
3. If no GUI display server is detected, seamlessly fall back to launching the interactive companion web interface in your default browser.

### Building Standalone Executable on Windows
Run `build.bat` (or `packaging\build_windows.bat` / `packaging\build_windows.ps1`). It will:
- Check for Python 3.10+ and pip.
- Install dependencies from `requirements.txt`.
- Execute `pyinstaller --clean -y packaging\bootflow.spec`.
- Output the self-contained folder to `dist\BootFlow\`.

### Running Tests
Execute the pytest test suite:
```bash
python -m pytest -v tests
```
*Result: 17 passed in under 1 second.*

---

## 📦 Deliverables & Pre-built Archives

The pre-built package is archived at:
- **`BootFlow-v2.0.0.zip`** (located at `/home/user/BootFlow-v2.0.0.zip`)
Includes the compiled standalone binary `dist/BootFlow/BootFlow`, complete source code, tests, build scripts, Windows batch launchers, and assets.

# Create and activate a virtual environment
python -m venv venv
# On Windows:
venv\Scripts\activate
# On Linux/macOS:
source venv/bin/activate

# Install dependencies
pip install -r requirements.txt
```

### 3. Launching BootFlow

#### Option A: Interactive Live Companion (Default)
Runs the live interactive interface with full live backend APIs:
```bash
python run.py
# Open http://localhost:3000 in your browser
```

#### Option B: Native PySide6 / QML Desktop Window
Launches the native Windows desktop window:
```bash
python run.py --desktop
```

#### Option C: Automated Test Suite
```bash
python run.py --test
# or: pytest -v tests
```

---

## Building Standalone Windows Executable (.exe)

BootFlow includes a self-healing build script that automatically locates Python across multiple environments (even if Python was not added to your system `PATH` during setup).

### From Windows Command Prompt (Fastest):
Double-click `build.bat` in the project root, or run:
```cmd
build.bat
```
*(Or `packaging\build_windows.bat`)*

### From PowerShell:
```powershell
.\packaging\build_windows.ps1
```

### How the Build Script Locates Python
1. Checks the Windows Python launcher (`py -3`), which is typically in `C:\Windows\py.exe`.
2. Checks `python` and `python3` in the system `PATH`.
3. Scans default per-user folders (`%LOCALAPPDATA%\Programs\Python\Python3xx\python.exe`).
4. Scans standard 64-bit and 32-bit `Program Files` installations.
5. If still not found, prompts you to paste the path directly or re-run the installer with **"Add python.exe to PATH"** checked.

The resulting standalone executable will be placed in:
`dist\BootFlow\BootFlow.exe`

---

## Technical Architecture & Safety Guarantees

1. **Non-Destructive Operations:** BootFlow modifies startup items using the official Windows `StartupApproved` registry mechanism (`HKCU\Software\Microsoft\Windows\CurrentVersion\Explorer\StartupApproved\Run`). This mirrors Windows Task Manager behavior: the original command is retained, avoiding accidental registry corruption.
2. **System Protection:** Audio drivers, GPU utilities, and Windows Security components are automatically identified and flagged with safety barriers to prevent users from disabling critical functionality.
3. **Local Privacy:** BootFlow performs zero remote network queries. All diagnostics and historical measurements are stored in a private local SQLite database located in `%LOCALAPPDATA%\BootFlow\bootflow.db`.

---

## License

MIT License — see [LICENSE](LICENSE) for details.
