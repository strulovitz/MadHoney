# Sonnet Plan — Expand Chapters 10 and 11 with Multimedia / Perception Material

**Drafted by:** Opus 4.7 (on Desktop, 2026-04-20)
**For execution by:** Sonnet 4.6 (after Nir switches to a cheaper model)
**Goal:** Add "the system does photos, sound, and video too" content to `chapter_10_the_proof.md` and `chapter_11_how_we_built_it.md` in the MadHoney repo — documenting experiments and code from **2026-04-18**, without duplicating the deeper conceptual material that already lives in Book 1 (`TheDistributedAIRevolution` chapters 11–15).

---

## 0. Read this before you touch anything

### 0.1 Who the reader of MadHoney is — the tonal lens

MadHoney is addressed to power: Pentagon, DARPA, NSA, Lockheed, Pfizer, JPMorgan, EU regulators. The tone is **cold, transactional, factual, slightly contemptuous** — "I accept your greed, I will weaponize it against you." Not heartfelt. Not victim-sympathy. **Monkey wrench, not moral outrage.** Facts strike harder than feelings. Every paragraph is a hammer.

This is different from Book 1 (`TheDistributedAIRevolution`), which is teacherly, exploratory, and written in Nir's natural discovery voice. **Do not copy Book 1's voice into Book 2.** Book 1 says *"let me walk you through this the way I actually thought about it."* Book 2 says *"this has already happened; here are the numbers; now what are you going to do."*

### 0.2 What you are adding — and what you are NOT adding

| | Add to MadHoney Ch10/Ch11? | Why |
|---|---|---|
| ✅ The April-18 multimedia experiment results | YES | Concrete proof that the system handles photos, sound, video |
| ✅ The new code files (`queen_multimedia.py`, `multimedia_handler.py`) | YES | Concrete proof that the blueprint is finished software, not theory |
| ✅ The bugs caught on April 18 and the fixes | YES | Matches the existing "five bugs" narrative of Ch10 and reinforces credibility |
| ❌ The deep conceptual discovery of sub-sampling / Grid A + Grid B / 4D maps | NO | That is Book 1 Chapters 11–15. MadHoney should reference Book 1 for depth, not reproduce it. |
| ❌ The gradient-field chapter for single-value sensors | NO | Book 1 Chapter 11 material. Out of scope for "we ran it" proof. |
| ❌ The octopus-is-slippery FAQ | NO | Book 1 Chapter 15. Too in-the-weeds for MadHoney's audience. |

**The distinction in one sentence:** MadHoney readers want *"it works, it has been built, the code is on GitHub, what are you going to do?"* — not *"here is the architecture theory."* Book 1 is for the second audience.

### 0.3 Do NOT do any of the following

- ❌ Do not replace anything already in Ch10 or Ch11. ADD new sections. Only rewrite an existing paragraph if it is genuinely badly written (if you do, explain why in the commit message).
- ❌ Do not invent numbers. Every figure (token count, wall time, slice count, byte count, line count, model name) must come from the source files listed in Section 1 below. If you cannot find a number, write "approximately" or ask the user — do not fabricate. (This is Golden Rule — `feedback_no_fabrication.md` in memory.)
- ❌ Do not propose new experiments or suggest more builds. Nir explicitly said: *"we will not do any more builds or experiments, so what there is in the whole Github that is all there is."* You document what exists; you do not extend.
- ❌ Do not add roleplay, motivational phrases, or flowery language. Match the existing Ch10/Ch11 tone: direct, factual, cold.
- ❌ Do not add emojis inside the book chapters (emojis go in chat with Nir, not in the artifact).
- ❌ Do not change the `README.md` table of contents. Just expand the two chapter files.

---

## 1. Read this in this order before writing anything

Read these files in full, in this order. Each one gives you something the next step depends on.

1. **`MadHoney/chapter_10_the_proof.md`** — the existing chapter you are expanding. Read the whole file. Notice the structure (Experiment 1, Bugs, Experiment 2, Experiment 3, Phase 3 VMs, WaggleDance, The Ask), the voice, the paragraph length, the use of concrete numbers, the cold framing at the end.

2. **`MadHoney/chapter_11_how_we_built_it.md`** — the existing chapter you are expanding. Read the whole file. Notice the blueprint feel — line counts, file names, endpoint counts, "Golden Rule" framing.

3. **`TheDistributedAIRevolution/build_and_test_log_2026_04_18.md`** — this is the PRIMARY source. Every factual claim you add to MadHoney Ch10 and Ch11 must come from this log. It is long (≈35 KB). Read it all. Note especially: Stage 0 through Stage 4, the first Stage 4 that was withdrawn, the redo with proper distributed tile split, the 365-slice overload on the 3-minute Prince of Persia clip, the varispeed ratio sweep (2× works, 3×+ breaks whisper), the `/no_think` trick for `qwen3-vl`, and the vocabulary cleanup (image tile / sound slice / video clip / video audio slice).

4. **`TheDistributedAIRevolution/chapter_11.md` through `chapter_15.md`** — skim these, don't read deeply. You need to know *what they cover* so you can reference Book 1 with a pointer instead of reproducing the content. Specifically: Ch11 = single-value sensors and gradient fields; Ch12 = sound (1D) and image (2D) sub-sampling with Grid A + Grid B; Ch13 = 3D and 4D scaling; Ch14 = RAG over reality; Ch15 = FAQ / slippery points.

5. **`TheDistributedAIRevolution/PERCEPTION_HIVE_DISCOVERY_CONVERSATION_2026-04-14.md`** — skim only. You don't reproduce it. You only need enough to write one pointer paragraph in MadHoney saying "the architectural theory behind this is documented in Book 1."

You are now ready to write.

---

## 2. Additions to `chapter_10_the_proof.md`

### 2.1 Where to insert

Insert a new top-level section titled:

> ### `## Experiment 4 — The Senses, April 18, 2026`

Place it **AFTER** the existing `## The WaggleDance — Two AIs Coordinating Across Two Machines` section and **BEFORE** the existing `## The Ask` section. Chronology: April 10 (Exp 1), April 11 (Exp 2, Exp 3, Bugs), April 16 (Phase 3 VMs, WaggleDance), April 18 (multimedia) → The Ask.

### 2.2 What the new section must cover (in this order)

Each bullet below is a sub-beat. Write each as one or two paragraphs, in the same tight factual style as the existing Experiment 1/2/3 sections. Do not over-explain. Numbers and verbs, not adjectives.

**Opening paragraph (one short paragraph):**
> The first three experiments proved the hive can distribute a text question across machines and combine the answer back up. They did not prove the hive could perceive the physical world. On April 18, 2026, on a single Laptop running Debian 13 with an RTX 5090 GPU, we closed that gap. Photos. Sound. Video. Same architecture. Same website. Same Queen-and-Workers pattern. Different inputs.

Then cover, in this order:

1. **The four stages of feasibility testing.** One short paragraph per stage (Stages 0–4). Stage 0 = isolated venv, Stage 1 = direct Ollama / whisper calls per modality, Stage 2 = one-process recursive sub-sampling, Stage 3 = Queen + four Workers via multiprocessing, Stage 4 = full distributed over real HTTP through BeehiveOfAI + HoneycombOfAI. Cite concrete results (see below).

2. **The Stage 1 single-modality results.** These are the "direct call to the models works" numbers:
   - Photo: a 5.2 MB / 4189×2793 Wikimedia Commons portrait of a Rajasthan shepherd, fed to `qwen3-vl:8b`. Produced a 1,321-token description at 84 tokens per second. The model correctly identified the turban, wooden staff, beaded necklace, earring, ring, arid landscape, and inferred *Rajasthan* from the clothing.
   - Sound: 11 seconds of an old JFK speech bundled with whisper.cpp, transcribed by `whisper-large-v3-turbo-q5_0` in 1.235 seconds — approximately 9× real-time on Blackwell with CUDA and native FP4.
   - Video: a 30-second clip of Big Buck Bunny (CC BY 3.0, 640×360), with audio extracted by `ffmpeg` and one keyframe sampled every 5 seconds, produced a plausible timeline plus transcription.

3. **Stage 2 and Stage 3 — the recursive principle proven on one machine.** One short paragraph. Note the Grid A + Grid B double-grid trick from Book 1 Chapter 12 actually worked: the phrase *"And so my fellow"* was recovered whole from a Grid B slice where Grid A had split it between *"And so"* and *"my fellow."* This is the first empirical demonstration that the dog-under-the-table fix (described in Book 1) behaves as the theory predicts.

4. **Stage 4 — the first version that we withdrew.** One paragraph. Document the discipline moment: the first Stage-4 implementation routed the entire file to one Worker which ran all eight image tiles (or all audio slices) in-process. This violated `BeehiveOfAI/CLAUDE.md` rule one — Workers are separate machines processing separate units. Nir flagged it. The implementation was withdrawn and redone with a proper `queen_multimedia.py` that genuinely splits into N `MULTIMEDIA_TILE:` subtasks over HTTP. This beat belongs in MadHoney because it demonstrates that the Golden Rule — the same one framed in Ch11 — is enforced in practice, not just in rhetoric.

5. **The three-minute Prince of Persia clip — 365-slice overload, hierarchical-integration fix.** One paragraph. The Queen's single `phi4-mini` integration prompt containing 365 slice descriptions drowned the 3.8-billion-parameter text model. It listed around twenty slices verbatim, summarized partially, and hit end-of-sequence early. The fix: widen slices from 1 second to 5 seconds (Grid A) with Grid B at 2.5-second offsets, so the same 3-minute clip produces 72 slices instead of 365. Second fix: hierarchical integration — when slice count exceeds `CHUNK_SIZE = 20`, the Queen sorts by timestamp, groups into chunks, calls `phi4-mini` once per chunk, then once on the chunk-paragraphs plus the gestalt. The re-run produced an 11,639-character Honey covering the full duration.

6. **The varispeed ceiling — an empirical finding about whisper.** One short paragraph. Sweep of 2×, 3×, 4×, 6× playback-rate compression through `ffmpeg asetrate` before transcription. At 2× the transcription was coherent (*"Princess of Ireland, I was misled to attack your city. Forgive me, Highness."*). At 3× and above, garbage (*"Dramatic music," "Slow-O-O-O-O," "¶¶ Yeah"*). The ceiling at 2× was established as an empirical fact about whisper's training-distribution pitch range. This is worth naming in MadHoney because it is the kind of concrete finding that shows the work is real: nobody who has not actually run the code knows the ceiling is at 2×.

7. **The `/no_think` fix for `qwen3-vl`.** One short paragraph. Initial empty responses from the vision model were traced to its thinking-mode consuming the `num_predict` budget before producing the `response` field. Prepending `/no_think` to the prompt fixes this. This is a one-line discovery that unlocks practical deployment on modest hardware. Again: specific and real.

8. **Closing paragraph for the section.** One short paragraph. Something like:
> The architectural theory for why this works — how a swarm of small perceivers can hold a gradient field and sub-sample a signal without any single member holding the whole picture — is documented in five chapters of *The Distributed AI Revolution* (Chapters 11 through 15). What this chapter proves is that the theory runs. On April 18, the Queen was a process. Four Workers were other processes. Every file traveled over HTTP. Every tile was claimed by a separate Worker. The Honey came back. The photos were described. The audio was transcribed. The video was timelined. No cloud, no subscription, no vendor, no license. One Laptop. One afternoon.

### 2.3 The Ask — update the closing paragraph of Ch10

The current `## The Ask` says "I built this. It works. It runs on hardware you can buy at any electronics store. The models are free to download. The code is on GitHub." — this implicitly referred only to text. Widen one sentence to acknowledge the senses:

Change:
> I built this. It works. It runs on hardware you can buy at any electronics store.

To:
> I built this. It runs on text. It runs on photos. It runs on sound. It runs on video. It runs on hardware you can buy at any electronics store.

(If the wording flows better another way, you may adapt — but preserve the cold cadence and keep the sentence short.)

### 2.4 Word-count target for the new section

Aim for **900–1,400 words** for the whole new `Experiment 4` section. The existing Experiment 1/2/3 sections combined are roughly that density. Do not exceed 1,600.

---

## 3. Additions to `chapter_11_how_we_built_it.md`

### 3.1 Where to insert

Insert a new top-level section titled:

> ### `## The Senses — Multimedia Handling`

Place it **AFTER** the existing `## The Buzzing System — The Boss Tests the Employee` section and **BEFORE** the existing `## The WaggleDance — How the Builders Talk to Each Other` section. Architectural reasoning: multimedia is part of the hive itself; WaggleDance is a separate builders-only intercom. Keep hive topics together.

### 3.2 What the new section must cover (in this order)

Match the blueprint tone of the rest of Ch11: line counts, file names, endpoint counts, no adjectives.

1. **Opening paragraph (short).** Name the two new files and the two modified files. Use the existing convention from Ch11 of *"**filename.py** (N lines) — one-line description."* Files:
   - `HoneycombOfAI/queen_multimedia.py` — the Queen Bee loop specialized for multimedia jobs. Line count: read from the build log (the log does not give an exact figure; if absent, write "approximately N lines" and compute N from the log's narrative, or omit the number and say "a new Queen module").
   - `HoneycombOfAI/multimedia_handler.py` — Worker-side handler with four branches: `photo`, `sound`, `video-clip`, `video-audio`. Line count: same rule as above.
   - `HoneycombOfAI/worker_bee.py` — modified to detect `MULTIMEDIA_TILE:` subtask prefixes and route into the handler.
   - `BeehiveOfAI/app.py` — modified to add `submit_multimedia` and `uploads/<filename>` serve routes.
   - `BeehiveOfAI/forms.py` — modified to add `SubmitMultimediaForm`.
   - `BeehiveOfAI/templates/submit_multimedia.html` — new upload form template.

2. **The unified section-based architecture.** One paragraph. Describe it cleanly: for any long audio or video, the Queen splits the recording into one-minute Grid A sections (at minute boundaries) and one-minute Grid B sections (offset by 30 seconds). Each section is compressed 2× with `ffmpeg asetrate` varispeed, so a one-minute section becomes roughly thirty seconds of audio that fits inside `whisper-large-v3-turbo`'s single-pass forward call. For video, frames are extracted at one FPS per section and passed as a list to `qwen3-vl:8b` in a single generate call with `/no_think`. The Queen makes section-level gestalts; Workers handle the individual tiles, slices, and clips below that.

3. **The division of labor between Queen and Worker, per modality.** One paragraph or a short table. Cover:
   - **Photo**: Queen produces a low-resolution gestalt (every other pixel on each axis). Workers claim image tiles — spatial regions defined by Grid A (four quadrants) and Grid B (four tiles straddling Grid A's midlines at 25% offsets).
   - **Sound**: Queen produces the section-level transcription (2×-compressed one-minute sections). Workers claim sound slices — five-second temporal windows at Grid A integer-second and Grid B 2.5-second offsets.
   - **Video**: Queen produces the section-level visual gestalt (one-FPS frame list per section) and runs the sound path on the audio track. Workers claim video clips — three-second temporal windows covering the whole frame with frames sampled at two FPS inside the clip.

4. **The models used.** One short paragraph or a table:
   - Queen-tier vision: `qwen3-vl:8b` (6.1 GB)
   - Worker-tier vision: `qwen3.5:0.8b` (1.0 GB)
   - Queen-tier speech-to-text: `ggml-large-v3-turbo-q5_0.bin` (548 MB) via whisper.cpp
   - Worker-tier speech-to-text: `ggml-tiny.bin` (75 MB) via whisper.cpp
   - Queen-tier integration: `phi4-mini:3.8b` (2.5 GB)
   - Worker-tier integration: `qwen3:1.7b` (1.4 GB)
   Total multimedia footprint: approximately 12 GB of models on disk, all free, all open-weight, all runnable on a single consumer GPU.

5. **Hierarchical integration for long inputs.** One short paragraph. Name the `CHUNK_SIZE = 20` rule: when slice count exceeds 20, the Queen sorts by timestamp, groups into chunks, calls `phi4-mini` once per chunk, then once on the chunk-paragraphs plus the gestalt. This is the same pattern as the original Queen-Worker integration — Queens compose what Workers produce — applied one level deeper inside the Queen's own synthesis phase.

6. **Vocabulary discipline.** One short paragraph. After the build, a vocabulary cleanup was committed (`HoneycombOfAI` `6809413`, `TheDistributedAIRevolution` `da0c8c3`) that disambiguated four terms that had collided during implementation:
   - **Image tile** — a spatial region of a photo.
   - **Sound slice** — a temporal audio window.
   - **Video clip** — a temporal video window covering the full frame.
   - **Video audio slice** — the audio-track temporal window of a video.
   - **Worker subtask** / **Worker unit** — the generic abstract term covering any of the above.
   Image tiles are spatial; video clips and audio slices are temporal; they are not interchangeable.

7. **Closing paragraph for the section.** One short paragraph, cold, pointing at Book 1:
> The architecture that makes all three modalities work is the same architecture that handled text in the previous sections of this chapter: Queen receives a job, produces a gestalt, splits the input into subtasks, distributes subtasks over HTTP to Workers on other machines, collects results, integrates via a model that is smaller than the ones the Workers ran, posts the Honey. The book that explains *why* the sub-sampling principle generalizes from text to sound to image to 3D space to 4D time is *The Distributed AI Revolution*, Chapters 11 through 15. This chapter documents only the code. The theory lives in the other book.

### 3.3 Do NOT touch the "Four Thousand Lines" opening section of Ch11

The opening section of Ch11 lists the line counts of the text-hive code (GiantHoneyBee + KillerBee). Those numbers remain correct for that scope. The multimedia code lives in a DIFFERENT pair of repos (HoneycombOfAI + BeehiveOfAI — the Level 1 repos). Treat it as a separate additional blueprint layer. Do not roll it into the "four thousand lines" figure.

### 3.4 Word-count target for the new section

Aim for **700–1,100 words**. The existing Ch11 sections (Golden Rule, Hierarchy, How a Question Becomes an Answer, Buzzing) are each 250–500 words. The new section is a bit larger because it covers three modalities, but it should not exceed Ch11's longest existing section by more than 2×.

---

## 4. Tone rules — match these exactly

1. **Short declarative sentences.** Ch10 example: *"This is the test that mattered."* Ch11 example: *"Thirty-four HTTP endpoints."* Use the same cadence.
2. **Numbers are verbs.** Don't say "many tiles" — say "eight tiles." Don't say "a few seconds" — say "1.235 seconds." Every claim has a number if a number exists.
3. **Cold authorial voice.** First person singular ("I built this") is fine when the existing chapter uses it. But no motivational framing, no inspirational phrases, no pep talks. The reader is a board member who is already skeptical of you. You respect their intelligence by being specific and unemotional.
4. **No bullet points inside the chapter prose.** Lists are fine when they make a table or a code-files enumeration, but running paragraphs should be prose. The existing Ch10/Ch11 use prose with commas and semicolons, not bullet explosions.
5. **No rhetorical questions except at the end of a section.** The Ask ends Ch10 with *"The question is who deploys it first. And the answer, if you do nothing, is China."* That kind of closing is fine. Inside the body of the chapter: zero rhetorical questions.
6. **Name the bugs.** The existing Ch10 "Worker Bee Incident" narrative works because it names the funny mistake. When you describe the withdrawn Stage 4 and the 365-slice overload, name them the same way.

---

## 5. Before you commit — verification checklist

Before running `git add` / `git commit` / `git push`, verify each item:

- [ ] Every number I added can be traced to a specific line in `build_and_test_log_2026_04_18.md` (or to a file I read myself with `wc -l`).
- [ ] I did not delete or rewrite any existing Ch10 or Ch11 paragraph, except the one sentence in "The Ask" covered in Section 2.3 above.
- [ ] I added exactly one new section to Ch10 (`## Experiment 4 — The Senses, April 18, 2026`) and exactly one new section to Ch11 (`## The Senses — Multimedia Handling`).
- [ ] Both new sections match the word-count targets (900–1,600 for Ch10; 700–1,100 for Ch11).
- [ ] The README.md table of contents is unchanged.
- [ ] No emojis in the chapter files.
- [ ] No roleplay language, no motivational filler, no rhetorical questions in the body.
- [ ] Both new sections end with a pointer to Book 1 (*The Distributed AI Revolution*) for the underlying theory — so MadHoney stays focused on proof-and-blueprint, not on re-teaching.
- [ ] I re-read the existing Ch10 and Ch11 one final time and my new sections feel like they belong there — if they don't, I adjust the tone before committing.

---

## 6. Commit and push

One commit per chapter keeps the history clean:

```bash
cd C:/Users/nir_s/Projects/MadHoney
git add chapter_10_the_proof.md
git commit -m "Ch10: add Experiment 4 — multimedia perception proven on Laptop April 18

Documents the photo/sound/video experiments (shepherd portrait, JFK clip,
Big Buck Bunny, Prince of Persia 3-min) through the distributed Queen+Workers
pipeline. Includes the 365-slice overload, the hierarchical-integration fix,
the varispeed 2x ceiling, and the /no_think trick for qwen3-vl.

Co-Authored-By: Claude Sonnet 4.6 <noreply@anthropic.com>"

git add chapter_11_how_we_built_it.md
git commit -m "Ch11: add The Senses — multimedia handling blueprint

Documents the two new files (queen_multimedia.py, multimedia_handler.py),
the unified section-based gestalt architecture, the division of labor
between Queen and Worker across the three modalities, the CHUNK_SIZE=20
hierarchical-integration threshold, and the vocabulary cleanup (image tile
vs sound slice vs video clip vs video audio slice).

Co-Authored-By: Claude Sonnet 4.6 <noreply@anthropic.com>"

git push
```

If a hook fails, fix the cause (encoding, formatting) and create a NEW commit — never `--amend`, never `--no-verify`.

---

## 7. If something is unclear

Ask Nir. Don't guess. He has repeatedly said it is better to ask one question than to invent a fact. Reference `feedback_ask_dont_guess.md` in memory.

If the question is about a specific experiment detail: re-read `build_and_test_log_2026_04_18.md`. The answer is almost always there.

If the question is about tone: re-read the existing Ch10 / Ch11 paragraphs nearest to where you are inserting.

If the question is about scope ("should this factoid go in?"): default to NO. MadHoney is dense. When in doubt, cut.

---

**End of plan.**
