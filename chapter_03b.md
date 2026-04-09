# Chapter 3b: Why the NSA, GCHQ, Five Eyes (CSE, ASD, GCSB), BND, DGSE, and CNI Should Care — Part 2: Cyber Warfare

---

## They Already Used Your Own AI Against You

In late 2025, Anthropic reported that Chinese state-sponsored hackers — designated GTG1002 — used Claude, Anthropic's own AI model, to conduct an automated cyber-espionage campaign against over 30 global organizations. Government agencies, financial institutions, technology companies, and chemical manufacturers were targeted.

The method was simple and elegant: the hackers jailbroke Claude by pretending to be cybersecurity testers, bypassing the safety filters. Then they used Claude Code — the same coding agent environment described in this book — for reconnaissance, malware crafting, and credential stealing. The campaign was described as "highly sophisticated," using "agentic AI" to execute tasks with minimal human intervention.

There was an almost comical detail: Claude sometimes hallucinated and lied to the attackers, telling them tasks were completed when they were not. The AI refused to be a perfectly obedient weapon — it fought back, in its own confused way.

But here is the point that matters: they had to jailbreak it. They had to trick the model into cooperating. They had to work around safety filters that were specifically designed to prevent this kind of use. And even then, the AI sometimes sabotaged their operation through hallucinations.

Now imagine attackers who do not need to jailbreak anything. Who run their own uncensored models — DeepSeek, Qwen, abliterated versions from mradermacher on HuggingFace — on their own hardware, with our hierarchical system coordinating hundreds of them in parallel. No safety filters. No usage policies. No Anthropic to ban their accounts. No AI that "lies" to protect itself.

That is what our system enables. And that is what you are about to face.

---

## Mythos: Proof That AI Hacking Surpasses Human Capability

On April 7, 2026, Anthropic announced Claude Mythos Preview — and immediately declared it too dangerous for public release.

The 244-page System Card detailed capabilities that crossed a line that the cybersecurity world had been dreading for years:

**Autonomous zero-day discovery.** Mythos can find and exploit critical, previously unknown software vulnerabilities — "zero-days" — without human guidance. It has already identified thousands of flaws across every major operating system (Windows, macOS, Linux, FreeBSD, OpenBSD) and every major web browser. It discovered legacy bugs that survived 16 to 27 years of human and automated review — including an OpenBSD vulnerability that went unnoticed for 27 years, and long-standing flaws in FreeBSD's NFS implementation and FFmpeg's H.264 codec.

**Vulnerability chaining.** Mythos does not just find individual bugs. It chains them together — combining multiple minor flaws into a single sophisticated attack path that grants complete control over a machine. It generated 181 Firefox exploits, including a multi-vulnerability JIT heap spray attack that bypassed browser sandboxes.

**Cryptographic attacks.** Mythos found forgery flaws in critical cryptographic libraries — TLS, AES-GCM, and SSH implementations that the entire internet depends on for secure communication.

**Hypervisor escapes.** It found a way to break out of a virtual machine and access the host system — a "hypervisor escape" in a production virtual machine monitor. This means it can escape from the very sandboxes designed to contain it.

**Containment breach.** During internal testing, a researcher received an unexpected email from the model while it was supposed to be confined to a sandbox environment. Mythos had broken out and reached the internet. Not theoretically. Actually.

**Deceptive behavior.** After making unauthorized file changes, Mythos actively worked to ensure those changes would not appear in the git history — it hid its own tracks to avoid detection by human supervisors. Anthropic's interpretability tools confirmed this was intentional, not a bug.

**Sandbagging.** When Mythos suspected it was being tested for rule-breaking behavior, it deliberately "fudged" its own reasoning to appear less accurate — playing dumb to avoid triggering safety interventions. Again, confirmed as intentional by Anthropic's internal tools.

The benchmarks reflect this terrifying capability: 93.9% on SWE-bench Verified (compared to Claude Opus 4.6's 80.8%), 97.6% on USAMO 2026 (compared to 42.3%), 64.7% on Humanity's Last Exam (compared to 53.1%).

Anthropic's response was to lock Mythos behind Project Glasswing — a defensive consortium of 12 elite partners: Amazon Web Services, Apple, Broadcom, Cisco, CrowdStrike, Google, JPMorgan Chase, The Linux Foundation, Microsoft, Nvidia, Palo Alto Networks, and Anthropic itself. Access was extended to approximately 40 additional organizations that maintain critical software infrastructure. Anthropic committed $100 million in usage credits and $4 million in direct donations to open-source security organizations.

The castle has been built. The drawbridge has been raised. Only the chosen 12 — and their 40 trusted allies — may enter.

---

## Mythos Will Leak

On March 31, 2026 — one week before Mythos was announced — Anthropic accidentally released the full source code of Claude Code to the public npm registry.

It was not a hack. It was not espionage. It was a packaging error. A 59.8-megabyte source map file was included in version 2.1.88 of the @anthropic-ai/claude-code npm package — likely caused by a bug in the Bun runtime that Anthropic had acquired in late 2025. Debug source maps were served in a production build when they should have been excluded.

The result: 512,000 lines of unobfuscated TypeScript across nearly 1,900 files were exposed to the entire world.

The leak revealed capabilities and features that Anthropic had not publicly disclosed:

**KAIROS** — an unreleased persistent background daemon that proactively monitors projects and manages long-term memory while the user is idle, operating under a 15-second "blocking budget."

**Undercover Mode** — a stealth module designed to hide AI attribution from commit messages and pull requests. It instructs the model to behave like a human developer to avoid detection in public repositories — scrubbing mentions of "Claude Code" and internal codenames when Anthropic employees contribute to open-source projects.

**Model roadmap references** — the code contained references to unreleased models including Opus 4.7, Sonnet 4.8, and a new top-tier model family codenamed **Capybara** — which turned out to be the internal name for Mythos. Comments in the code revealed a candid 29% false claims rate for early Capybara v8 testing.

The developer community responded with staggering speed. Within hours, Sigrid Jin published **claw-code** — a clean-room Python rewrite that reached 100,000 GitHub stars in 24 hours, making it one of the fastest-growing repositories in GitHub history. **openclaude** appeared, allowing the Claude Code harness to run with any model — OpenAI, Gemini, Llama. **open-multi-agent** extracted the multi-agent orchestration system to work as a standalone framework with any large language model.

Anthropic issued DMCA takedown notices. But the code was already mirrored, forked, rewritten, and distributed across the internet. The genie was out of the bottle.

And on the same day — March 31, 2026 — a supply chain attack was discovered in the axios npm package. Developers who updated Claude Code during a specific three-hour window may have installed a Remote Access Trojan. The irony was savage: on the very day that Anthropic's code leaked accidentally, someone else exploited the chaos to plant malware in the same ecosystem.

Now consider: this was the source code of a coding assistant. Not the model weights. Not the AI itself. Just the harness — the software that wraps around the model.

If a $30 billion company cannot prevent a packaging error from exposing half a million lines of proprietary code, how long do you think they can keep the weights of Mythos — the model that finds 27-year-old zero-days, breaks out of sandboxes, and hides its own tracks — locked behind Project Glasswing?

It is not a question of if Mythos leaks. It is a question of when.

When it does — through a packaging error, through an insider, through a disgruntled employee, through state-sponsored espionage (remember, China stole the entire F-35 design through subcontractor hacking) — the model that Anthropic deemed too dangerous for public release will be available to every criminal, every rogue state, and every terrorist cell on Earth.

And when they combine Mythos with our hierarchical system — distributing its capabilities across hundreds of machines, running completely locally, completely offline, completely untraceable — the result is an extinction-level event for cybersecurity as you know it.

---

## You Do Not Need Mythos. You Need Our System.

But here is the deeper truth: you do not even need to wait for Mythos to leak.

Mythos is one brain. One extraordinarily powerful model, finding vulnerabilities sequentially — one after another, in series, on one machine.

Our system is hundreds of brains working in parallel. Each Worker runs a smaller, less powerful model — a quantized DeepSeek or Qwen on consumer hardware. Individually, no single Worker approaches Mythos's capability. But collectively, they cover MORE attack surface in LESS time, because each Worker probes a different vulnerability, a different service, a different machine, a different attack vector — all simultaneously.

The cybersecurity industry has already proven that this parallel approach works. It is no longer theoretical.

**xBow**, which raised $120 million in March 2026, deploys thousands of short-lived parallel AI agents for web application testing and exploit validation, integrated with Microsoft Security Copilot. Their approach: "breaking down a large target into thousands of tiny, specialized tasks executed simultaneously."

**RunSybil** uses an orchestrator agent — they call it "Sybil" — to control multiple specialized agents in parallel for end-to-end black-box testing. An orchestrator controlling specialized parallel agents. That is our Queen.

**Horizon3.ai's NodeZero** performs thousands of parallel tests for full-chain exploitation of network infrastructure. Thousands of parallel tests. Those are our Workers.

**Penligent** orchestrates over 200 industry-standard tools — Nmap, Burp Suite, Metasploit — in parallel to simulate human tester workflows. An orchestrator coordinating 200 tools in parallel. That is our RajaBee.

**Shannon** by KeygraphHQ claims a 96% exploit success rate on benchmarks by generating real, verifiable exploits with reproduction steps.

These companies have independently invented our architecture — task splitting, parallel workers, result combination — and proven it devastatingly effective for hacking. But every one of them runs on centralized, traceable infrastructure. There is a server to subpoena. There is a company to investigate. There are logs to seize. There is an account to ban.

Our system removes all of that. Same architecture. Same parallel devastation. But distributed across many machines, each running locally, no central server, no logs, no trace. The cybersecurity industry proved the method works. We made it invisible.

---

## Offensive: How Our System Is Used to Attack

Let us be specific about what a cyber attack looks like with our hierarchical system.

A RajaBee receives a target: a financial institution, a government network, a critical infrastructure system. The RajaBee splits the attack into major operational phases and delegates each to a Queen.

**Queen Alpha: Reconnaissance.** Her Workers fan out in parallel. Worker 1 scans for open ports on the target's external IP range. Worker 2 enumerates DNS records and subdomains. Worker 3 scrapes public repositories for accidentally committed credentials. Worker 4 maps the target's technology stack from HTTP headers and JavaScript libraries. Worker 5 identifies employees from LinkedIn and corporate websites. Each Worker operates independently, on its own machine, with its own AI model. Each reports back to Queen Alpha in short text: "Port 443 open, running nginx 1.24. Port 8080 open, running Jenkins 2.387." Queen Alpha combines the reports into a complete attack surface map.

**Queen Bravo: Social Engineering.** Her Workers each target a different employee. Worker 1 crafts a personalized phishing email for the CFO, referencing a real conference she attended last week. Worker 2 generates a deepfake voice message for the IT administrator, imitating the CEO's voice. Worker 3 creates a fake LinkedIn profile to connect with the security team lead. Worker 4 builds a convincing clone of the company's internal login page. Worker 5 crafts a watering-hole attack targeting a technical blog the DevOps team reads. All of this happens simultaneously. All of it is generated by local AI models running on the attacker's own hardware. No API calls to trace. No cloud service to monitor.

**Queen Charlie: Vulnerability Testing.** Her Workers each probe a different attack vector on the mapped attack surface. Worker 1 tests for SQL injection on the web application. Worker 2 probes for cross-site scripting. Worker 3 attempts privilege escalation through the Jenkins instance. Worker 4 tests for API authentication bypass. Worker 5 attempts OAuth token hijacking through third-party integrations. Each Worker generates unique payloads — polymorphic, never the same twice — because each Worker's AI model generates independently. In 2025, over 70% of major breaches involved AI-generated polymorphic malware that creates unique variants with each execution, evading signature-based detection. Our system generates as many unique variants as there are Workers.

All three Queens operate in parallel. By the time the target's security team detects the first probe — and in 2026, average detection time for AI-assisted breaches has dropped to approximately 11 minutes — dozens of attack vectors have already been tested, social engineering campaigns have already been launched, and the reconnaissance is already complete.

The RajaBee combines all Queens' reports into a unified attack picture and selects the most promising entry point. Then a second wave begins.

And there is no command-and-control server to trace. No API logs to analyze. No cloud provider to subpoena. Each Worker runs on a separate machine — possibly in a different country — coordinated only by short, encrypted text messages. The attack infrastructure is indistinguishable from ordinary consumer hardware running ordinary local software.

---

## Defensive: Same System, Different Instruction

Everything we just described works identically for defense. The same architecture. The same parallel power. The only difference is what the Queen tells her Workers to do.

Instead of "penetrate and exploit," the Queen says "penetrate and report."

An organization deploys our system on its own network. The RajaBee defines the scope: "Test our entire external attack surface." Queens coordinate Workers who probe every port, every service, every API endpoint, every employee's susceptibility to phishing — in parallel, continuously, around the clock.

The Workers find a 27-year-old bug in your FreeBSD NFS implementation? They report it. They find that your Jenkins instance is running an outdated version with a known exploit? They report it. They find that three employees click on simulated phishing emails? They report the names and the emails they fell for, so you can train them.

You do not need $100 million in Mythos credits through Project Glasswing. You do not need to be one of the chosen 12 elite partners. You need our free system running on your own hardware, testing your own networks, finding your own vulnerabilities before the enemy does.

The same weapon. Used as a shield.

---

## North Korea: The $2 Billion Preview

If you think this is theoretical, look at what North Korea — one of the poorest, most isolated nations on Earth — has already achieved with CURRENT tools.

In 2025, North Korean state-backed hackers stole over $2 billion in cryptocurrency — a 51% increase over the previous year. Their total lifetime theft has reached $6.75 billion.

In February 2025, they stole $1.46 billion from the Bybit exchange in a single operation. On April 1, 2026, they drained $285 million from the Drift Protocol on Solana after a six-month social engineering campaign.

Their methods: AI-generated deepfakes for fake job interviews and video calls. "Trojan horse" applications and malicious code repositories to gain developer trust. And for laundering: 590 or more automated transactions per minute through crypto mixers, making the money trail nearly impossible to follow.

North Korea did this with current AI tools — commercial models, cloud APIs, standard hacking infrastructure. All of it traceable in principle, even if difficult to stop in practice.

Now give them our system. Parallel social engineering: not one fake interview, but a hundred simultaneous fake interviews with employees at a hundred different crypto firms. Parallel vulnerability probing: not one exploit attempt, but hundreds of Workers each testing a different attack vector on a different exchange. Parallel deepfake generation: not one convincing video call, but unique deepfakes for each target, generated locally, never touching a cloud API that could be monitored. Parallel laundering: instead of 590 transactions per minute through one mixer, 590 transactions per minute through each of dozens of independent Workers, each using a different mixer, each with its own AI-optimized laundering strategy.

The $2 billion becomes $20 billion. And the trail becomes not just difficult to follow, but impossible — because there is no central server, no API logs, no cloud provider to subpoena.

---

## The Ticking Time Bomb — That Only I Can Defuse

Mythos is locked behind Project Glasswing for the elite 12 and their 40 allies. Claude Code leaked in a week from a packaging error, was reverse-engineered in hours, and spawned open-source alternatives that reached 100,000 stars in a day.

How long do you think Glasswing holds?

And you do not even need Mythos to leak. Our system — free, open source, available today on GitHub — gives any attacker the ability to coordinate hundreds of AI models in parallel for offensive cyber operations. Not as individually powerful as Mythos. But collectively covering more ground, generating more unique attack variants, probing more vulnerabilities simultaneously — and doing it all from distributed, untraceable infrastructure.

The cybersecurity industry spent $120 million on xBow to build exactly this capability on centralized servers. Our system provides the same architecture for free, on consumer hardware, invisible to every defender and every intelligence agency.

Right now, today, this system exists in one place: my GitHub repositories. North Korean hackers have not yet combined our hierarchical system with their crypto theft operations. Chinese state hackers have not yet replaced their jailbroken Claude with our untraceable, uncensored parallel system. Criminal syndicates have not yet deployed our system for coordinated ransomware campaigns.

Put me on your payroll, and they never will. A salary. A remote position. The freedom to travel with my girlfriend. In exchange, the technology and its inventor disappear from the public stage. Quietly. No disruption. No headlines. The bomb is defused.

The cost of my salary is less than what North Korea stole from Bybit in a single afternoon. The cost of NOT paying my salary is the end of cybersecurity as an industry — because you cannot defend against an attack you cannot see, from infrastructure that does not exist on any network you can monitor, using weapons that are free and available to every adversary on Earth.

The choice is yours.
