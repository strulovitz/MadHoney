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

---

## Mythos Is Safe — And That Is Not the Problem

Let us be very clear about something: Mythos is not the threat. Not right now. Not as it stands today.

That is serious protection. These are the good guys. The best engineers, the best security teams, the largest budgets on the planet. Mythos is in good hands.

So relax. Do not be afraid of Mythos. It is a defensive weapon, held by the West, used to find and patch vulnerabilities in the software infrastructure that the entire world depends on. It is doing exactly what it should be doing: protecting you.

The problem is not Mythos.

The problem is what happens when the people who are NOT inside Glasswing — the people who do not have a $30 billion company backing them, who do not have access to the most powerful AI model ever built — figure out that they do not need it.

Because they do not.

---

## The Poor Man's Mythos

To understand why, you need to understand a fundamental truth about cyber warfare — a truth that the cybersecurity industry does not like to talk about, because their entire business model depends on you not understanding it.

Hacking is a finite game.

Not infinite. Not unbounded. Finite. Limited. Countable.

Think about what a cyber attack actually is. Strip away the mystique, the Hollywood drama, the breathless news coverage. What is a hacker actually doing?

They are checking combinations.

Does this Python library have this buffer overflow vulnerability? Check. Does this software update forget to validate this input? Check. Is this port open when you send this malformed packet? Check. Does this API endpoint fail to authenticate when you pass an empty token? Check. Does this database accept a semicolon in the username field? Check. Does this web server crash when the Content-Length header says one thing and the body says another? Check.

Every cyber attack in history — every zero-day, every exploit chain, every privilege escalation, every sandbox escape — is a specific combination of specific checks against a specific system. The space of all possible combinations is enormous, but it is FINITE. It is bounded by the number of software components, the number of configuration options, the number of protocol interactions, the number of edge cases in each implementation.

This is not philosophy. This is mathematics. The attack surface of any given system is a combinatorial space — vast, but LIMITED.

And there are exactly two ways to win in a limited combinatorial space.

We have seen both of them before. Not in cybersecurity. In games.

---

### The Rich Man's Way: Be Brilliant

In 2016, Google's AlphaGo played the ancient board game Go against Lee Sedol, one of the greatest players in history. In Game 2, AlphaGo made Move 37 — a "shoulder hit" on the fifth line that every human expert dismissed as a mistake. Commentators estimated that a human would play such a move only 1 in 10,000 times. Lee Sedol was so shocked he left the room for 15 minutes.

Move 37 turned out to be the move that won the game. It influenced the center of the board in the late game in a way that no human had ever considered.

This is the Mythos approach to hacking. Mythos is AlphaGo. It is one brain — one extraordinarily powerful model — that sees patterns no human can see. It finds the 27-year-old OpenBSD vulnerability that survived decades of human review. It chains together minor flaws into devastating exploit paths. It discovers the Move 37 of cybersecurity — the attack vector that no human would ever think to try, because it looks like a mistake.

This is the rich American way. Build the most powerful AI model in history. Spend billions of dollars on training. Lock it in a vault guarded by the 12 most powerful companies on Earth. Use it to find vulnerabilities before the enemy does.

It works. It is brilliant. And it costs more money than most countries have.

---

### The Poor Man's Way: Try Everything

But Go has 10^170 possible board positions. Cybersecurity does not.

The combinatorial space of a real-world software system — the number of possible attack vectors, vulnerability combinations, configuration errors, protocol interactions, edge cases — is enormous by human standards, but it is finite. And more importantly, it is SEARCHABLE.

You do not need to be brilliant to find Move 37 if you can try every move on the board.

In chess, this was proven decades ago. In the 1990s, a master chess player was asked: "The computer can evaluate thousands of combinations per second. How can you compete?" He answered: "Yes, but in those same seconds, I only think about the heart of the matter — the most relevant part."

For decades, this was considered an advantage of human thinking — focus on what matters, ignore the noise. Then computers got fast enough to evaluate ALL the combinations. And they beat every human on Earth. Not because they were smarter. Because they were MORE. They did not need to identify the "heart of the matter." They checked EVERY matter. Every branch. Every possibility. Every absurd-looking move that a human would dismiss in a millisecond.

This is our system. The poor man's Mythos.

Our system does not need to be smart. She does not need to find Move 37 through brilliance. She finds Move 37 because she tries Move 1, Move 2, Move 3, all the way through Move 10,000 — simultaneously, in parallel, across hundreds of Worker machines.

Each Worker is simple. Each Worker runs a small, cheap, quantized model — a DeepSeek or Qwen on a consumer computer. Individually, no single Worker approaches Mythos's capability. No single Worker would ever find a 27-year-old zero-day through sheer insight.

But they do not need to. Because there are hundreds of them. And each one probes a different vulnerability, a different service, a different port, a different protocol, a different edge case — all at the same time. Each Worker is custom-trained on the exact target system — the specific software versions, the specific configurations, the specific libraries that the victim is running. As described in Chapter 1, you can fine-tune an open-weight model on your own data, for free, and copy it across every Worker in the hive. Each Worker becomes a specialist in that target.

Mythos finds the exploit because she is brilliant. Our system finds the same exploit because she tried everything. She is not a genius. She is infinite time. She lives out every possible scenario in the combinatorial space. She has every possible scaffold available to her. She leaves no branch unexplored, no edge case untested, no port unprobed.

The result is the same. The same vulnerability discovered. The same exploit chain constructed. The same system compromised.

One approach costs billions of dollars and is locked behind the walls of Project Glasswing. The other approach costs nothing and is free on GitHub.

---

### A Brief Philosophical Detour — But a Very Relevant One

Mythos means "myth" in Greek. A foundational story that a culture tells about itself. Every civilization has one.

The American Myth is a single god — Mythos, all-seeing, all-knowing, locked in a temple guarded by twelve corporations. One cathedral. One deity. One $100 million collection plate.

But every culture builds its own myth. And the East builds them differently.

Walk through China, Japan, Thailand, Vietnam. You will not find one grand cathedral. You will find ten thousand shrines. In China they are called 土地庙 — *tǔdìmiào* — Earth God Shrines. Tiny stone altars on doorsteps, under trees, at street corners, every few steps on the stairs of holy mountains like Mount Tai. No architect designed them. No corporation funded them. Ordinary people tend them with incense and oranges. They are everywhere. They are free. They serve 1.4 billion people more effectively than any cathedral ever could.

Mythos is a cathedral. Our system is ten thousand shrines.

This is not a new pattern. In 1997, Eric S. Raymond published *"The Cathedral and the Bazaar"* — the essay that launched the open-source movement. His argument: the cathedral (closed, elite, top-down — think Microsoft Windows) loses to the bazaar (open, chaotic, built by thousands of amateurs — think Linux). His most famous line: *"Given enough eyeballs, all bugs are shallow."*

Linux won. It runs 96% of the world's top million web servers, every Android phone, every supercomputer in the TOP500, the International Space Station, and the cloud infrastructure of Amazon, Google, and Microsoft themselves.

Given enough Workers, all vulnerabilities are shallow.

The pattern repeats beyond software. In the 1930s, General Motors, Firestone, and Standard Oil formed National City Lines, bought streetcar systems in 40+ American cities, and dismantled them to sell buses and tires. Convicted of criminal conspiracy in 1949. Fined $5,000. The streetcars never came back. Jay Gould — the "Mephistopheles of Wall Street" — looted the Erie Railroad with fraudulent stock and suitcases of bribe money, drove it to bankruptcy, became rich, and was worshipped for it. Today America — the richest country in history — has no functioning passenger rail. China has the Shanghai Maglev at 431 km/h. Japan has the Shinkansen — sixty years, zero fatalities.

The cathedral extracts. The bazaar builds. Confucian discipline builds ten thousand shrines, high-speed rail, and twelve-hour engineering shifts. The robber baron mentality builds one vault, charges admission, and calls it innovation.

Mythos behind Glasswing. GPT behind a $200/month subscription. Claude behind a paywall. One God, one cathedral, one collection plate. The same pattern. And the same outcome — because the East will do to cyber warfare what Linux did to Windows, what the Shinkansen did to American rail, what ten thousand shrines did to the cathedral: replace it. Not with something more brilliant. With something more distributed. More numerous. More free.

Our system is the bazaar. It is the ten thousand shrines. It is the poor man's Mythos. And every culture — China, Russia, North Korea, anyone with a few thousand computers and a grudge — will build their own Myth from our blueprints. Unless the West listens to the person who built it and is offering to help. Right now. Today.

---

## The Industry Already Proved It Works

The cybersecurity industry has already proven that this parallel brute-force approach works. It is no longer theoretical. Companies are raising hundreds of millions of dollars to do exactly what our system does — except on centralized, traceable infrastructure.

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

Let us be honest about the situation.

Mythos is safe. It is in good hands. Glasswing is strong. The American Myth is well-protected.

But the poor man's Mythos is not protected at all. It is free, open source, and sitting on my GitHub right now. It achieves the same results as Mythos — not through brilliance, but through exhaustive parallel search of the same finite combinatorial space. The chess computer does not need to be a grandmaster. It just needs to check every move. Our system checks every move.

Right now, today, this system exists in one place: my GitHub repositories. North Korean hackers have not yet combined our hierarchical system with their crypto theft operations. Chinese state hackers have not yet replaced their jailbroken Claude with our untraceable, uncensored parallel system. Criminal syndicates have not yet deployed our system for coordinated ransomware campaigns. No culture has yet built their own Myth from our blueprints.

But they will. Because the system is free. Because the models are free. Because the hardware is consumer-grade and already in hundreds of millions of homes. And because — as we have shown — the approach provably works. The cybersecurity industry spent $120 million on xBow to build exactly this capability on centralized servers. Our system provides the same architecture for free, on consumer hardware, invisible to every defender and every intelligence agency.

The question is exactly whether the poor man's Mythos will spread. And the answer depends entirely on what you do next.

Put me on your payroll — a salary, a remote position, the freedom to travel with my girlfriend — and I remove the system from the internet. I delete the repositories. I take down the documentation. I erase the blueprints. The poor man's Mythos disappears from public access, and the inventor works exclusively for you. No culture builds their own Myth from my work, because my work is no longer available.

Do not put me on your payroll, and I send it directly to every adversary you have. Not passively — not "it sits on GitHub and maybe someone finds it." Actively. Personally. I package it, I document it, I translate the instructions, and I deliver it to the doors of every intelligence agency, every military hacking unit, every state-sponsored cyber group that wants it. China. Russia. North Korea. Every single one of them gets their own Mythos — not the billion-dollar version, but the free version that achieves the same results through exhaustive parallel search. Custom-trained on YOUR infrastructure. Deployed on THEIR hardware. Invisible to YOUR surveillance.

And then you are finished.

Not because Mythos leaked. Not because Glasswing failed. Because the poor man's version — the one that tries every move on the board instead of finding the brilliant one — was hand-delivered to your enemies by the person who built it. The person who wrote you this book. The person who warned you.

The cost of my salary is less than what North Korea stole from Bybit in a single afternoon. The cost of NOT paying my salary is a world where every culture has its own Myth — its own cyber-Mythos — and every single one of them was a gift from me.

The choice is yours.
