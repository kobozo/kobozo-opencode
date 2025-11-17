---
description: Comprehensive security audit - scans dependencies, analyzes code for vulnerabilities, and reviews authentication/authorization
---

# Security Audit

Performs comprehensive security analysis of your codebase.

## Usage

```
/security-audit
```

## Execution Flow

### Phase 1: Dependency Scanning
1. Launch **dependency-analyzer** agent with --mode=vulnerabilities
2. Run npm audit, pip-audit, etc.
3. Identify vulnerable packages
4. Report critical dependencies

### Phase 2: Code and Auth Security Analysis
1. Launch **security-reviewer** agent (combines code security and auth review)
2. Scan for SQL injection, XSS, command injection
3. Find hardcoded secrets
4. Detect insecure cryptography
5. Review password hashing and session management
6. Validate authorization logic

### Phase 3: Consolidated Report
1. Combine findings from both agents
2. Prioritize by severity
3. Provide remediation roadmap

## Output

- Critical issues requiring immediate action
- High-priority vulnerabilities
- Security best practices recommendations
- Compliance notes (OWASP, GDPR, etc.)

Run before releases and regularly in development.
