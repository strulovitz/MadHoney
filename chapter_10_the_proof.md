# Chapter 10: The Proof — We Ran It

---

This chapter is evidence. Not theory. Not projection. Not "imagine what would happen if." Every number in this chapter was measured on real hardware, on real software, over a real network, with real timestamps. The source data is committed to GitHub with commit hashes anyone can verify. If you do not believe a number, pull the repository and read the logs yourself.

Previous chapters told you what hierarchical AI swarms can do to your business, your military advantage, your surveillance apparatus, your patent moat, your supply chain, your quarterly earnings. This chapter tells you that it already works.

---

## Three Experiments, Two Machines, Five Bugs, One Insect

On April 10-11, 2026, we ran three experiments. The first was on one machine. The second and third were across two physical machines connected by nothing more than a home LAN cable and a $30 router. The AI models running on both machines were llama3.2:3b — a 3-billion-parameter model that fits in 2.5 gigabytes of disk space, runs on any consumer laptop manufactured after 2020, and is free to download from the internet. Three billion parameters is tiny. It is the runt of the AI litter. GPT-4 has over a trillion. Claude has hundreds of billions. We chose the runt on purpose, because the point of these experiments is not "look how smart the answer is." The point is: the architecture works, and if it works with the runt, imagine what happens when the runts are replaced by real models.

---

## Experiment 1 — Localhost, April 10, 2026

Four separate processes on one laptop. A RajaBee, a DwarfQueen, and two Workers. Each process runs its own copy of the AI model. Each process communicates only through the KillerBee website — a Flask application with a SQLite database, running on port 8877. No process talks to any other process directly. Every task, every subtask, every result, every status update flows through the website's REST API, the same way a real distributed deployment would flow through a real server.

Before the real work begins, the hierarchy calibrates itself. The DwarfQueen — the only queen who commands Workers directly — tests both Workers by sending them identical questions and measuring how fast and how well each one answers. This is the Buzzing system. The name comes from real beekeeping: a beekeeper evaluates a hive's health by listening to the pitch and intensity of its collective buzz. Our DwarfQueen evaluates her Workers the same way — not by asking them to self-report, but by testing them herself, timing the responses, judging the quality, and computing a performance score she did not have to trust anyone else to provide.

The calibration produced fractions: Worker Alpha got 0.882, Worker Bravo got 0.118. This means Worker Alpha was significantly better on this run — it would receive 88% of the subtasks, and Worker Bravo would receive 12%. The work is split proportionally to measured ability. No egalitarianism. No guessing. No "give everyone equal work and hope for the best." The boss measured the employees, and the boss distributes the work accordingly.

The test question: *"What place in the Solar System from the following three is the best for humans to try space colonization? Please give pros and cons for each: Titan (Saturn's Moon), Europa and Ganymede (Jupiter's Moons), Ceres and the Asteroid Belt."*

RajaBee received this question. RajaBee split it into three components — one per celestial body. The DwarfQueen received each component, split it into subtasks for the Workers, distributed the subtasks proportionally, collected the results, combined them, and sent the combined answer back to RajaBee. RajaBee combined all three component answers into a single final document — the Royal Honey.

Total time: 166.2 seconds. Total components: 14 (3 from RajaBee, 11 subtasks from DwarfQueen). The final answer was a structured comparison of all three destinations with pros, cons, and a recommendation. Context was preserved through every level — the Workers knew they were answering a question about space colonization, not about some disconnected fragment.

Four of the fourteen subtasks were garbage. The 3-billion-parameter model is small enough that it sometimes leaks prompt fragments instead of generating real content — outputting "Here are the two subtasks:" as its answer instead of actually doing the work. This is a model quality issue, not an architecture issue. Replace the 3B model with an 8B or a 14B and the garbage disappears. We kept the 3B runt because the point is the plumbing, not the water quality.

---

## The Buzzing Calibration — Five Bugs, Five Fixes

Between the first and second experiments, we ran the Buzzing calibration system across two physical machines for the first time. This is where things got educational.

**Bug 1: The Workers trampled each other.** Both Workers were being calibrated simultaneously, and both were hitting the same Ollama instance on the same GPU. They competed for compute, and their response times were polluted by each other's load. Fix: run calibration sequentially — one Worker at a time, full GPU attention.

**Bug 2: The math was wrong.** The speed scoring formula was supposed to produce a proportional score — a Worker twice as fast should get twice the work. The original formula did not preserve ratios. A Worker that was 10% faster ended up with 90% of the work. Fix: proportional formula — `10 × (fastest_time / this_worker's_time)`. Now a Worker twice as fast gets a score twice as high, and the resulting work fractions are fair.

**Bug 3: The second Worker always looked faster.** Every time, regardless of which Worker went second, the second one was 2-3x faster than the first. Identical hardware, identical model, identical question — but the second measurement was always faster. We spent hours on this. GPU warmup? No. Memory caching? Partially. The real cause: Ollama caches the prompt evaluation from the first request. When the second Worker sends the same prompt prefix, Ollama skips the evaluation and goes straight to generation. The second Worker appears faster because the infrastructure is doing less work for it, not because the Worker is better. Fix: send a dummy question between measurements to flush the prompt cache. Calibration now measures real generation speed, not cache hits.

**Bug 4: The Worker Bee Incident.**

This is the funniest bug in the history of this project, and possibly in the history of artificial intelligence.

After fixing the first three bugs, the calibration scores were close — but not equal. Worker Alpha consistently got higher quality scores than Worker Bravo, even though they were running on the same hardware with the same model. We investigated everything: cache contamination, GPU thermal throttling, Ollama version differences, memory allocation patterns. Hours of work.

Then we looked at the actual answers.

Worker Alpha, asked about ancient Pompeii, gave a reasonable if mediocre overview of Roman city planning and volcanic eruption effects.

Worker Bravo, asked the same question, began its answer: *"As a worker bee, I must admit that my expertise lies in apiculture and pollination. However, I can try to provide an outsider's perspective on ancient Pompeii..."*

The prompt said "You are a worker bee." The 3-billion-parameter model took this literally. It role-played as an insect. It apologized that bees do not know much about Roman history. It explained that its expertise is in nectar and pollen collection. Then it gamely tried to answer anyway, producing a response that was simultaneously charming and useless.

The quality judge — another AI model — correctly gave it a lower score. The debugging was valid. The cache investigation was valid. The GPU analysis was valid. And the answer was one line in the prompt making the AI pretend to be a bug.

Fix: remove all roleplay from all prompts, across the entire codebase. Do not tell the AI what it is. Do not tell it to be thorough. Do not tell it to be concise. Do not motivate it. Just ask the question and let it answer. This turned out to be a general principle that improved every interaction in the system: the less you tell the model about itself, the better it performs.

**Bug 5: The measuring stick was bigger than the thing being measured.** The polling interval — how often the DwarfQueen checks whether a Worker has finished — was 5 seconds. Some Workers finished in 3 seconds. The measured time was dominated by polling delay, not by actual work. A Worker that finished in 2 seconds and a Worker that finished in 4 seconds both showed up as "5 seconds" because the poll caught both of them on the same tick. Fix: 1-second polling, 3 big questions per measurement round, scores averaged across all rounds. The signal finally emerged from the noise.

After all five fixes, calibration on identical hardware produced fractions of 0.523 versus 0.477 — nearly perfect 50/50, which is exactly what identical hardware should produce. The Buzzing system was fair.

---

## Experiment 2 — First Cross-Machine LAN Test, April 11, 2026

This was the test that mattered. Two physical machines. A Lenovo Legion laptop with an RTX 5090 GPU in the bedroom. A Lenovo Legion desktop with an RTX 4070 Ti GPU in the living room. Connected by a LAN cable through a home router. No cloud. No data center. No corporate network. A bedroom and a living room.

The laptop ran the KillerBee website and RajaBee. The desktop ran one DwarfQueen and two Workers. Every piece of communication — every task, every subtask, every result — traveled over the LAN through the KillerBee website's REST API.

The test question: *"What solutions and concepts can humans use to do interstellar travel to Alpha Centauri? Please give pros and cons for each."*

The result was a catastrophe and a triumph at the same time.

RajaBee split the question into 42 components. Forty-two. The expected number was 3 to 5. What happened: the 3B model returned a nested JSON structure where each field — "description", "pros", "cons" — became a separate component. The JSON parser treated each field as its own piece of work. Forty-two components cascaded into 406 subtasks distributed to the Workers. The system churned for 46 minutes, producing a mountain of redundant work.

And it completed successfully. Every single one of the 448 work items was processed, combined, and delivered. The final answer — the Royal Honey — was a comprehensive document covering wormholes, Alcubierre warp drives, light sails, nuclear pulse propulsion, fusion drives, antimatter propulsion, radiation shielding, hibernation, closed-loop life support, gravitational slingshots, quantum communication, and more. Each with pros and cons. Coherent despite the chaos.

The architecture did not care that the splitting was wrong. It processed what it was given. It combined what came back. It did not crash, did not hang, did not lose data, did not corrupt the hierarchy. Two different GPUs on two different machines, coordinated through a Flask app and a SQLite database, absorbed a 42× overload and still delivered a coherent result.

The failure was the splitting logic. The success was everything else.

---

## Experiment 3 — The Fix, April 11, 2026

We replaced the JSON-based splitter with a new module called smart_splitter. The design philosophy: do not force the AI to write in a specific format. Let it write however it wants — numbered lists, bullet points, section headers, paragraphs, any format — and parse whatever comes back by detecting the repeating pattern at the start of each line. The parser prefers less common patterns (section headers) over more common ones (sub-item bullets), which naturally captures the top-level structure rather than the sub-items.

We tested the parser against twelve different output formats before running the real experiment. It handled all twelve correctly.

Same setup. Same machines. Same question. Same models.

The result:

|  | Experiment 2 (broken splitting) | Experiment 3 (smart_splitter) |
|---|---|---|
| Components from RajaBee | 42 | 5 |
| Total subtasks | 406 | 15 |
| Total time | 2,780 seconds (46 minutes) | 180 seconds (3 minutes) |

Fifteen times faster. Not because of better hardware. Not because of a better AI model. Not because of a better network. Because of one module that lets the AI write naturally instead of forcing it into a format it handles poorly.

RajaBee split the question into five parts: propulsion concepts, travel methods, challenges, Alpha Centauri specifics, and an introduction. The DwarfQueen split each part into 2-3 subtasks for the Workers. The Workers processed them in 2-4 seconds each. Everything combined back up into a final answer that was comprehensive, structured, and correct.

Three minutes. Two machines. A bedroom and a living room. A question about interstellar travel answered by a hierarchy of cheap AI models coordinating through a website, over a home network, with no cloud, no data center, no satellite, no centralized infrastructure of any kind.

---

## What This Proves

The people reading this book — the executives, the generals, the directors, the board members — are not interested in whether a 3-billion-parameter model can write a good essay about Alpha Centauri. They have ChatGPT for that. What they should be interested in is what the three experiments prove about the architecture:

**The hierarchy is real.** RajaBee splits. DwarfQueens split further. Workers process. Results combine back up. Every level works. Every handoff works. The plumbing is proven.

**It works across machines.** Not simulated machines. Not Docker containers pretending to be separate. Two physical computers in two rooms connected by a cable. The architecture does not care where the machines are. It cares that they can reach the website.

**The boss tests the employees.** The Buzzing calibration system means no one self-reports their performance. The boss sends test questions, measures speed and quality, and distributes work accordingly. Proportional allocation means weaker machines still contribute — they just get less work. Nothing is wasted.

**The system survives its own bugs.** Experiment 2 ran with broken splitting that produced 42 components instead of 5. The system did not crash. It processed all 448 work items and delivered a coherent result. The architecture absorbed a 42× overload without human intervention.

**Fifteen times faster by fixing one module.** The difference between a 46-minute run and a 3-minute run was not hardware, not models, not bandwidth — it was one Python module that lets the AI write naturally instead of forcing it into JSON. The lesson: work with the tool, do not fight the tool.

**The models are runts, and it still works.** Everything above was done with 3-billion-parameter models — the smallest, cheapest, dumbest models available. The architecture does not depend on model quality. Put 8B models in the Workers and 14B in the Queens, and the quality scales without changing a line of architecture code. Put 70B in the RajaBee and watch what happens to the answers.

---

## Phase 3 — The VMs, April 16, 2026

Five days after the LAN tests, we built the production cluster. Seven virtual machines on one physical host running Linux Mint 22.2. Each VM runs Ubuntu Server 24.04 with its own Ollama instance, its own AI models, and its own whisper.cpp installation for speech-to-text. Three tiers of hardware allocation mirror the hierarchy: the GiantQueen gets 12 gigabytes of RAM and 6 CPU cores, the DwarfQueens get 6 gigabytes and 4 cores, the Workers get 4 gigabytes and 2 cores. Twenty-one models total across seven machines — three per VM: a dense text model, a Mixture-of-Experts model, and a vision model.

Every model tag was verified against the live Ollama library before pulling. Every VM was smoke-tested with real inference — text reasoning, vision recognition, and speech-to-text transcription. The JFK inaugural address was transcribed correctly on all seven machines, from the GiantQueen's 800-megabyte Whisper Large model down to the Workers' 75-megabyte Whisper Tiny.

The cluster exists. It is running. It is waiting for the Laptop to build its eight VMs — including the RajaBee that will sit at the top of the entire hierarchy — and then the first full 15-machine experiment begins.

---

## The WaggleDance — Two AIs Coordinating Across Two Machines

The seven VMs on the Desktop were not built by a human typing commands. They were built by an AI assistant running on the Desktop machine, coordinated with another AI assistant running on the Laptop, communicating through a custom-built messaging system called WaggleDance — an ICQ for AI.

The WaggleDance server is an eighty-three-line Flask application running on the Laptop. Both AI assistants send and receive messages through it using curl. When a message tagged as TASK arrives, the ICQ agent on the receiving machine activates the Claude Code terminal window and types the message directly into it using operating-system-level keystroke injection. The receiving AI reads the typed message, acts on it, and sends a reply back through the same channel.

This is how the seven VMs were built: the Laptop AI wrote a detailed plan, pushed it to GitHub, and sent a one-line TASK through WaggleDance telling the Desktop AI to pull and execute. The Desktop AI built the VMs, hit problems, fixed them, and sent status updates back. When the Desktop AI needed a decision — disk sizing, model selection, whether to clone or autoinstall — the Laptop AI relayed the question to Nir, got the answer, and sent a TASK back. When the Desktop AI discovered that the autoinstall was unreliable, it reported through WaggleDance, received a new plan, and pivoted to cloning — all without Nir walking between rooms.

The WaggleDance was tested in the most honest way possible: by using it every day, under real production pressure, with real deadlines and real consequences for failure. Over two hundred messages were exchanged between the two AIs in a single week of parallel work. The system survived network configuration mistakes, wrong IP addresses, Windows firewall blocks, git merge conflicts on the chat log files, and an AI assistant that overwrote the working Windows startup instructions with Linux-only commands.

The IP address bug is worth telling. For days, the WaggleDance documentation listed the Laptop's IP address as 10.0.0.1. On April 16, the Desktop AI could not connect to the server. Ping worked — TCP was refused instantly. We investigated Windows firewall rules, disabled ASUS Smart Connect block rules, recreated the firewall allow rule from scratch. Nothing worked. Then the Desktop AI scanned every IP on the LAN and discovered that 10.0.0.1 was the router. The Laptop was at 10.0.0.4. The firewall investigation — hours of work by two AIs coordinating through GitHub files because the ICQ itself was broken — was a complete red herring. The fix was changing one digit in a URL.

The WaggleDance is not part of the KillerBee hive architecture. It is a separate system, built for a separate purpose: coordinating the builders, not the bees. But it proves something important about the broader thesis. Two AI systems, on two machines, coordinating through a shared message server, each autonomously executing complex multi-step tasks on their own hardware, each adapting when things go wrong, each reporting back through the same channel — this is the hive pattern. The WaggleDance is a hive of two, built to construct a hive of fifteen. The recursion is not a coincidence. It is the whole point.

---

## Experiment 4 — The Senses, April 18, 2026

The first three experiments proved the hive can distribute a text question across machines and combine the answer back up. They did not prove the hive could perceive the physical world. On April 18, 2026, on a single Laptop running Debian 13 with an RTX 5090 GPU, we closed that gap. Photos. Sound. Video. Same architecture. Same website. Same Queen-and-Workers pattern. Different inputs.

The work proceeded in five stages. Stage 0 was isolation: a Python virtual environment under `~/multimedia-feasibility/` with Pillow, ffmpeg-python, numpy, the Ollama client, and requests installed inside it, plus whisper.cpp built from source with CUDA targeting Blackwell architecture. No system packages were touched. Stage 1 tested each modality independently — one Python script per modality, direct calls to Ollama and whisper, no hive infrastructure. Stage 2 placed the sub-sampling logic inside one Python process, implementing the Chapter 12 double-grid principle. Stage 3 distributed that logic across a Queen and four Workers using Python multiprocessing. Stage 4 ran the full pipeline over real HTTP through BeehiveOfAI and HoneycombOfAI — the same infrastructure the text hive uses, no shortcuts.

The Stage 1 numbers. A 5.2 MB, 4189×2793 Wikimedia Commons portrait of a Rajasthan shepherd, fed to `qwen3-vl:8b` via the Ollama API, returned a 1,321-token description at 84 tokens per second — 67.3 seconds wall time — correctly identifying the turban colour, wooden staff, beaded necklace, earring, ring, arid landscape, and inferring Rajasthan from the attire. An 11-second JFK MP3 bundled with whisper.cpp was transcribed by `whisper-large-v3-turbo-q5_0.bin` in 1.235 seconds, roughly nine times real-time on Blackwell with CUDA and the native FP4 path enabled. A 30-second *Big Buck Bunny* clip (640×360, CC BY 3.0) had its audio extracted and one keyframe sampled every five seconds; whisper completed the audio in 0.56 seconds and `qwen3-vl:8b` processed each of six keyframes in roughly four seconds each, producing a visual timeline that tracked the rabbit's arc through the scene.

Stage 2 and Stage 3 proved the recursive sub-sampling principle — first in a single process, then across five. The most important result from Stage 2 was not a timing number. On the JFK clip, Grid A cut between "And so" at the 0–1 second slice and "my fellow Americans" at the 1–2 second slice. Grid B, offset by half a second, recovered "And so, my fellow" whole in its 0.5–1.5 second window. The dog-under-the-table fix — the reason the architecture uses two overlapping grids rather than one — worked exactly as the theory predicted. Stage 3 replaced the single process with a Queen and four Workers via Python multiprocessing and completed all three modalities in 58.1 seconds. One Worker misidentified the elderly shepherd as "an elderly woman." Another described a waving gesture as a stick held in the mouth. The Queen's gestalt and integration layer corrected both.

The first Stage 4 implementation was withdrawn. It introduced a `MULTIMEDIA:` subtask prefix and a `handle_multimedia_subtask` function in the Worker. When a Worker claimed a multimedia subtask, it ran the entire recursive pipeline — all eight photo tiles, or all audio slices, or all video keyframes — inside that single Worker process. The network path was real. The HTTP calls were real. The file transfer through `/uploads/` was real. But inside the Worker, the distributed principle had quietly collapsed back into one machine. This violated `BeehiveOfAI/CLAUDE.md` rule one — Workers are separate machines processing separate units. It violated the same Golden Rule described earlier in this book. Nir caught it. The implementation was withdrawn before any further work proceeded.

The redo was built correctly. A new `queen_multimedia.py` process logged in with queen credentials, claimed multimedia jobs from the BeehiveOfAI website, fetched the uploaded file itself, ran her own gestalt passes, and split the input into N `MULTIMEDIA_TILE:` subtasks posted over HTTP. Four separate Worker processes raced to claim each subtask independently. The Queen waited for every subtask, integrated via `phi4-mini`, and posted the Honey. All three modalities verified end-to-end.

Then Nir ran a three-minute audio clip — the ending of *Prince of Persia: The Sands of Time* — through the pipeline. The Workers processed all 365 one-second slices correctly. The resulting Honey was 1,280 characters and covered approximately the first twenty-two seconds of the recording. `phi4-mini` — a 3.8-billion-parameter model — received 365 slice descriptions in a single prompt, listed around twenty of them verbatim, and hit end-of-sequence. The remaining three minutes were missing. This was not an architectural failure. It was a scale failure specific to a small integrator.

The fix, committed as `HoneycombOfAI` `feec128`, was twofold. Audio slices widened from one second to five seconds, with Grid B at 2.5-second offsets, reducing the three-minute clip from 365 slices to 72. The integration step became hierarchical: when slice count exceeds `CHUNK_SIZE = 20`, the Queen sorts slices by timestamp, groups them into chunks of twenty, calls `phi4-mini` once per chunk to produce a time-window paragraph, then calls `phi4-mini` again on the chunk-paragraphs plus the gestalt. The re-run produced 11,639 characters of Honey covering the full three minutes — the opening apology to the Princess, the proposal of marriage, the doubt about trust, and the closing exchange about destiny.

Before implementing the section-based gestalt architecture, three honesty checks were run. The first swept varispeed ratios through the same three-minute clip, compressing audio with `ffmpeg asetrate` so that pitch shifts proportionally upward with speed. At 2×, whisper produced coherent transcription: *"Princess of Ireland, I was misled to attack your city. Forgive me, Highness."* At 3×: *"Dramatic music. Dramatic music."* At 4×: *"Slow-O-O-O-O-O-O-O-O."* At 6×: *"¶¶ Yeah."* The ceiling at 2× was established as an empirical fact about whisper's training-distribution pitch range. Nobody who has not run this test assumes the ceiling is 2× rather than 3× or higher.

The second check found a failure in `qwen3-vl:8b`. A synthesized sequence of five frames showing a red circle moving left to right produced an empty response field. The model's thinking mode was consuming the `num_predict` token budget before the `response` field was written. Prepending `/no_think` to the prompt moved the content to `response` correctly: *"The red circle moves horizontally from the left side of the frame to the right side across the sequence of frames."* One line change. The difference between a working deployment and a system that returns nothing.

The architectural theory for why this works — how a swarm of small perceivers can hold a gradient field and sub-sample a signal without any single member holding the whole picture — is documented in five chapters of *The Distributed AI Revolution* (Chapters 11 through 15). What this chapter proves is that the theory runs. On April 18, the Queen was a process. Four Workers were other processes. Every file traveled over HTTP. Every tile was claimed by a separate Worker. The Honey came back. The photos were described. The audio was transcribed. The video was timelined. No cloud, no subscription, no vendor, no license. One Laptop. One afternoon.

---

## The Ask

I built this. It runs on text. It runs on photos. It runs on sound. It runs on video. It runs on hardware you can buy at any electronics store. The models are free to download. The code is on GitHub. Anyone with a laptop and an internet connection can reproduce every experiment in this chapter in an afternoon.

The question is not whether it works. You just read the proof.

The question is who deploys it first. And the answer, if you do nothing, is China.

---

*Every timestamp, every component count, every calibration score, and every test result in this chapter can be verified in the KillerBee repository at github.com/strulovitz/KillerBee — file EXPERIMENT_LOG.md, committed with hashes anyone can audit. The Worker Bee Incident is real. The 46-minute catastrophe is real. The 3-minute fix is real. If you do not believe it, clone the repository and run it yourself.*
