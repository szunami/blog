---
layout: post
title: Evaluating Optimizations With Criterion and Github Actions
tag: rust
---

## What

I set up a Github workflow to run Criterion benchmarks in a hosted runner.

The full workflow is defined [here](https://github.com/szunami/criterion_demo/blob/main/.github/workflows/bench.yml).

A sample benchmark report can be downloaded from the `Artifacts` dropdown [here](https://github.com/szunami/criterion_demo/pull/1/checks). Check out `report/index.html`.

## Why

When writing performance sensitive rust, I often have hypotheses about how to make things faster. It can be difficult to test these hypotheses in a robust way, especially when multitasking on my computer. I recently developed a workflow for doing this using [Criterion](https://lib.rs/crates/criterion) and Github Actions.

## How

Criterion has great support for [measuring changes in performance](https://bheisler.github.io/criterion.rs/book/user_guide/command_line_output.html#change). As the Criterion book mentions, performance can vary for [many reasons](https://bheisler.github.io/criterion.rs/book/user_guide/command_line_output.html#a-note-of-caution). To reduce the noise in my benchmarking, I set up a Github workflow that runs my benchmarks in comparison with the `main` branch. In my experience, Github hosted runners produce consistent performance results (Check out [this](https://github.com/szunami/criterion_demo/pull/2/checks) dummy change: )

## Caveats

This workflow runs benchmarks on `main` and then on the new branch, so it will take roughly twice as long as your benchmark suite. In theory, benchmarks on `main` could be reused to reduce CI time. Unfortunately this is not currently possible using vanilla Github Actions due to [limitations in Github's APIs](https://github.com/actions/download-artifact/issues/70).

In my experience, optimization hypotheses often relate to parts of code that are not well benchmarked. When using this workflow, it is best to add a new benchmark to your suite *before* opening a pull request that attempts to optimize the benchmark. This provides a baseline to measure against.