# Chapter 1 Research — Google Search Results (2026-04-09)

All data from Google AI Overview, searched by Nir on 2026-04-09.

---

## API Pricing Comparison

### DeepSeek vs ChatGPT
- DeepSeek V3/R1: ~$0.28/M input tokens ($0.028 with cache hit), $0.42/M output
- ChatGPT GPT-4o/5.2: $2.50+/M input, up to $15+/M output
- DeepSeek is **96% cheaper** for reasoning tasks, **79% cheaper overall**
- DeepSeek allows self-hosting and local running (open-weight)

### Qwen vs Claude
- Qwen 3.5 Plus: $0.40/M input, $2.40/M output
- Claude Opus 4.6: $5/M input, $25/M output
- Qwen is **10-17x cheaper** than Claude
- Apache 2.0 license = self-host for free

### Kimi 2.5 vs Claude
- Kimi 2.5: $0.60/M input, $2.50-$3.00/M output
- Claude Opus 4.6: $5/M input, $25/M output
- Kimi is **8-12x cheaper**, designed to "destroy current high-end API pricing structures"
- 10 prompts on Kimi = cost of 1 on Claude Opus

---

## Revenue Numbers

### OpenAI
- 2025 revenue: ~$13B total, $20-21.4B annualized run rate
- 2026 (March): $25B annualized run rate
- NOT profitable until at least 2030
- Burning $8B/year in compute costs
- 15-20M paid ChatGPT users by mid-2025
- Plans to introduce advertising in ChatGPT

### Anthropic
- Early 2025: $1B annualized
- End 2025: $9B annualized
- Feb 2026: $14B annualized
- April 2026: $30B+ annualized
- Claude Code: $2.5B run-rate by Feb 2026
- 1000+ business customers spending $1M+/year (doubled from 500 in Feb)
- 70% of Fortune 100 using Claude

---

## ChatGPT Pricing Tiers (2026)
- Free ($0): Ads, tight usage limits, lower priority
- Go ($8/month): Ad-supported, higher limits
- Plus ($20/month): Ad-free, full GPT-5/5.2 access
- Pro ($200/month): Unlimited, deep research
- Team ($25-30/user/month)

---

## ChatGPT Ads (2026)
- Introduced early 2026, free tier + Go tier
- "Sponsored Recommendations" at bottom of conversations
- Managed through Criteo partnership
- $200,000 minimum spend for early ad partners
- Projected $1B ad revenue in 2026
- Contextual targeting, not personal data
- No ads for under-18 or sensitive topics

---

## DeepSeek Benchmarks
### DeepSeek R1
- MATH-500: 97.3% (vs GPT-4o ~83%)
- Codeforces: 96.3 percentile
- MMLU-Redux: 92.9
- MMLU-Pro: 84.0
- Open-weight model, local deployment possible

### DeepSeek V3.2 Speciale
- AIME: 96% accuracy
- Codeforces: 2701 rating
- GPQA: 73.8-84%
- 5x cheaper input, 24x cheaper output vs GPT-4o
- 128k context window, open-weight

---

## Nvidia Crash (Jan 27, 2025)
- Stock dropped 17% in one day
- Lost ~$589-593B in market value
- Largest single-day loss in U.S. stock market history
- Triggered by DeepSeek R1 announcement
- Caused wider semiconductor sell-off (Broadcom, AMD)
- Nasdaq down 3.1%

---

## Fine-Tuning Costs
- GPT-4o training: $25/M tokens
- GPT-4o-mini: $0.30-$3/M tokens
- Azure OpenAI: ~$100/hour for enterprise fine-tuning
- Does NOT include inference costs for using the fine-tuned model

---

## HuggingFace Community Fine-Tuners
### bartowski
- Most popular GGUF creator on HuggingFace
- Provides "imatrix" quants for better quality at lower sizes
- Uploads variants for almost every major new model

### Unsloth (Unsloth AI)
- Startup focused on faster/more efficient fine-tuning
- 2-5x faster training
- "Dynamic quants" for higher quality or smaller sizes

### mradermacher
- Prolific GGUF creator
- Specializes in "abliterated" (uncensored) models
- Quick to follow new foundation model releases

---

## OpenClaw / Anthropic War (2025-2026)
- Nov 2025: Peter Steinberger launches "ClawdBot"
- Anthropic forces rename (ClawdBot → Moltbot → OpenClaw)
- Feb 2026: Anthropic disables third-party OAuth for consumer subscriptions
- Feb 2026: OpenAI hires Steinberger to lead "personal agents"
- Anthropic absorbs OpenClaw features into Claude Code
- Apr 4, 2026: Anthropic bans third-party harnesses from subscription tokens
- Users forced to pay-per-token API (10-50x more expensive)
- One day of OpenClaw usage could cost Anthropic $1000+ in tokens
- Classic "Platform Squeeze": absorb features, block competitors

---

## AlphaGo Move 37 (2016)
- Game 2 vs Lee Sedol
- "Shoulder hit" on fifth line — experts thought it was a mistake
- "1 in 10,000" chance a human would play it
- Turned out to be brilliant — influenced center of board for late game
- Symbol of AI's capacity for creative, non-human strategy
- Our system explores these "1 in 10,000" branches that centralized AI skips

---

## Unconventional Parallel Computing
1. Quantum Computing: superposition + entanglement, 2^n states simultaneously (IBM, Google, D-Wave)
2. Neuromorphic Computing: brain-like, event-driven parallel (Intel Loihi, IBM TrueNorth)
3. DNA/Molecular Computing: trillions of strands in a drop (Adleman 1994, NP-complete problems)
4. Optical Computing: photons for parallel matrix multiplication (AI inference)
5. Cellular Automata & Membrane Computing: localized parallel cells
6. Reservoir/Chaos Computing: physical systems for higher-dimensional mapping
7. Memristive Computing: crossbar arrays for one-shot matrix multiplication (edge AI, IoT)
