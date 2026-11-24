# Multi-Agent RL for Adaptive Urban Traffic Signal Control

> Urban traffic signals operate on fixed cycles, unable to adapt to real-time conditions, causing congestion, fuel waste, and emergency response delays.

**Status: Phase 1 (Problem Formulation and Algorithm Survey).** No experimental results yet.

## Problem and Motivation
- Fixed-time signals waste green time on empty roads while other lanes queue
- Affects commuters, emergency vehicles, freight logistics, and the environment
- Traffic is dynamic and non-linear, so a learned adaptive policy is a good fit

## ML Formulation
| Field | Details |
|---|---|
| Task | Multi-Agent Reinforcement Learning (sequential decision making) |
| Input | Queue length per lane, waiting time, flow rate, current phase, time of day, neighbor states |
| Output | Signal phase action per intersection (4 discrete phases) |
| Unit of analysis | One decision step at one intersection (agent) |

## Pipeline
```
CityFlow JSON data -> Preprocessing (graph + features) -> CityFlow environment
-> GNN message passing -> MAPPO training -> Evaluation vs baselines -> Policy + logs
```

## Dataset
- **CityFlow Open Dataset** (Hangzhou, New York, Jinan): https://traffic-signal-control.github.io/dataset.html
- Format: JSON (`roadnet.json` + `flow.json`)
- See [`data/README.md`](data/README.md) for download steps
- Fallbacks: pNEUMA (Athens), InTAS (SUMO)

## Optimization Methods
- **Gradient Descent:** updates actor/critic network weights (core of learning)
- **Line Search:** adaptive step size for stable policy updates
- Details: [`docs/optimization_survey.md`](docs/optimization_survey.md)

## Evaluation Plan
- **Primary metric:** average vehicle waiting time (seconds)
- **Secondary:** throughput, emergency vehicle clearance time
- **Split:** train on Hangzhou, test on New York/Jinan (tests generalization across cities)
- **Baselines:** fixed-time, LP-based plan

## Scope
**In scope:** multi-intersection signal control, GNN coordination, emergency priority, baseline comparison
**Out of scope:** hardware deployment, pedestrian signals, accidents/closures, live camera integration, routing

## Assumptions and Limitations
- Simulator may not capture heterogeneous Indian traffic (bikes, autos)
- Instant communication between agents assumed
- Sim-to-real gap is possible
- GNN assumes a static road graph

## Project Status
- [x] Problem formulation
- [x] Optimization survey
- [ ] Environment setup (CityFlow wrapper)
- [ ] Baselines (fixed-time, LP)
- [ ] GNN + MAPPO implementation
- [ ] Training and evaluation
- [ ] Results and analysis

## Installation (planned)
```bash
git clone https://github.com/ASHUTOSHPURKAYSTH/marl-traffic-signal-control.git
cd marl-traffic-signal-control
pip install -r requirements.txt
```

## References
- Zhang et al., *CityFlow: A Multi-Agent RL Environment for Large Scale City Traffic Scenario*, WWW 2019
- Yu et al., *The Surprising Effectiveness of PPO in Cooperative Multi-Agent Games* (MAPPO), 2022
- Barmpounakis and Geroliminis, *pNEUMA drone dataset*, 2020

## License
MIT
