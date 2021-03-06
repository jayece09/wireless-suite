# Wireless Suite

## Overview
Wireless Suite is a collection of problems in wireless telecommunications.

Comparing research results in telecoms remains a challenge due to the lack of standard problem implementations against
which to benchmark.
To solve this, Wireless Suite implements some well-known problems, built as Open-AI Gym compatible classes.
These are intended to establish performance benchmarks, stimulate reproducible research and foster quantitative
comparison of algorithms for telecommunication problems.

## Getting started
The code has been tested to work on Python 3.7 under Windows 10.

1. Get the code:
    ```
    git clone https://github.com/nokia/wireless-suite.git
    ```

2. Use `pip` to install the package:
   ```
   pip install --upgrade pip
   pip install .
   ```
3. Modify the script *scripts/launch_agent.py* to execute an  environment of your choosing and obtain performance results.

## Provided problems 

### TimeFreqResourceAllocation-v0
This environment simulates a OFDM resource allocation task, where a limited number of frequency resources are to be
allocated to a large number of User Equipments (UEs) over time.
An agent interacting with this environment plays the role of the MAC scheduler. On each time step, the agent must
allocate one frequency resource to one of a large number of UEs. The agent gets rewarded for these resource allocation
decisions. The reward increases with the number of UEs, whose traffic requirements are satisfied.
The traffic requirements for each UE are expressed in terms of their Guaranteed Bit Rate (if any) and their Packet
Delay Budget (PDP).

You are invited to develop a new agent that interacts with this environment and takes effective resource allocation
decisions.
Four sample agents are provided for reference in the *wireless/agents* folder.
The performance obtained by the default agents on the default environment configuration is:
* Random                       -69590
* Round Robin                  -69638
* Round Robin IfTraffic        -3284
* Proportional Fair            -9595

Note that the above average rewards are negative values. The best performing agent is thus the Round Robin IfTraffic.

Additional details about this problem are provided in document *wireless/doc/TimeFreqResourceAllocation-v0.pdf*

#### Evaluation
The script *wireless/scripts/launch_agent.py* runs 16 episodes with a maximum of 65536 time steps each, and collects the reward
obtained by the agent on each time step. The result is calculated as the average reward obtained in all time steps on
all episodes.

## How to contribute
There are two main ways of contributing to Wireless Suite:

1. **Implementing new problems**: The first version of Wireless Suite contains only one problem implementation. New
problems can be easily added as simple variations of the first one (e.g. by changing its parameters), or by introducing
fully new problem implementations (e.g. Adaptive Modulation and Coding, Open Loop Power Control, Handover optimization,
etc).

2. **Implementing new agents**: Ideally, new agent contributions shall perform better than the default ones.

## References
1. [Open AI Gym Documentation](http://gym.openai.com/docs/)
2. [How to create new environments for Gym](https://github.com/openai/gym/blob/master/docs/creating-environments.md)
3. [Sacred Documentation](https://sacred.readthedocs.io/en/stable/index.html)
