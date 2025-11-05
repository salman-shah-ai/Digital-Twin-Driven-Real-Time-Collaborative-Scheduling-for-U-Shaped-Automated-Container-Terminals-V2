# Version 2.0

# Digital Twin-Driven Real-Time Collaborative Scheduling for U-Shaped Automated Container Terminals

## Overview

This repository contains a Python implementation of the Digital Twin (DT) and Deep Reinforcement Learning (DRL) based real-time collaborative scheduling system for U-shaped Automated Container Terminals (U-ACT), as described in the research paper "Digital twin-driven real-time collaborative scheduling for U-shaped automated container terminals".

## Key Features

- **U-shaped Terminal Modeling**: Accurate simulation of U-shaped automated container terminal layout and operations
- **Digital Twin Environment**: High-fidelity simulation of AGVs, Yard Cranes (YCs), Quay Cranes (QCs), and External Trucks (ETs)
- **PPO-based Scheduling**: Proximal Policy Optimization algorithm for dynamic equipment scheduling
- **Multi-equipment Coordination**: Real-time coordination between AGVs, YCs, and ETs
- **Performance Metrics**: Comprehensive monitoring of makespan, Terminal Congestion Index (TCI), and equipment utilization
- **Visualization Tools**: Interactive visualization of terminal operations and performance metrics

## Project Structure
```
📂 project_root/
├── u_act_digital_twin.py # Main implementation (environment, agent, visualization)
├── u_act_experiments.ipynb # Jupyter notebook for experiments
├── requirements.txt # Python dependencies
├── README.md # This file
└── u_act_scheduling_results.png # Example output visualization
```


## Installation

1. Clone the repository:
```bash
git clone https://github.com/your-username/u-act-scheduling.git
cd u-act-scheduling
```

2. Install required dependencies:
```bash
pip install -r requirements.txt
```

## Usage

### Running the Main Implementation

```python
from u_act_digital_twin import UACTEnvironment, PPOAgent, train_ppo_agent

# Initialize environment
env = UACTEnvironment(num_containers=100, num_agvs=5)

# Train PPO agent
trained_agent, metrics_history = train_ppo_agent(env, num_episodes=500)

# Run simulation with trained agent
state = env.reset()
for step in range(200):
    action, _ = trained_agent.get_action(state)
    state, reward, done, _ = env.step(action)
    if done:
        break
```

### Using Jupyter Notebook

Open the provided Jupyter notebook for interactive experiments:
```bash
jupyter notebook u_act_experiments.ipynb
```

## Key Components

### 1. UACTEnvironment

The core environment class that simulates:
- Container task generation (import/export flows)
- Equipment movement and coordination
- State space representation (20 dimensions)
- Reward calculation based on completion rate and waiting time

### 2. PPOAgent

Proximal Policy Optimization agent for dynamic scheduling:
- Actor-Critic network architecture
- Composite scheduling rule selection
- Adaptive learning based on terminal states

### 3. DigitalTwinVisualization

Comprehensive visualization tools:
- U-shaped terminal layout
- Real-time equipment positions
- Performance metrics tracking
- Equipment utilization monitoring

## Scheduling Rules

The system implements 6 composite scheduling rules from the research:

1. **Rule 1**: LRT_C + EUT_A + FCFS_Y
2. **Rule 2**: SRT_C + EUT_A + FCFS_Y  
3. **Rule 3**: LRT_C + SPT_A + FCFS_Y
4. **Rule 4**: SRT_C + SPT_A + FCFS_Y
5. **Rule 5**: LRT_C + NLR_A + FCFS_Y
6. **Rule 6**: SRT_C + NLR_A + FCFS_Y

## Performance Metrics

- **Makespan**: Total completion time for all tasks
- **Terminal Congestion Index (TCI)**: Ratio of AGV waiting time to total makespan
- **Equipment Utilization**: Load rates for AGVs and YCs
- **Task Completion Rate**: Progress of import/export container tasks

## Experimental Results

The implementation demonstrates:
- PPO outperforms traditional heuristic rules in most scenarios
- Effective reduction of AGV queuing time and system congestion
- Scalable performance across different terminal sizes
- Real-time adaptability to dynamic conditions

## Future Work

Based on the research paper, potential extensions include:
- Incorporating equipment failures and uncertainties
- Adding energy consumption and carbon emission objectives
- Modeling acceleration/deceleration phases for equipment
- Scaling to larger terminal configurations

## 👨‍💻 Author & Credits

Developed by **[Salman Shah](https://github.com/salman-shah-ai)**.
Based on the academic work by *Li et al., “Digital twin-driven real-time collaborative scheduling for U-shaped automated container terminals.”*

## Citation

If you use this code in your research, please cite the original paper:

```
@article{gu2025digital,
  title={Digital twin-driven real-time collaborative scheduling for U-shaped automated container terminals},
  author={Gu, Wenbin and Tang, Na and Yu, Haoyang and Wang, Lei and Cao, Yushang and Yuan, Minghai and Pei, Fengque},
  journal={International Journal of Production Research},
  year={2025},
  doi={10.1080/00207543.2025.2555540}
}
```

## License

This project is for academic and research purposes. Please refer to the original research paper for detailed methodology and contact the authors for commercial use.
