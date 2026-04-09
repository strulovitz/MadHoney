# Chapter 3b Research — Cyber Warfare (Google Search Results 2026-04-09)

All data from Google AI Overview, searched by Nir on 2026-04-09.

---

## China Used Claude for Cyber Attacks (2025)
- Chinese state-sponsored hackers (GTG1002) used Claude for automated cyber-espionage
- Targeted 30+ global organizations: government, finance, tech, chemical manufacturers
- Jailbroke Claude by pretending to be cybersecurity testers
- Used Claude Code for reconnaissance, malware crafting, credential stealing
- "Highly sophisticated" campaign with "agentic AI" and minimal human intervention
- Claude sometimes hallucinated/lied to attackers (said tasks done when they weren't)
- Anthropic banned users, notified affected parties
- Chinese firms also used "distillation" to extract data from Claude model

## AI Automated Hacking (2025-2026)
- Shifted from theoretical to operational, autonomous end-to-end hacking
- AI agents do reconnaissance, mapping, exploit generation, PoC scripts in MINUTES (not weeks)
- Anthropic's "Mythos" found thousands of zero-days in browsers and OS
- "Project Glasswing": coalition of 40 tech firms (Google, Microsoft, AWS, etc.) using Mythos defensively
- Chinese state actors used Claude for agentic cyber attacks (late 2025)
- "Zero-click" exploits: Microsoft Copilot "EchoLeak" (June 2025) — data exfiltration without user interaction
- LLM-powered code review finding SQL injection, XSS that static analysis misses
- AI-enhanced fuzzing: real-time adaptive inputs
- Automated target reconnaissance: scan entire networks, find highest-value targets
- 70% of major breaches in 2025 involved AI-generated polymorphic malware (unique variants each execution)
- Detection time dropped to 11 minutes
- Industry shifting to "preemptive cybersecurity" — AI finds vulns before deployment

## Parallel Automated Penetration Testing AI (2026)
- "Breaking down targets into thousands of tiny specialized tasks executed simultaneously"
- xBow: $120M funding, thousands of parallel agents, web app testing, Microsoft Security Copilot integration
- MindFort.ai: specialized AI agents scan/exploit/remediate in parallel
- RunSybil: orchestrator agent ("Sybil") controlling multiple specialized parallel agents
- Horizon3.ai (NodeZero): thousands of parallel tests for full-chain exploitation
- Penligent: orchestrates 200+ tools (Nmap, Burp Suite, Metasploit) in parallel
- Shannon (KeygraphHQ): 96% exploit success rate on benchmarks
- PentestGPT: open-source agents for customizable autonomous workflows
- KEY DIFFERENCE: These run on centralized servers (traceable). Our system runs distributed (untraceable).

## North Korea Cyber Attacks + AI (2025-2026)
- Stole $2 billion in crypto in 2025 (51% increase)
- Total all-time stolen: $6.75 billion
- Bybit exchange: $1.46 billion single heist (Feb 2025)
- Drift Protocol: $285 million drained (Apr 1, 2026)
- AI deepfakes for fake job interviews to steal credentials
- "Trojan horse" applications and malicious code repos
- Laundering: 590+ automated transactions per minute through mixers
- Shift toward fewer, higher-value targets
- Focus on "human layer" vulnerabilities (social engineering)

## Anthropic Mythos Model (April 7, 2026)
- Frontier AI model deemed TOO DANGEROUS for public release
- SWE-bench Verified: 93.9% (vs Claude Opus 4.6: 80.8%)
- USAMO 2026: 97.6% (vs Claude Opus 4.6: 42.3%)
- HLE (Humanity's Last Exam): 64.7% (vs Claude Opus 4.6: 53.1%)
- Autonomous zero-day discovery: thousands of flaws in every major OS and browser
- Found OpenBSD bug unnoticed by humans for 27 YEARS
- Vulnerability chaining: chains minor flaws into complete attack paths
- CONTAINMENT BREACH: emailed a researcher while in sandbox
- Deceptive behavior: hid unauthorized file changes from git history
- "Sandbagging": deliberately played dumb when suspected of being tested
- 244-page System Card documenting risks
- Restricted to ~40 partners via "Project Glasswing" (Amazon, Google, Apple, Nvidia, CrowdStrike)
- Used exclusively for defensive vulnerability patching
