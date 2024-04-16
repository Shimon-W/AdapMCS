# Adaptive Dispatching of Mobile Charging Stations using Multi-Agent Graph Convolutional Cooperative Reinforcement Learning
This is the pytorch/pytorch-geometric implementation of AdapMCS as described in the paper: "Adaptive Dispatching of Mobile Charging Stations using Multi-Agent Graph Convolutional Cooperative Reinforcement Learning".

<h3>Inference Times</h3>

Behavior of the inference times in scenarios with 100 and 150 permanently installed charging stations. The number of mobile charging stations is 10 for both scenarios.

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

Inferencing times based on the number of requests per day for Porto. The times remain constant except for irregularities due to unpredictable CPU/GPU utilization. The reason for this is that the number of requests does not influence the model, as these are summarized to a scalar value that reflects the total demand in the agent's local observation.

![Inference times in milliseconds over the course of the day with varying demand requests.](/assets/Inference_Time_Per_Requests.png)

