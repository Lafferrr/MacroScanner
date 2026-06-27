# Laffer's Macro Scanner

## ⚠️ Antivirus Notice

This tool **will be flagged as suspicious by some antiviruses**. This is a false positive.

- The tool reads **process memory** of `dwm.exe`, `powershell.exe`, `pwsh.exe`, `conhost.exe`, `ctfmon.exe`, `explorer.exe`, `taskhostw.exe` and others — behavior that overlaps with generic AV heuristics
- The tool enumerates **USN journals**, **prefetch files**, **registry Run keys**, **UserAssist**, **BAM**, **RecentDocs** and **ActivityCache** — same surfaces malware kits touch
- The tool embeds **encrypted detection signatures** and ships with **anti-debug** checks (`IsDebuggerPresent`, `NtQueryInformationProcess` with `ProcessDebugPort`) — patterns that AV heuristics sometimes score
- **The tool does NOT upload any data** — all analysis is 100% local
- **The tool does NOT modify any file** — read-only at every step (the only writes are to `C:\SSTools\MacroScanner\MacroScannerResults.txt`, the report file)


## Usage

Download and run `MacroScanner.exe` as **Administrator**. Admin rights are required because:

At startup you'll see the main window with an animated starfield, three nebula clouds, two drifting planets, a translucent glass title bar, and a stat-card strip. Press **Start Scan** to begin a full sweep of every fixed drive on the machine.

## Severity Model

Every result is assigned a severity based on the **number of keywords** matched:

| Keywords | Severity |
|----------|----------|
| 1        | LOW      |
| 2        | MEDIUM   |
| 3        | HIGH     |
| 4+       | CRITICAL |

## Detection Categories (Group Order)

Results in the GUI and report are grouped in this exact order:

1. **A–Z extension categories** — AHK Scripts, AMC2 Macros, AU3 Scripts, Automation Scripts, CueCfg Macros, JS Automation, KBS Macros, Lua Scripts, MCR Macros, PowerShell Scripts, Python Script Files, Python Window Script Files, Sh Scripts, TS Automation, VBS Scripts
2. **DWM Macro Strings**
3. **Macro Window Strings**
4. **USN Journal Evidence** (Soon)
5. **Cmd.exe Evidence** (Soon)
6. **Powershell.exe Evidence** (Soon)
7. **Conhost.exe Evidence** (Soon)
8. **External USB Drive** (Soon)
9. **FAT32/ExFAT Drive** (Soon)
10. **Virtual Machine Detection** (Soon)
11. **Activities Cache** (Soon)
12. **Prefetch Evidence** (Soon)
13. **Registry Evidence** (Soon)
14. **Suspicious Active Scripts** 
15. **Suspicious Scripts Ran**
16. **Suspicious Processes**
17. **Suspicious PowerShell Activity** (Soon)
18. **Memory Access Artifact** (Soon)
19. **Potential Shellcode Injection** (Soon) 
20. **Portable Executables** (Soon)
21. **Executed File Without Extension** (Soon)
22. **And More**

Each group header shows the count: `AHK Scripts (12)`, `DWM Macro Strings (3)`, etc. Empty groups are hidden.


## Output

The GUI shows:
- **Title bar** with the app name + min / max / close buttons (drawn over the animated scene)
- **Phase label** (e.g. `Scanning Files (45.2%)`) + **percent label**
- **Start Scan** / **Open Report** buttons
- **Progress bar** (0–100%)
- **Stat-card strip**: Files Scanned, Total Found, Critical, High, Medium, Low — each card is a clickable filter
- **ListView** with columns: RISK, NAME, PATH, KEYWORDS, MODIFIED, SCORE — grouped by category, color-coded by risk

Results stream in **real time** during the scan — every 80 ms, the queue is drained and the ListView is rebuilt so you see categories filling up as the scan progresses.

Severity colors:
- 🟢 **LOW** — green `RGB(63, 185, 80)`
- 🟡 **MEDIUM** — yellow `RGB(255, 212, 0)`
- 🟠 **HIGH** — orange `RGB(255, 148, 0)`
- 🔴 **CRITICAL** — red `RGB(248, 81, 73)`

The report file is written to `C:\SSTools\MacroScanner\MacroScannerResults.txt` with categorized sections matching the GUI order, plus a risk summary at the bottom.
