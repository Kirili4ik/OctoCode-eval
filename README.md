# OctoCode-eval
This repo is divided into 4 parts:
1. [[PDF]](https://github.com/Kirili4ik/OctoCode-eval) Annotated paper with comments and thoughts. Original paper: [OctoPack: Instruction Tuning Code Large Language Models by N Muennighoff et. al 2023](https://arxiv.org/abs/2308.07124)
1. [[notebook]](https://github.com/Kirili4ik/OctoCode-eval/blob/main/data_exploration/dataset_exploration_CommitPackFt.ipynb) Data Exploration (basic) for [CommitPackFt](https://huggingface.co/datasets/bigcode/commitpackft)
1. [[notebook]](https://github.com/Kirili4ik/OctoCode-eval/blob/main/eval_reproduction/OctoCoder_eval_reproduce.ipynb) Reproducing evaluation from the paper (using model: Octocoder; data: humanevalfixtests-python, pass@1: 31.4) + qualitative analysis
1. Final thoughts:

Commits can be used as a source of natural language instructions for code editing. This way has one clear advantage and disadvantage: while we have lots and lots of data, the quality is questionable. Even after lots of filtering done by the authors of the paper, the data can still be unpredictable and/or completely useless/lies (we have no guarantees or ways to check that). That brings me to a point where using datasets like CommitPack is a great idea for pretraining and training of backbones (as it sees like they word better than pure code datasets now), while final finetuning and polishing should probably be done via human-generated tasks/rlhf/dpo etc.

References:
- BigCode: [bigcode-project.org](https://www.bigcode-project.org/)
- Paper: [OctoPack: Instruction Tuning Code Large Language Models by N Muennighoff et. al 2023](https://arxiv.org/abs/2308.07124)
- Octopack: [github.com/bigcode-project/octopack](https://github.com/bigcode-project/octopack)
- CommitPackft: [huggingface.co/datasets/bigcode/commitpackft](https://huggingface.co/datasets/bigcode/commitpackft)
