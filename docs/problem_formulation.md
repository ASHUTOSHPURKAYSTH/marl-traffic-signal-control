# Problem Formulation

**Problem:** Urban traffic signals operate on fixed cycles, unable to adapt to real-time conditions, causing congestion, fuel waste, and emergency response delays.

**Affected:** commuters, emergency vehicles, freight logistics, the environment.

**Why ML:** traffic is dynamic, stochastic, and non-linear; no closed-form map from traffic state to optimal phase; MARL handles multi-intersection coordination.

| Field | Details |
|---|---|
| Task | Multi-Agent RL |
| Input | Queue length, waiting time, flow rate, phase, time of day, neighbor states |
| Output | Phase action (NS-Green, EW-Green, NS-Left, EW-Left) |
| Sample | One decision step at one intersection |
| Labels | No pre-annotated labels; policy learned via reward (negative waiting time) |

**Success metric:** average vehicle waiting time (accuracy is not applicable, since this is a control problem).
**Partitioning:** train on one city, test on another (temporal correlation makes random splits invalid).
**Contingency:** pNEUMA, OSM + SUMO synthetic traffic, InTAS.
