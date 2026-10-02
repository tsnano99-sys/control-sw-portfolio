# Taeseung Kim — Equipment Control Software Engineer Portfolio

Equipment control software engineer with 5+ years of experience developing C#/.NET and C++ software for semiconductor handling and process equipment — memory test handlers, laser drilling, laser marking, and dispensing systems. Experienced across the full lifecycle, from requirement analysis and design to deployment and on-site debugging in customer cleanroom environments.

📧 tsnano99@gmail.com

---

## Core Competencies

- **Multi-axis motion control** — 40+ axis synchronized motion, sequence profiling and bottleneck analysis, buffer-based look-ahead scheduling
- **Equipment communication protocols** — TCP/IP, RS-232/485, SCPI; priority-queue command scheduling with retry/timeout handling for asynchronous device control
- **SECS/GEM (HSMS) & MES integration** — host event reporting (S6F11) and process gating on host response (S6F12), adapted to customer-specific host implementations
- **Hardware–software root-cause analysis** — isolating issues across vision hardware, communication, and control logic under live production constraints
- **On-site field support** — cleanroom tool setup and production-line support at overseas customer sites (China, Vietnam)
- **Self-directed tooling** — identifying recurring field problems and independently designing, building, and shipping internal diagnostic tools

## Tech Stack

| Category | Details |
|---|---|
| Languages & Frameworks | C# (.NET Framework, WinForms), C++, Python |
| Software Design | Object-oriented design, state machine pattern, multi-threaded asynchronous processing, priority-queue scheduling |
| Communication | TCP/IP, RS-232, RS-485, SECS/GEM (SECS-II, HSMS), SCPI |
| Data & Visualization | SQLite, MySQL, OpenGL, pandas, matplotlib |
| Tools | Git, SVN, Bitbucket, Jira, Visual Studio |
| Others | Quadtree spatial partitioning, DXF/Gerber import, LLM API integration (OpenAI/Claude) |

## Experience Summary

| Period | Company | Key Responsibilities |
|---|---|---|
| Mar 2026 – Present | APTEC Co., Ltd. | Control software for semiconductor packaging equipment (dispensing, stiffener attach, laser marking) |
| Feb 2024 – Mar 2026 | KOSES Co., Ltd. | Laser/scanner equipment control software; requirement analysis through deployment |
| Jan 2022 – Mar 2023 | EO Technics Co., Ltd. | Multi-axis motion control for laser drilling equipment; overseas cleanroom setup (Vietnam) |
| Jul 2020 – Sep 2021 | Techwing Inc. | Memory test handler control logic development and on-site troubleshooting |

---

## Projects

### 1. Dispenser Sequence Optimization (UPH +33%)

**Context**: A 40+ axis dispenser's throughput was capped by an unidentified wait bottleneck in the index-axis motion sequence.

**Approach**
- Profiled 48 production sequences through log analysis to pinpoint where the index axis stalled waiting on upstream steps
- Redesigned the flow with buffer-based look-ahead processing, allowing downstream axes to proceed without waiting on strict step completion
- Structured magazine and tray handling as a state machine with pre-execution map re-validation to preserve data consistency under the new flow

**Result**: Increased UPH from 600 to 800 (+33%) with no loss of placement accuracy or data integrity

---

### 2. Multi-threaded Laser Communication Module (99.9% Success Rate)

**Context**: A laser controller accepted only one command at a time, but both interactive UI commands and a periodic status-polling thread needed to issue commands concurrently without blocking or corrupting state.

**Approach**
- Implemented 40+ SCPI commands over TCP/IP and RS-232
- Serialized asynchronous UI commands and periodic polling through a single priority queue, so polling never starved or collided with user-initiated commands
- Added retry and timeout handling around each transaction to recover from transient communication failures

**Result**: Achieved a 99.9% communication success rate in production operation

---

### 3. Precision Pin-Placement Verification Tool

**Context**: Fixture pin layouts were verified manually against DXF/Gerber design files, which was slow and error-prone at micron-level tolerances.

**Approach**
- Imported industry-standard DXF/Gerber design files and visualized pins, fiducials, leads, and components by layer using OpenGL
- Implemented µm-level interference (overlap) checks using quadtree spatial partitioning for efficient proximity queries
- Built an extensible, polymorphism-based shape model so new component/pin shapes could be added without changing the core verification logic

**Result**: Reduced setup/verification time from 10 minutes to 1 minute and error rate from 20% to under 1%

---

### 4. Log Analysis Tool with AI-assisted Diagnostics

**Context**: Diagnosing equipment faults required manually searching through large, unstructured log files — slow and inconsistent across engineers.

**Approach**
- Streamed and indexed 100,000+ log records into SQLite, with search/filtering by time, level, module, and keyword
- Optimized large-dataset display using WinForms Virtual Mode to keep the UI responsive at scale
- Integrated an LLM (GPT-based) log Q&A feature so engineers could ask natural-language questions about a session's logs
- Added automated error-trend visualization to support pattern recognition over time

**Result**: Substantially reduced time-to-diagnosis and gave engineers a consistent first-pass triage tool

---

### 5. SECS/GEM (HSMS) MES Integration

**Context**: Dispensing equipment needed to report production data to the customer's MES and respect host-controlled process gating, with each customer's host interpreting the standard slightly differently.

**Approach**
- Implemented SECS/GEM over HSMS, reporting lot and quantity data via S6F11 event reports
- Gated process start on the host's S6F12 response rather than proceeding unconditionally
- Resolved host-specific interpretation differences through integration testing with each customer

**Result**: Stable MES integration across multiple customer hosts with correct event sequencing and process gating

---

### 6. Automatic Serial Device Discovery Tool

**Context**: In a field with many types of serial-connected peripherals (temperature controllers, pulse heaters, air controllers, precision scales), manually mapping COM ports to devices was a recurring source of human error — the problem was self-identified and the tool was independently designed and built.

**Approach**
- Iterated over COM port × baud rate combinations, sending each device type's identify command and validating the response against known device signatures
- Modularized device-recognition logic with a probe pattern, so new device types could be registered in the field without recompilation
- Used asynchronous processing to scan multiple ports concurrently while keeping the UI responsive

**Conceptual flow** *(simplified pseudocode for illustration, not the actual implementation)*
```
for each COM port:
    for each candidate baud rate:
        open connection
        send identify_command
        response = read_response(timeout)
        if validate(response) matches known device signature:
            register device(port, baud_rate, device_type)
```

**Result**: New devices could be onboarded in the field without code changes, eliminating the manual-identification errors it replaced

---

## Field Debugging Highlight

While supporting a customer production line in China from tool setup through stable auto-run, vision calibration values intermittently failed to apply. By narrowing the scope step by step — vision hardware, communication, then control logic — the root cause was identified within 30 minutes and the fix was verified by reproducing the original failure conditions.

---

## Note

- Projects reflect actual work performed in production roles. Source code is proprietary to each employer and is not published here; this portfolio describes approach, design decisions, and measured results.
- Code snippets shown are simplified, generalized pseudocode for illustration — not the actual implementation.
