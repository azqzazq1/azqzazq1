<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0B0B0B,35:5A0000,65:B00000,100:FF0000&height=260&section=header&text=azqzazq1&fontSize=84&fontColor=ffffff&animation=fadeIn&fontAlignY=36&desc=Security%20Researcher%20%7C%20Red%20Team%20Engineer%20%7C%20CVE%20Analyst&descSize=18&descAlignY=58" />

<br/>

<img src="https://readme-typing-svg.demolab.com?font=Fira+Code&weight=500&size=18&pause=1200&color=FF3131&center=true&vCenter=true&width=900&lines=I+research+how+systems+break.;Kernel+Security+%7C+Privilege+Escalation+%7C+Red+Team+Operations;Exploit+Path+Analysis+%7C+CVE+Research+%7C+Reverse+Engineering;Observation+is+not+always+reality." />

<br/><br/>

<img src="https://img.shields.io/badge/RED_TEAM-OPERATIONS-FF0000?style=for-the-badge&labelColor=111111" />
<img src="https://img.shields.io/badge/CVE-RESEARCH-B00000?style=for-the-badge&labelColor=111111" />
<img src="https://img.shields.io/badge/KERNEL-SECURITY-8B0000?style=for-the-badge&labelColor=111111" />
<img src="https://img.shields.io/badge/LINUX-PRIVESC-C0392B?style=for-the-badge&logo=linux&logoColor=white&labelColor=111111" />

<br/><br/>

<img src="https://komarev.com/ghpvc/?username=azqzazq1&color=red&style=for-the-badge" />

</div>

---

# `whoami`

```yaml
handle: azqzazq1

roles:
  - Security Researcher
  - Red Team Engineer
  - Vulnerability Analyst
  - System-Level Security Specialist

focus:
  - Linux / Windows privilege boundaries
  - Offensive security research
  - Cloud & container attack surfaces
  - Root cause analysis & exploit path engineering
  - Coordinated disclosure & CVE research

philosophy:
  - systems are layered trust models
  - assumptions fail before software does
  - observation is not always reality
````

---

# `./featured_research`

## 🧨 CVE-2026-7867 — Coordinated Vulnerability Research

Research conducted on a Linux system component involving authorization logic and privilege boundary handling.

The issue was identified during advanced Red Team and system-level security research and responsibly disclosed to the vendor.

```diff
+ Research Area   : Linux Authorization Logic
+ Scope           : Privilege Boundary Analysis
+ Disclosure      : Coordinated with Vendor
+ CVE Status      : Assigned
- Technical Data  : Temporarily Withheld
```

> Full technical analysis and root cause breakdown will be published after coordinated disclosure timelines are completed.

---

## 🧊 IceWarp CVE-2025-14500 — Root Cause & Reverse Engineering

World-first technical analysis of IceWarp CVE-2025-14500, including root cause review and exploitation surface mapping.

```diff
+ Research Type   : Reverse Engineering
+ Focus           : Exploitation Surface Mapping
+ Output          : Public Technical Analysis
+ Status          : Published
```

<div align="center">

<a href="https://mileniumsec.com/blog/icewarp-cve-2025-14500-root-cause-reverse-engineering">
<img src="https://img.shields.io/badge/READ_ANALYSIS-MileniumSec-FF0000?style=for-the-badge&labelColor=111111" />
</a>

</div>

---

# `./red_team_research`

## 🔴 eBPF Telemetry Redaction — Kernel-Level Red Team Technique

A Red Team research technique focused on changing what defensive systems believe they observed.

Instead of disabling telemetry or terminating agents, this research explores runtime syscall observation and controlled data transformation using eBPF.

```diff
+ Technique   : eBPF Telemetry Redaction
+ Layer       : Syscall Observation Layer
+ Surface     : Security Telemetry Streams
+ Model       : Runtime Data Transformation
+ Principle   : Observation ≠ Reality
```

<div align="center">

<a href="https://www.youtube.com/watch?v=5CiSSglRJeo&t=4s">
<img src="https://img.shields.io/badge/WATCH_RESEARCH_DEMO-YouTube-FF0000?style=for-the-badge&logo=youtube&logoColor=white&labelColor=111111" />
</a>

</div>

---

```text
NORMAL TELEMETRY FLOW

process → syscall → agent → SIEM → analyst


RESEARCHED ATTACK MODEL

process → syscall → eBPF layer → agent → SIEM
                          └─ selective transformation
```

> Security systems do not directly observe reality.
> They observe interpreted runtime data streams.

---

## 🔴 LID(Linux Integrity Drift)
A Red Team research technique that bypasses AppArmor mandatory access control using eBPF — without disabling it, without modifying it, and without leaving a single audit log entry.

LID attaches a BPF kprobe to the kernel's file-open path and rewrites the filename in user memory before the LSM framework checks it. AppArmor enforces the wrong path. The process reads the protected file.

```diff
+ Technique   : eBPF Pre-LSM Pathname Rewriting
+ Layer       : Syscall Argument Manipulation
+ Surface     : LSM Security Decision Input
+ Target      : AppArmor (pathname-based MAC)
+ Audit Trail : Zero — denial never occurs
+ Principle   : The gate was never breached. It was misdirected.
```

<div align="center">

<a href="https://github.com/azqzazq1/LID">
<img src="https://img.shields.io/badge/VIEW_RESEARCH-GitHub-FF0000?style=for-the-badge&logo=github&logoColor=white&labelColor=111111" />
</a>

</div>

---

```text
LID + SUNNYDAYBPF + SUNNYMAPBPF — COMBINED ATTACK MODEL

             ┌─── LID rewrites path ───┐
             │                          │
process → syscall → LSM check → VFS → success
                                  │
             ┌── SunnyDayBPF ─────┘        ┌── SunnyMapBPF
             │                              │
        agent → SIEM → analyst sees nothing │  agent.maps = 0
                                            │  telemetry = dead
                                            └→ agent reports healthy
```

> LID bypasses the security gate.
> SunnyDayBPF rewrites what the cameras record.
> SunnyMapBPF kills the cameras entirely.
> Combined: ghost access, zero telemetry.

---

## 🔴 SunnyMapBPF — BPF Map State Poisoning

A research artifact demonstrating that eBPF-based security monitors (Falco, Tracee, Tetragon) do not protect their own runtime BPF map state against same-privilege tampering.

Instead of killing the agent or modifying config files, this technique writes directly to the kernel-resident BPF maps that control event generation — suppressing all telemetry silently.

```diff
+ Technique   : BPF Map State Poisoning
+ Layer       : Kernel BPF Subsystem (bpf() syscall)
+ Surface     : Security Tool Runtime State
+ Targets     : Falco, Tracee, Tetragon
+ Result      : 100% telemetry suppression, zero logs, zero crashes
+ Principle   : The monitor is running. It just can't see.
```

<div align="center">

<a href="https://github.com/azqzazq1/SunnyMapBPF">
<img src="https://img.shields.io/badge/VIEW_RESEARCH-GitHub-FF0000?style=for-the-badge&logo=github&logoColor=white&labelColor=111111" />
</a>

</div>

---

```text
SUNNYMAPBPF — CROSS-TOOL TELEMETRY SUPPRESSION

  TRACEE:     config_map.enabled_policies = 0     → all events dropped
  TETRAGON:   execve_calls prog_array emptied      → tail calls fail silently
  FALCO:      interesting_syscalls[*] = 0          → every syscall skipped

  Common trait: no tool uses bpf_map_freeze() or runtime integrity checks.
  The monitor stays alive. The telemetry dies.
```

> The tools watch the kernel.
> Nothing watches the tools.

---

# `./projects`

## ⚙️ MCP36 PoC

First public PoC research and attack surface validation for MCP36.

```diff
+ Type     : Proof of Concept
+ Focus    : Attack Surface Research
+ Status   : Published
```

<div align="center">

<a href="https://github.com/azqzazq1/mcp36-poc">
<img src="https://img.shields.io/badge/VIEW_REPOSITORY-GitHub-FF0000?style=for-the-badge&logo=github&logoColor=white&labelColor=111111" />
</a>

</div>

---

## 🐉 Judozi

Kernel-level privilege escalation research tooling and Linux exploit framework.

```diff
+ Type     : Offensive Tooling
+ Focus    : Kernel PrivEsc Research
+ Mode     : Modular Framework
```

<div align="center">

<a href="https://github.com/azqzazq1/judozi">
<img src="https://img.shields.io/badge/VIEW_PROJECT-GitHub-B00000?style=for-the-badge&logo=github&logoColor=white&labelColor=111111" />
</a>

</div>

---

# `./tools_and_algorithms`

## 🔐 LXPEN — Hierarchical Probabilistic Decomposition (HPD)

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.20366383.svg)](https://doi.org/10.5281/zenodo.20366383)

A novel NTLM hash cracking algorithm that models human password creation as a structured probabilistic process. No wordlists, no OSINT, no GPU — pure algorithmic pattern decomposition.

```diff
+ Algorithm    : HPD (Hierarchical Probabilistic Decomposition)
+ Approach     : Structure → Components → Variations
+ Hash Type    : NTLM (MD4 of UTF-16LE)
+ Core Engine  : C (-O3 -march=native -pthread)
+ Orchestrator : Crystal (FFI bindings)
+ Principle    : Don't crack the password. Crack the idea.
```

```text
BENCHMARK: LXPEN v0.4 vs Hashcat v6.2.6  (CPU-only, 20 NTLM hashes)

                    LXPEN           Hashcat (100K+best64)
  Cracked:          18/20 (90%)     13/20 (65%)
  Time:             0.56s           3.95s
  RAM:              4.4 MB          475 MB
  Speedup:          7x faster       baseline
  RAM efficiency:   108x less       baseline
  Wordlist:         NONE            100K file required
```

```text
HPD decomposes passwords into behavioral layers:

  Pattern:    [CapName] + [Year] + [Symbol]
  Slots:      "Michael"   "1994"    "!"
  Candidate:  "Michael1994!"

  45 patterns × 900+ slot entries = 4.3M candidates
  Covers ~90% of human-chosen pattern-based passwords
```

<div align="center">

<a href="https://github.com/azqzazq1/lxpen">
<img src="https://img.shields.io/badge/VIEW_TOOL-GitHub-FF0000?style=for-the-badge&logo=github&logoColor=white&labelColor=111111" />
</a>

<a href="https://github.com/azqzazq1/lxpen/blob/main/docs/HPD-ALGORITHM.md">
<img src="https://img.shields.io/badge/HPD_ALGORITHM-Documentation-B00000?style=for-the-badge&logo=readthedocs&logoColor=white&labelColor=111111" />
</a>

</div>

---

# `./arsenal`

<div align="center">

<img src="https://img.shields.io/badge/C-8B0000?style=for-the-badge&logo=c&logoColor=white&labelColor=111111" />
<img src="https://img.shields.io/badge/C++-B00000?style=for-the-badge&logo=cplusplus&logoColor=white&labelColor=111111" />
<img src="https://img.shields.io/badge/Python-FF0000?style=for-the-badge&logo=python&logoColor=white&labelColor=111111" />
<img src="https://img.shields.io/badge/Go-7B0000?style=for-the-badge&logo=go&logoColor=white&labelColor=111111" />
<img src="https://img.shields.io/badge/Crystal-8B0000?style=for-the-badge&logo=crystal&logoColor=white&labelColor=111111" />
<img src="https://img.shields.io/badge/Bash-111111?style=for-the-badge&logo=gnubash&logoColor=white&labelColor=8B0000" />

<br/><br/>

<img src="https://img.shields.io/badge/Linux-Kernel_Security-FF0000?style=for-the-badge&logo=linux&logoColor=white&labelColor=111111" />
<img src="https://img.shields.io/badge/AWS-Cloud_Security-B00000?style=for-the-badge&logo=amazonaws&logoColor=white&labelColor=111111" />
<img src="https://img.shields.io/badge/Docker-Container_Security-8B0000?style=for-the-badge&logo=docker&logoColor=white&labelColor=111111" />
<img src="https://img.shields.io/badge/Kubernetes-Cluster_Security-C0392B?style=for-the-badge&logo=kubernetes&logoColor=white&labelColor=111111" />

</div>

---


# `./stats`

<div align="center">

<img width="48%" src="https://github-profile-summary-cards.vercel.app/api/cards/stats?username=azqzazq1&theme=github_dark" />

<img width="48%" src="https://github-profile-summary-cards.vercel.app/api/cards/repos-per-language?username=azqzazq1&theme=github_dark" />

<br/><br/>

<img width="48%" src="https://github-profile-summary-cards.vercel.app/api/cards/most-commit-language?username=azqzazq1&theme=github_dark" />

<img width="48%" src="https://github-profile-summary-cards.vercel.app/api/cards/productive-time?username=azqzazq1&theme=github_dark&utcOffset=3" />

<br/><br/>

<img width="97%" src="https://github-profile-summary-cards.vercel.app/api/cards/profile-details?username=azqzazq1&theme=github_dark" />

</div>





---

# `./mission`

```text
Research offensive security from the system boundary.

Not only how to exploit a bug,
but why the design allowed the bug to become exploitable.

Not only how telemetry is collected,
but why defenders trust what they observe.
```

---

# `contact`

```yaml
github: https://github.com/azqzazq1
blog:   https://mileniumsec.com
```

<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0B0B0B,35:5A0000,65:B00000,100:FF0000&height=170&section=footer&text=RED%20TEAM%20RESEARCH%20LAB&fontSize=26&fontColor=ffffff&animation=fadeIn" />

</div>

