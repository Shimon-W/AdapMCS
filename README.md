# Adaptive Dispatching of Mobile Charging Stations using Multi-Agent Graph Convolutional Cooperative Reinforcement Learning
This is the pytorch/pytorch-geometric implementation of AdapMCS as described in the paper: "Adaptive Dispatching of Mobile Charging Stations using Multi-Agent Graph Convolutional Cooperative Reinforcement Learning".

<h3>Evaluation of Hamburg</h3>

In order to further consolidate the generalizability of the approach, we evaluated the method in the city of Hamburg. To determine the demand distribution, we used a proprietary trajectory data set of a ride-hailing service in Hamburg. The charging network consists of 150 charging stations which were divided between two CSOs. We trained the full model, i.e. MAPPO + ADR + MAC, with 10 MCS for 7000 iterations and then evaluated it in both scenarios: with and without demand mutation.

| Model Setup       | Mutation | Profit[%] | MCS Profit[%] | CWT[%] | CSV[%] |
|-------------------|----------|-----------|---------------|--------|--------|
| EXISTING          |          |    100    |       0       |   100  |  45.47 |
| GREEDY            |          |   +9.81   |     +16.66    | -10.97 |  48.72 |
| MAPPO + ADR + MAC |          |   +13.83  |     +22.41    | -17.17 |  49.98 |
| EXISTING          |     X    |   +1.87   |       0       |  +1.24 |  46.15 |
| GREEDY            |     x    |   +4.23   |     +5.69     |  -3.41 |  46.80 |
| MAPPO + ADR + MAC |     x    |   +15.45  |     +23.90    | -16.10 |  50.19 |

<h3>Inference Times</h3>

Behavior of the inference times in scenarios with 100 and 150 permanently installed charging stations for Porto and Hamburg, respectively. The number of mobile charging stations is 10 for both scenarios.

```
city 	 | #FCS  | Inference Time [ms]
--------------------------------------
porto 	 | 100 	 | 8.75 
--------------------------------------
hamburg	 | 150 	 | 10.43 
--------------------------------------
```

Inference times in relation to the number of agents (MCS). The relationship is linear, since both the local/global observations and the action space increase linearly with the number of agents. All times are under one minute, so that each step can be calculated in time without falling behind schedule.

![Inference times in milliseconds with increasing number of MCS.](/assets/Inference_Time_Per_MCS.png)

Inferencing times based on the number of requests per day for Porto. The model contains 10 MCS. The times remain constant except for irregularities due to unpredictable CPU/GPU utilization. The reason for this is that the number of requests does not influence the model, as these are summarized to a scalar value that reflects the total demand in the agent's local observation.

![Inference times in milliseconds over the course of the day with varying demand requests.](/assets/Inference_Time_Per_Requests.png)

