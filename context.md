# 🔐 Vulnerability Assessment Tool – Project Summary (Rust-Based)

## 🧠 Project Objective

The goal is to develop a custom vulnerability assessment application that scans modern software applications for security weaknesses — from common vulnerabilities (e.g., SQLi, XSS) to misconfigurations, insecure headers, and outdated dependencies. This tool will be used for testing and hardening applications, ensuring stronger security posture before deployment.

---

## ⚙️ Technology Stack

##### ✅ Primary Language

**Rust**: Chosen for its **memory safety** guarantees, **high performance**, and **modern tooling**, making it ideal for building reliable, **low-level**, and concurrent **security tools**.

---

## 🧱 Core Libraries & Crates

|Purpose|Crate / Tool|
|---|---|
|HTTP Requests|`reqwest`, `hyper`, `surf`|
|Async Concurrency|`tokio`, `rayon`|
|HTML/DOM Parsing|`scraper`, `select`|
|CLI Interface|`clap`, `dialoguer`|
|Logging|`log`, `env_logger`, `tracing`|
|Templating / Reports|`tera`|
|Serialization|`serde`, `serde_json`, `serde_yaml`|
|Network Scanning|`std::net`, custom TCP/UDP using `tokio`, or Nmap API integration|
|Database (optional)|`rusqlite`, `sqlx`, `diesel`|

---

## 🔍 Target Capabilities

The application aims to support multiple vulnerability detection modules, including:

|Module|Functionality|
|---|---|
|✅ HTTP Security Checker|Analyze HTTP headers, TLS, redirects, and cookies|
|✅ Port Scanner|Detect open ports and services using raw sockets or Nmap|
|✅ Directory Bruteforcing|Scan common endpoints and directories|
|✅ Injection Testing|Detect SQLi/XSS with payload injections and response analysis|
|✅ API Testing|Fuzz REST endpoints with varied/mutated data|
|✅ Dependency Check|Parse manifests (e.g., Cargo.toml, package.json) for CVEs|
|✅ Report Generation|Produce readable reports in HTML/Markdown (PDF optional)|

 --- 

## 📦 Integration Possibilities

Although Rust will be the core, integration with external tools is planned:

|External Tool|Integration Method|
|---|---|
|**Nmap**|Via XML output parsing or subprocess|
|**OWASP ZAP**|REST API calls via `reqwest`|
|**sqlmap**|Command-line interface parsing|
|**OpenVAS**|Optional REST API integration|

---

## 🛡️ Why Rust?

- **Memory-safe by design**: Prevents common security flaws at compile time.

- **Blazing-fast**: Suitable for heavy scanning or parallel requests.

- **Reliable: Errors handled explicitly**; no silent failures.

- **Modern developer experience**: Cargo, documentation, and tooling are top-notch.

---

## 🧾 1. Project Overview

- **Name**: DYSAI-VCT stands for Dynamic Systems with Artificial Intelligence - Vulnerability Check Tool

- **Goal**: Build a desktop MVP vulnerability scanner with a GUI

- **Platform**: Rust + Tauri + React

- **Scope**: Local scanning, with modules for basic vulnerability tests

---

## 🔍 2. MVP Feature Scope

|Feature|Description|
|---|---|
|✅ CLI or GUI launcher|Launch the desktop app|
|✅ URL Input & Scan|User enters a URL or IP to scan|
|✅ HTTP Header Analysis|Check for missing/insecure headers|
|✅ Port Scanner (basic)|Check for open TCP ports|
|✅ Directory Brute Force|Scan common directories using wordlist|
|✅ Report Preview/Export|Generate local report in HTML or Markdown|
|⬜ Integration/APIs|**Out of scope** for MVP; future hybrid version|
  
---

## 🧠 3. Architecture Overview

Break down by modules/components:

```
[ GUI (Tauri Frontend) ]
         |
         v
[ App Controller (Rust) ] <--> [Scanner Engine (Rust Lib)]
         |                           |
         v                           v
[ Report Generator ]         [HTTP, Port, Dir modules]
         |
         v
[ Filesystem Output ]
```


---

## 🧱 4. Module Design (Skeleton)

**Scanner Engine (Rust)**:
- `mod http_headers`
- `mod port_scanner`
- `mod dir_bruteforce`
- `mod utils`
- **Shared models**: `ScanResult, ScanTarget`, etc.

**Tauri Backend**:
- Exposes commands like:
	- `start_scan()`
	- `get_result()`
	- `export_report()`

**Frontend (React):**
**UI Components: Input form, results table, report view**
**Tauri IPC calls to Rust backend**

---

## 📈 5. Flow Diagram (Scan Flow)

**Example in words** (For the moment):

User launches app
Enters target URL
Clicks "Start Scan"
App passes target to Rust backend via Tauri command
Rust runs selected scan modules
Backend returns structured result
Frontend shows live progress (optional)
User views result and can export report



---

## 📄 6. Technologies & Crates

| Layer     | Tools                                                    |
| --------- | -------------------------------------------------------- |
| Backend   | Rust, Tauri, `reqwest`, `tokio`, `serde`, `clap`, `tera` |
| Frontend  | React or SvelteKit, TailwindCSS, Tauri bindings          |
| Reporting | Markdown or Tera-based HTML templates                    |
| File I/O  | Native Rust filesystem access (`std::fs`)                |

---

## 🧪 7. Development Milestones

|Milestone|Outcome|
|---|---|
|✅ Project scaffold|Rust + Tauri running with Hello World|
|✅ Implement HTTP header scan|Basic GET + header analysis|
|✅ Add port scan module|Scan top 1000 ports using TCP|
|✅ Add directory brute force|Wordlist + concurrent GETs|
|✅ GUI integration|Buttons and result display|
|✅ Report generation|Export HTML/Markdown|
|⬜ Optional UX polish|Loading states, icons, etc|

---
## 🔐 8. Security Considerations

- Limit risky system access
- Validate target input
- Warn before scanning private networks
- Respect user privacy (no telemetry unless opted-in)

---

## 📁 9. Folder Structure (Proposed)

```
dysai-vct/
├── src-tauri/             # Rust backend
│   ├── main.rs
│   ├── tauri.conf.json
│   ├── commands.rs
│   ├── scanner/
│   │   ├── http.rs
│   │   ├── ports.rs
│   │   └── dirs.rs
│   └── report/
│       └── generator.rs
├── src/                   # React frontend
│   ├── App.tsx
│   ├── main.tsx
│   └── ...
├── README.md
└── docs/
    └── architecture.md

```


## 🧠 10. Use Cases / Scenarios

**Use Case 1:** A developer wants to check their internal test server for security headers and open ports before deployment.

**Use Case 2:** A pen-tester wants to brute-force hidden directories in a staging environment and generate a report.

## 🔐 11. Threat Model

|Threat|Mitigation|
|---|---|
|User inputs malicious targets|Sanitize and validate input|
|Scanner accesses sensitive files|Restrict scan scope|
|Output files overwrite system files|Set strict output paths|
|Network misuse|Warn users; disable by default in some cases|

## 🧪 12. Testing Strategy

- Unit tests in Rust for scanners
- Mock HTTP servers (for headers/404s)
- Integration tests via Tauri commands
- Manual tests for the frontend

## 🗺️ 13. Future Hybrid Mode Plan

In the future, DYSAI-VCT will include an optional server module to enable remote scan submissions, scan scheduling, and dashboard-based report viewing.

**API server** for features like:

- Submitting scan reports
- Syncing settings
- Collaborating with teams
- Scheduling scans

This hybrid model keeps the **core scanning secure and local**, while enabling **remote insights and integrations**.


