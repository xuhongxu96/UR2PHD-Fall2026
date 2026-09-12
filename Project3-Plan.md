## Students

- Aarnav Thite
- Jinay Desai
- Yulchan Shin
- Rohan Mandhotra (TBD)

## Overview

> Plans are subject to change.

| Week              | Date               | Objective                                                         |
| ----------------- | ------------------ | ----------------------------------------------------------------- |
| [Week 1](#week-1) | Term begins - 9/18 | Setup development environment; select papers                      |
| [Week 2](#week-2) | 9/21 - 9/25        | Paper presentation; assign tasks                                  |
| [Week 3](#week-3) | 9/28 - 10/2        | Share and discuss design docs (Task 1)                            |
| Week 4            | 10/5 - 10/9        | Develop the task 1                                                |
| Week 5            | 10/12 - 10/16      | Joint debugging and evaluate the minimal harness                  |
| Week 6            | 10/19 - 10/23      | Present the results; brainstorm tool ideas and assign next tasks  |
| Week 7            | 10/26 - 10/30      | Share and discuss design docs (Task 2)                            |
| Week 8            | 11/2 - 11/6        | Develop the task 2                                                |
| Week 9            | 11/9 - 11/13       | Evaluate the harness with tools                                   |
| Week 10           | 11/16 - 11/20      | Finish ablation studies; summarize and present the entire project |

## Resources

### Code Repository

- https://github.com/xuhongxu96/llvm-harness

### Recommended Readings

- https://mcyoung.xyz/2023/08/01/llvm-ir/
- https://llvm.org/docs/InstCombineContributorGuide.html
- https://llvm.org/docs/LangRef.html
- https://github.com/dtcxzyw/llvm-harness
- https://arxiv.org/abs/2607.02684
- https://arxiv.org/abs/2603.20075
- https://arxiv.org/abs/2607.02370
- https://arxiv.org/pdf/2607.01808

### Remote Dev Server (ppc64le, no GPU)

I will provide a remote server for you to run the harness and LLVM. You can also run it on your own machine if you prefer.
Notice that **the remote server is a ppc64le machine**, so you **won't be able to use VSCode remote** development extension to connect to it.
You can SSH into it and use `vim` or your preferred editors to edit the code.

### LLM Endpoint

I will setup a vllm on a GPU server and provide you an endpoint to access the LLM service. You can use it to run your agentic harness.

### API Key (Subject to Change)

In the later phase of the project, I may be able to provide you an API Key to access a model hosted by cloud providers. **It would be a paid service, but I will cover the cost.** You can use it to run the experiments more efficiently, but **please be mindful of the usage**. I will provide more details when the time comes.

## Week 1

### Objectives

1. Setup development environment for llvm-harness
2. Form two groups and select papers to present in the next week

### Tasks

#### Environment Setup

- [ ] Connect to the remote dev server (required)
    - [ ] Configure SSH keys
    - [ ] Test SSH connection
    - [ ] Clone the llvm-harness repo and **checkout the `ppc64le` branch**
- [ ] Local development environment setup (optional)
    - [ ] Clone the llvm-harness repo
    - Docker (Recommended)
        - [ ] Install Docker
        - [ ] Build your own Docker image (very time-consuming)
    - VM
        - [ ] Install a VM with Ubuntu 24.04
        - [ ] Install the dependencies manually (very time-consuming)
    - Local (Strongly NOT Recommended)
        - [ ] Install the dependencies manually (very time-consuming)
- [ ] Run Docker image (`llvm-harness` is already built on the server)
    - [ ] Start a tmux session: `tmux new -s <session name>` (to keep it running after logging out)
    - [ ] change directory to the llvm-harness repo
    - [ ] Start a container inside the tmux session: `docker run --rm -it -v $(pwd):/llvm-harness --cap-add=SYS_PTRACE --security-opt seccomp=unconfined llvm-harness:latest` (it could take a while)
    - [ ] Configure the API Key to access the LLM endpoint
    - [ ] Run the harness with a small example
- [ ] Clone the benchmark repo (https://arxiv.org/abs/2607.02684)

#### Paper Selection

In the next week's meeting, each group will present one paper.
Please read the papers and prepare a short presentation (10 minutes + 5 minutes for Q&A) to summarize the approach, the experiments, and the results. You can also discuss your thoughts on the paper and any questions you may have.

- [ ] Elect a team lead mainly for communication
- [ ] Form two groups
- [ ] Each group selects one paper to present
    - https://arxiv.org/abs/2603.20075
    - https://arxiv.org/abs/2607.02684

## Week 2

### Objectives

1. Present the selected papers
2. Assign the first-iteration tasks to each group

### Tasks

- [ ] Present and discuss the selected papers
- [ ] Assign the first-iteration tasks to each group
    1. Create a minimal agent harness based on llvm-harness framework with built-in tools only
        - References: [autofix/mini.py](https://github.com/xuhongxu96/llvm-harness/blob/main/autofix/mini.py) and [autoreview/archer.py](https://github.com/xuhongxu96/llvm-harness/blob/main/autoreview/archer.py)
    2. Create an evaluation script to run the harness on the benchmark and collect the generated patches
        - References: `<benchmark_repo>/pull_requests/*/metadata.json` and `<benchmark_repo>/scripts/agent/run.ts`

## Week 3

### Objectives

1. Each group presents their design doc
2. Discuss and finalize the design doc

### Tasks

- [ ] Prepare a design doc for your assigned task
    - Slides are not necessary, but you can use them if you want to.
- [ ] Present your design doc to the team
- [ ] Discuss and finalize the design doc
    - The gathering lasts for 1 hour, so each group has 10-15 minutes to present their design doc,
        and the rest of the time is for discussion.
