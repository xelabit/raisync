# 3. Context & Scope

Raisync starts with a recording of a completed listening experiment. OpenMIIR supplies what the participant heard and the EEG recorded during the session. Raisync is responsible for matching the excerpt to the trial, aligning the two signals, and showing how precisely their timing is known. The first milestone produces a local reference result. The later Signal Observatory replays the same inputs so a reviewer can compare streaming results with that reference.

## 3.1 Business Context

| External party | What they provide or select | What they receive |
| --- | --- | --- |
| OpenMIIR maintainers and dataset hosts | Participant EEG recordings, stimulus audio, and metadata describing the experiment. | Requests for the selected source files during setup. |
| Music cognition researcher or student | A listening trial, the EEG channel to inspect, and analysis settings. | A plot of the EEG, audio amplitude envelope, and detected onsets on one timeline, with the trial identity and timing uncertainty. |
| Project maintainer or technical reviewer | A reference trial to rerun. Later, the same trial to replay or restart. | Reproducible feature values and their provenance. During replay, the reviewer can inspect processing delay and compare completed time windows with the offline result. |
| Public demo visitor | A recording to follow in the later Signal Observatory. | A browser view of EEG and musical features unfolding at the original pace. Public audio playback follows the conditions in [chapter 2](02-constraints.md#23-dataset-licensing). |

The first milestone covers **one OpenMIIR music-perception trial**. Comparing responses across trials and against time-shifted onsets is a later scientific use case described in [chapter 1](01-introduction-and-goals.md). The experimental protocol, recruitment, and EEG acquisition belong to the original study. Live headset input and additional datasets are outside the scope of both the first milestone and the planned replay demo.

## 3.2 Technical Context

**Dataset files → Raisync.** Setup obtains the participant’s raw EEG file in FIF format from an OpenMIIR download source and the matching stimulus and metadata from the project repository. Both analysis modes read the cached files locally. The input selection identifies the participant, trial, listening condition, and stimulus. This matters because OpenMIIR also recorded trials in which participants imagined the music. [OpenMIIR files and download instructions](https://github.com/sstober/openmiir) · [Study conditions](https://doi.org/10.3389/fpsyg.2017.01255)

**Local command line → reference result.** The researcher supplies the trial and channel through the Signal Explorer command line. Raisync writes the synchronized plot and numerical features to local files, together with the source identifiers, code version, and settings. Time zero means the start of the musical excerpt. The listening experiment includes cue clicks, so the output identifies the marker or offset used to locate the music onset in the EEG. If the inputs cannot establish that alignment, the researcher sees the reason. [OpenMIIR stimulus and cue description](https://doi.org/10.3389/fpsyg.2017.01255)

**Replay → browser.** The later Signal Observatory runs locally and may also be hosted. A visitor selects and starts a recorded trial in the browser. Raisync uses the original recording timestamps to place features on the timeline and reports processing delay separately. If a result arrives late, its position relative to the music stays the same. While audio rights are unconfirmed, the public view displays the EEG trace, envelope, and onset markers with audio playback disabled.
