# 2. Constraints

## 2.1 Local-first execution

The Signal Explorer must run on a reviewer’s laptop using its CPU and local storage. Setup may use the network to install locked dependencies and download the selected participant’s EEG recording, matching audio excerpt, and trial metadata. With those inputs cached and the network disconnected, a reviewer must be able to regenerate the synchronized plot and onset times for the real listening trial described in [chapter 1](01-introduction-and-goals.md).

The later Signal Observatory must be able to replay that same trial locally, using its recorded timestamps. A hosted demo is optional. Taking it offline must leave both the reference analysis and the local replay available for comparison.

## 2.2 Limited budget

The budget target for the first milestone is **€0 in additional hardware purchases or recurring service fees**. Existing hardware and recorded trials are sufficient. OpenMIIR distributes raw EEG separately, at roughly 700 MB per participant. Fetching only the selected participant’s recording and caching it keeps a routine rerun from downloading the full dataset. Small synthetic signals are sufficient for automated timing tests. [OpenMIIR download notes](https://github.com/sstober/openmiir#obtaining-the-raw-eeg-data)

For the later public demo, **€0–35 per month** is a planning estimate. It covers hosting considerations such as compute, storage, and outbound traffic. Until a hosting budget is set, the replay must be demonstrable on demand from the local machine.

## 2.3 Dataset licensing

| Material | Constraint for Raisync |
| --- | --- |
| EEG recordings and trial metadata | The OpenMIIR maintainers publish the dataset under the Open Data Commons Public Domain Dedication and License (PDDL 1.0). Record the source and version used for the reference trial and cite Stober et al. (2015) alongside published results, as the maintainers request. [OpenMIIR license and citation](https://github.com/sstober/openmiir#license-and-citations) |
| Musical excerpts | The stimuli include recordings of existing compositions. The PDDL covers rights held by the party granting it. Before bundling a clip in a release or playing it on the public website, document the basis for that use for both the composition and the specific recording. [OpenMIIR stimulus list](https://doi.org/10.3389/fpsyg.2017.01255) · [PDDL scope](https://opendatacommons.org/licenses/pddl/1-0/) |
| Public demo while audio rights are unconfirmed | Show the real trial’s EEG, onset markers, and amplitude envelope on the shared timeline with audio playback disabled. This preserves the link between the EEG and the excerpt the participant actually heard. A reviewer can reproduce the analysis locally using the matching stimulus from OpenMIIR. |
