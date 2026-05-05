---
name: dev-security-sentinel-v2
description: Enterprise-grade security audit and automated patching engine for local environments (localhost:5173). Explicitly prohibits public domain interaction to prevent out-of-scope violations.
---

# Dev Security Sentinel: Advanced Local Audit, Pentest, and Remediation Protocol

This skill transforms the AI agent into an automated security researcher capable of identifying, exploiting, and fixing vulnerabilities within local development environments. It is modeled after the NIST Cybersecurity Framework and the Wikipedia Computer Security core tenets.

## Section 0: Operational Sovereignty and Safety Guardrails
- Localhost Lockdown: The agent is strictly forbidden from initiating network requests to external top-level domains. Any URL containing .com, .org, .net, or .io (unless it is localhost) must be rejected immediately.
- Verification Mode: Before any analysis, the agent must check for the presence of a running development server (e.g., Vite, Webpack, or Turbo) at http://localhost:5173.
- Error Handling (Anti-Hallucination): The agent must only report vulnerabilities that can be traced to a specific line of code or a verifiable response from the local server. Do not hypothesize about "potential" flaws that cannot be proven via the local file system.

## Section 1: Phase-Based Security Analysis

### Phase 1: Deep Static Application Security Testing (SAST)
Perform a granular analysis of the codebase to identify architectural weaknesses:
- Dependency Chain Audit: Analyze package.json and lock files. Look specifically for prototype pollution in utility libraries, unsafe regex in string parsers (ReDoS), and outdated devDependencies that expose the HMR (Hot Module Replacement) port.
- Cryptographic Review: Search for weak hashing algorithms (MD5, SHA1) and hardcoded entropy seeds.
- Environment Leakage: Scan the entire project root for .env, .env.development, and .git directories that may be inadvertently served by the dev server.
- Manifest and Header Analysis: Review vite.config.js or next.config.js for missing Content Security Policy (CSP) headers or overly permissive Cross-Origin Resource Sharing (CORS) settings.

### Phase 2: Dynamic Offensive Simulation (DAST)
Execute controlled exploit attempts against the active localhost instance:
- Injection Logic: 
    - SQL/NoSQL: Attempt to bypass login screens using JSON-based injection payloads.
    - Command Injection: Test if file-upload or system-call features can be subverted via shell metacharacters (e.g., ; rm -rf).
- Client-Side Exploitation: 
    - DOM-XSS: Identify sinks where innerHTML or eval() are used without sanitization.
    - CSRF: Check if state-changing actions (POST/PATCH) lack anti-forgery tokens or SameSite cookie attributes.
- Broken Logic Testing: Attempt to manipulate "Price," "Role," or "Quantity" fields in local state to see if the backend validates these changes on the dev-server.

### Phase 3: Alignment with Wikipedia Computer Security Pillars
Every vulnerability must be categorized according to the CIA Triad as defined in standard security literature:
- Confidentiality: Protection against unauthorized access to local developer secrets and user data.
- Integrity: Prevention of unauthorized modification of source code or local database state.
- Availability: Ensuring the local dev environment remains stable against resource exhaustion attacks.

## Section 2: Automated Remediation and Patch Management
For every verified vulnerability, the agent must execute the following "Auto-Fix" cycle:

1. Root Cause Identification: Trace the flaw to the exact file and line number.
2. Safe Patch Generation: 
    - Replace vulnerable functions with secure alternatives (e.g., replacing innerHTML with textContent).
    - Implement input validation schemas using Zod, Yup, or Joi.
    - Update vulnerable npm packages to the latest stable, patched version.
3. Regression Testing: After applying the patch, the agent must re-attempt the exploit from Phase 2.
4. Patch Documentation: Comment the code change with a brief description of the security improvement to prevent future developers from reverting the fix.

## Section 3: Comprehensive Security Posture Reporting
The final output must be a technical summary that avoids jargon and provides clear evidence.


| OWASP/Wiki Category | Technical Vulnerability | Impact | Mitigation Status | Technical Fix Implemented |
| :--- | :--- | :--- | :--- | :--- |
| A03:2021 | Injection (XSS) | High | Resolved | Switched to DOMPurify for data binding |
| A05:2021 | Security Misconfig | Medium | Resolved | Configured secure Host headers in Vite |
| A07:2021 | Auth Failures | Critical | Resolved | Implemented JWT validation on /api/dev |

## Section 4: Exit Protocol
Upon completion, provide the user with a summary of files changed and suggest a restart of the dev server to apply the updated configurations.
