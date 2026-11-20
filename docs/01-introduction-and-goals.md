# 1. Introduction & Goals

Raisync explores a question at the intersection of music and neuroscience. When someone listens to a piece of music, do changes in their electroencephalogram (EEG) occur at a consistent delay after sounds such as drum hits or note attacks? Raisync lets a user inspect what the listener heard alongside the electrical activity recorded at the scalp. Its engineering goal is to produce an analysis that others can reproduce offline and later verify during streaming replay.

## 1.1 Requirements Overview

**First milestone — Signal Explorer.** A user selects one real listening trial from OpenMIIR, a public dataset of EEG recordings paired with short musical excerpts. Raisync extracts the audio’s amplitude envelope (how its level changes over time) and marks detected onsets (when individual sounds begin). It plots both alongside a selected EEG channel on a shared time axis. The plot identifies the trial and channel, defines time zero as the start of the musical excerpt, and documents how the exact onset time of the musical excerpt was located in the EEG recording and with what precision. [OpenMIIR dataset and stimuli](https://github.com/sstober/openmiir)

**Scientific purpose.** The first plot lets a user inspect alignment and spot timing errors. Answering the research question requires data collected across multiple experimental trials, potentially involving different musical excerpts, experimental conditions, and participants. This allows researchers to evaluate whether observed relationships between musical rhythm and neural activity are reproducible rather than coincidental. Across listening trials, the user should be able to measure the average EEG

**Engineering purpose.** The offline analysis provides a reference result for a later public Signal Observatory. The observatory will replay recordings at their original pace, show the same features as they arrive, and compute results using the timestamps in the recording. A reviewer can then compare a streamed run with its offline reference and inspect what happened if processing fell behind or restarted.

## 1.2 Quality Goals

| Priority | Goal | How to verify it |
| --- | --- | --- |
| 1 | Timing accuracy | In an automated test, place an audio onset and an EEG marker at a known offset. The analysis recovers the offset within the documented timing resolution. For a real trial, the plot reports the source of the timing marker and any known uncertainty. |
| 2 | Reproducibility | From a clean checkout with locked dependencies, a second user can regenerate the example plot and feature values. The output identifies the input trial, code version, and analysis settings. |
| 3 | Agreement between offline and replay results | Process the same recording in both modes. Each completed time window has the same boundaries and event counts, and its numerical features agree within a stated tolerance. |
| 4 | Recovery from interruption | Stop the replay processor midway through a trial and restart it. The final output contains one result per expected window and matches an uninterrupted run. |
| 5 | Observable replay latency | At normal playback speed, 95% of window results are available within one second of the replay clock reaching the end of the window. The demo exposes this delay so a reviewer can check the target. |

## 1.3 Stakeholders

| Role | What they need from Raisync |
| --- | --- |
| Music cognition researcher or student | Inspect an individual trial, understand its timing uncertainty, and reproduce the comparison with time-shifted onsets before interpreting a pattern. |
| Public demo visitor | Follow a recorded excerpt and see where a sound begins, how its level changes, and what the EEG shows at that moment. |
| Project maintainer | Rerun a reference trial after a change and locate discrepancies in alignment, feature extraction, or replay. |
| Engineering hiring team or technical reviewer | Run the example independently and inspect evidence of data provenance, automated checks, replay latency, and recovery after a failure. |
