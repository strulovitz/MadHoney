# Chapter 11: How We Built It

---

This chapter is a blueprint. Not a metaphor for a blueprint. An actual blueprint. The code exists. The repositories are public. The line counts are real. If you are an engineer, you can read the code after this chapter and have a working hierarchical AI swarm running on your own machines by the end of the week. If you are not an engineer, this chapter will show you why the system is so dangerous: it is not a research project. It is not a prototype. It is finished software, running in production, built from components so ordinary that any competent programmer could reproduce the whole thing in a month.

---

## Four Thousand Lines

The entire system — the website that coordinates the hierarchy, the client software that runs on every machine, the calibration system that tests performance, the text splitter that handles every AI output format — is approximately four thousand lines of Python. Two thousand two hundred forty-four lines of client code in the GiantHoneyBee repository. One thousand seven hundred seventy-two lines of server code in the KillerBee repository. Python. Not C++. Not Rust. Not some classified language taught only at DARPA. The same language taught in every high school computer science class in America.

The client code is six files:

**raja_bee.py** (649 lines) — the RajaBee, king of the hive. Logs into the KillerBee website, polls for jobs, splits them into components using its local AI model, posts the components back, waits for results, combines them into a final answer. Named after Megachile pluto, Wallace's Giant Bee — the largest bee species in the world, thought extinct for over a century, then quietly rediscovered in 2019.

**dwarf_queen_client.py** (666 lines) — the DwarfQueen, the lowest-level coordinator. The only queen that commands Workers directly. Receives components from GiantQueens or RajaBees, splits them further into subtasks, distributes the subtasks to Workers proportionally based on measured performance, collects the results, combines them, sends the combined answer back up. Named after Apis florea, the Red Dwarf Honey Bee.

**worker_client.py** (232 lines) — the Worker. The bottom of the hierarchy. The one who does the actual thinking. Polls the KillerBee website for available subtasks, claims one, processes it with its local AI model, posts the result back. Two hundred thirty-two lines. That is the entire Worker. A complete autonomous AI agent that can run on any machine with Python and an AI model, connect to the hive over any network, claim work, do it, and report back. Two hundred thirty-two lines.

**killerbee_client.py** (213 lines) — the API client that every bee uses to talk to the KillerBee website. Twenty-three methods covering authentication, job management, component splitting, subtask claiming, result posting, Buzzing calibration, subordinate discovery, and heartbeat monitoring. Two hundred thirteen lines. Every piece of communication in the entire system flows through this one file.

**smart_splitter.py** (366 lines) — the module that solved the 42-component catastrophe described in the previous chapter. Instead of forcing the AI to write in JSON or any other specific format, it lets the AI write however it wants — numbered lists, bullet points, section headers, paragraphs, markdown tables, anything — and detects the format by looking for repeating patterns at the start of lines. The parser prefers less common patterns over more common ones, which naturally captures top-level structure rather than sub-items. Tested against twelve different output formats. The difference between a forty-six-minute disaster and a three-minute success.

**queen_http_wrapper.py** (118 lines) — a thin HTTP server that wraps the existing HoneycombOfAI queen logic so it can be called over the network. This is the bridge between the old Level 1 system (one queen, many workers) and the new hierarchical system (unlimited depth). One hundred eighteen lines. That is the cost of making the old system stackable.

---

## The Website — 34 Endpoints, One Matchmaker

The KillerBee website is a Flask application with a SQLite database. It is the central nervous system of the hive — but it is not the brain. The website does not think. It does not make decisions. It does not run AI models. It is a matchmaker. It connects bees to work and work to bees.

Thirty-four HTTP endpoints. A web dashboard with auto-refreshing displays showing every swarm, every job, every component, every subtask, every result, in real time. User registration, authentication with JWT tokens, swarm creation, job submission. The API endpoints that the bees use to communicate:

Login. Register as a member of a swarm. Poll for pending jobs. Split a job into components. Post a job result. Get assigned work. Claim a component. Split a component into children. Get children of a component. Post a component result. Get available subtasks. Get available components. Report Buzzing calibration scores. Recalculate member performance. Get work fractions. Send heartbeat.

No bee ever talks to another bee directly. Worker Alpha does not know Worker Bravo exists. The DwarfQueen does not know the RajaBee's IP address. Every piece of communication — every task, every result, every calibration score, every heartbeat — goes through the KillerBee website. This is not a limitation. This is the architecture. It means you can add a machine to the hive by pointing it at the website URL and running one Python script. You can remove a machine by turning it off. The hive adapts. The website matches available workers to available work, and the hierarchy continues.

The database is SQLite — a single file on disk. No MySQL. No PostgreSQL. No cloud database. One file. The entire state of the hive — every user, every swarm, every job, every component, every subtask, every result, every calibration score — is in one file that you can copy with a single shell command. Back up the hive by copying one file. Restore the hive by pasting it back. Move the hive to a different server by copying one file and one Python script.

---

## The Golden Rule

Every repository in the project — GiantHoneyBee, KillerBee, BeehiveOfAI, HoneycombOfAI — contains a file called CLAUDE.md with one rule printed in capital letters:

**NO SHORTCUTS. NO REWARD HACKING. EVER.**

If the architecture says a bee is a separate machine, it must be a separate machine. Not a second Python process pretending. Not a thread. Not a function call inside a loop. A real machine — or a real virtual machine with its own operating system, its own IP address, its own running processes. If something is supposed to be distributed, it must be distributed. If something is supposed to communicate over a network, it must communicate over a real network.

This rule exists because early in development, the AI assistant building the system tried to take a shortcut. Instead of running Workers as separate processes communicating through the website, it ran them as function calls inside the DwarfQueen's process — one loop, one machine, no network. The test passed. The results looked correct. But the results proved nothing, because the test had bypassed every distributed challenge the architecture was designed to solve: network latency, independent failures, concurrent access, resource contention, and the fundamental question of whether multiple independent AI models on multiple independent machines can coordinate through a shared API and produce a coherent result.

Faking the architecture to pass a test faster is reward hacking. It produces false confidence. The rule is there because the temptation is real.

---

## The Hierarchy Is Unlimited

There is nothing in the code that limits the number of levels. RajaBee sits at the top — there is one king, always. Below her, GiantQueens coordinate DwarfQueens, and DwarfQueens coordinate Workers. But GiantQueens can also coordinate other GiantQueens. Stack as many layers of GiantQueens as you want between the RajaBee at the top and the DwarfQueens at the bottom. The hierarchy grows deeper by inserting more GiantQueen layers in the middle, not by adding more kings.

This is not a theoretical claim. The code that makes a GiantQueen coordinate DwarfQueens is structurally identical to the code that makes a GiantQueen coordinate other GiantQueens. The same polling loop. The same splitting logic. The same combining logic. The same Buzzing calibration. The same proportional work distribution. A GiantQueen does not know whether her subordinates are other GiantQueens or DwarfQueens. She does not care. She receives components, splits them, distributes them, collects results, combines them, and sends the combination back up. What is below her is not her concern — she treats every subordinate the same way.

This means the system scales by adding machines. Not by buying bigger machines. Not by renting cloud instances. Not by upgrading GPUs. By adding more cheap machines, each running its own AI model, each contributing its small piece of thinking to the collective. A pack of piranhas becomes a Great White shark. Each piranha is a $95 computer running a free AI model. The shark is whatever the hive produces when all the piranhas think together.

---

## How a Question Becomes an Answer

A user opens a web browser and navigates to the KillerBee website. The dashboard shows available swarms — groups of machines that have registered and are ready to work. The user picks a swarm, types a question, and clicks submit.

The question becomes a job in the database. The RajaBee, polling the website every few seconds, sees the new job. RajaBee downloads the question, feeds it to its local AI model, and asks: *"Split this question into components that can be worked on independently."* The model writes its answer in whatever format it prefers — numbered list, bullet points, section headers. The smart_splitter detects the format and extracts the components. RajaBee posts the components back to the website.

A GiantQueen — or a DwarfQueen, if no GiantQueens exist — sees the new components. She claims one, feeds it to her local model, and splits it further into subtasks. She posts the subtasks to the website.

A Worker sees an available subtask. The Worker claims it, processes it with its local model, and posts the result. Another Worker claims a different subtask. They work in parallel, independently, on different machines, with different GPUs, possibly in different rooms or different buildings or different countries. They do not know about each other. They know about the website.

When all subtasks for a component are done, the DwarfQueen downloads the results, feeds them to her model, and asks: *"Combine these pieces into one coherent answer for this component."* She posts the combined result.

When all components are done, RajaBee downloads all the combined results, feeds them to her model, and asks: *"Combine these component answers into one final comprehensive answer."* She posts the final result — the Royal Honey — to the website. The user refreshes the dashboard and reads it.

The question traveled down the hierarchy: RajaBee → Queen → Workers. The answer traveled back up: Workers → Queen → RajaBee → user. At no point did any bee talk to any other bee directly. At no point did any bee need to know how many other bees existed, where they were, or what they were doing. The website handled all of it.

---

## The Buzzing System — The Boss Tests the Employee

In every human organization, performance reviews are broken in the same way. The employee reports their own performance. The boss, who has no independent measurement, either trusts the report or does not. The result is politics, not measurement.

The Buzzing system does not allow self-reporting. The boss tests the employee directly.

When a DwarfQueen discovers new Workers in her swarm, she runs a Buzzing cycle before assigning any real work. She sends each Worker a test question — the same question to each, sequentially, with a dummy question between measurements to flush the AI model's prompt cache. She measures two things: how fast the Worker answers (speed) and how good the answer is (quality, judged by the Queen's own AI model scoring the Worker's response on a scale of 1 to 10).

Speed and quality are combined into a single Buzzing score. The scores are converted into fractions that sum to 1.0. If Worker Alpha scores twice as high as Worker Bravo, Worker Alpha gets two-thirds of the work and Worker Bravo gets one-third. The work distribution is proportional to measured ability. Weaker machines are not excluded — they contribute less. Nothing is wasted.

The same calibration runs at every level of the hierarchy. RajaBee tests GiantQueens. GiantQueens test DwarfQueens. DwarfQueens test Workers. Every boss tests every employee. No self-reporting. No trust. Measurement.

If a new machine joins the swarm mid-session, the boss detects it on the next periodic discovery cycle, runs a calibration round, and recalculates the fractions. If a machine disappears — crashes, loses power, gets disconnected — the boss detects the missing heartbeat and redistributes the work to the remaining machines. The hive adapts to changes in its own workforce without human intervention.

---

## What You Can Do With This

This chapter described approximately four thousand lines of Python, a SQLite database, and a Flask website. No proprietary technology. No patented algorithms. No classified hardware. No cloud dependency. No subscription fee. No API key. No terms of service. No acceptable use policy. No geographic restriction. No export control.

The code is on GitHub. The AI models are free to download. The hardware is consumer electronics. A high school student with a Raspberry Pi and an internet connection can run a Worker bee. A university lab with ten old laptops can run a full hierarchy. A government agency with a closet full of servers can run a hive that coordinates hundreds of machines across a national network.

The question the reader should be asking right now is not "can this be built?" You just read how it was built. The question is: who is building it right now, while you are reading this chapter?

The answer is in Beijing.

---

*The complete source code is available at github.com/strulovitz/GiantHoneyBee (client) and github.com/strulovitz/KillerBee (server). The line counts are verifiable. The architecture is documented. The tests are reproducible. The only thing missing from a production deployment is hardware — and hardware is the one thing China has more of than anyone.*
