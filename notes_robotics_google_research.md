# Robotics Chapter — Google Research Results (2026-04-10)

> All data from Google AI Overviews. Used for writing the robotics chapter.

---

## 1. Robot Training Costs (NVIDIA GPUs)

- Small models (experimentation): $2,000-$15,000 (1-7 days on 8x RTX 4090s)
- Large humanoid control models: $1.2M-$6M (3-8 weeks on 256x H200s)
- Advanced models (175B+ params): $25M-$120M+ in cloud computing
- Cloud H100 pricing: $2.75-$3.50 per GPU hour
- 100,000 H100 hours needed for serious 2B-14B training runs
- LoRA/fine-tuning reduces costs by 90%+ vs training from scratch

## 2. Parallel Simulations Scale

- Common: 4,096+ parallel robots on single GPU (Isaac Gym, Genesis)
- Advanced: tens of thousands of environments
- Total steps: hundreds of millions to billions of interactions per training run
- GPU-accelerated simulation eliminates CPU-GPU bottleneck
- Training time reduced from DAYS to MINUTES with massive parallelism
- PPO (Proximal Policy Optimization) algorithm used for parallel rollouts

## 3. NVIDIA Isaac Sim Requirements

- Minimum GPU: RTX 4080 (16GB VRAM) — $1,000+
- Recommended: RTX 4090/5080 — $1,400-$2,000+
- Professional: RTX 6000 Ada (48GB VRAM) — $5,000+
- Requires NVIDIA GPUs with RT Cores specifically
- 64-128GB RAM recommended
- Linux (Ubuntu) or Windows

## 4. MuJoCo Distributed Training

- MJX (MuJoCo XLA): fully vectorized on GPUs/TPUs, massive parallelization
- Supports multi-machine distributed training
- Architecture: "simulation on multiple worker nodes, send experience tuples to central learner node"
- THIS IS EXACTLY OUR RAJABEE → WORKERS ARCHITECTURE
- MuJoCo Playground: supports multi-GPU training, zero-shot sim-to-real
- Open source, runs on ANY hardware (not locked to NVIDIA)

## 5. How Tesla Trains Optimus

- Sim-to-real reinforcement learning pipeline
- Motion capture suits + first-person video for data
- 1,000+ units used internally for manufacturing tasks
- Cortex 2.0 AI training cluster (2026) for large-scale simulation
- Learning from internet videos (YouTube) by 2026
- CENTRALIZED approach — expensive, proprietary

## 6. How Figure AI Trains Robots

- "Helix" unified neural network controls entire body
- Thousands of virtual robots in parallel simulation
- Reinforcement learning + domain randomization
- Zero-shot sim-to-real transfer
- KEY QUOTE: "By 2026, Figure AI aims to have their robots learn from every other robot's experience via the cloud" — CLOUD DEPENDENT
- Teleoperation data + synthetic data generation

## 7. Chinese Robot Companies

- Unitree G1: UNDER $20,000 (vs Boston Dynamics $75,000-$150,000+)
- 20,000 units shipping in 2026 (250% increase from 2025)
- China produces 90% of global humanoid robots
- Unitree filed $610M IPO, $7 billion valuation
- "Robot schools" in China for real-world training scenarios
- Other players: AgiBot, Galbot, MagicLab, Noetix Robotics, TARS Robotics
- Open datasets being released (TARS "World in Your Hands")

## 8. Cloud vs Distributed Computing for Simulation

- Cloud: good for sporadic use, pay-as-you-go, 30% waste on idle resources
- Distributed: better for constant 24/7 heavy workloads, better long-term cost
- KEY QUOTE: "For large enterprise with consistent, heavy-duty simulation needs, setting up a distributed local cluster will provide better long-term cost benefits"
- OUR SYSTEM: the hive IS the distributed cluster, but with ZERO CapEx

---

## Key Arguments for Our Chapter

1. **Training costs are insane**: $1.2M-$6M for one humanoid model. Our system: free (volunteers' hardware)
2. **4,096 parallel sims on one GPU**: Our system does same across 4,096 Workers on cheap hardware
3. **MuJoCo already supports distributed**: worker nodes → central learner = our Workers → RajaBee
4. **Open source simulators exist**: MuJoCo, PyBullet run on ANY hardware, not locked to NVIDIA
5. **Tesla/Figure AI are cloud-dependent**: one outage = entire fleet stops
6. **China dominates cheap robots**: $20K Unitree + our free training = game over for $300K Western robots
7. **Distributed beats cloud for heavy workloads**: Google literally says so

## Chapter Structure (proposed)

Part 1: TRAINING — distribute simulation across hive (main substance, unique to this chapter)
Part 2: FIELD OPERATIONS — military resilience angle (brief, references drone chapter)
Part 3: HONEST COMPARISON — what we're good at vs what we're not (from notes_robotics_chapter.md)
