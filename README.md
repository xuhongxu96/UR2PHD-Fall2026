# Documents for UR2PHD - Fall 2026

[What is UR2PHD?](https://uwaterloo.ca/women-in-computer-science/programs-events/early-undergraduate-research-experience-program-erepur2phd)

## Project 1: A Compiler Optimization Observatory — Instrumenting LLVM at Scale

[Plan](Project1-Plan.md)

Every time you compile a C or C++ program, the compiler quietly rewrites
your code thousands of times to make it faster, e.g. "x + 0 -> x". In LLVM
(behind Clang, Swift, and Rust), one pass called InstCombine performs an
enormous share of these rewrites. We have built an open-source tool,
instcombine-debugger, that patches LLVM to record every transformation
InstCombine performs. This project extends that tool to capture richer
traces, turning an opaque, heavily-used optimizer into something we can
observe and understand.

Live demo: https://xuhongxu.com/instcombine-instrumentor/

## Project 3: An Agentic Harness for Implementing Missed Compiler Optimizations

[Plan](Project3-Plan.md)

AI coding agents can attempt real compiler work, but they stumble on
implementing optimizations: asked to add a rewrite rule to LLVM's
InstCombine pass, they often produce patches that miscompile programs,
break tests, or land in the wrong place, and our benchmarking shows agents
fail many such tasks. The open question is what feedback closes the gap:
when the agent is handed a correctness counterexample, a profitability
estimate, or a regression result, does its success rate improve, and which
helps most? This project answers that on a fixed open model in a fully
observable loop.

Recommended readings:
- https://arxiv.org/abs/2607.02684
- https://arxiv.org/abs/2607.02370
- https://github.com/dtcxzyw/llvm-harness