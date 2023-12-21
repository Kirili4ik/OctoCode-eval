# OctoCode-eval
This repo is divided into 5 parts:
1. [[PDF]](https://github.com/Kirili4ik/OctoCode-eval/blob/main/2308.07124_annotated.pdf) Annotated paper. Original paper: [OctoPack: Instruction Tuning Code Large Language Models by N Muennighoff et. al 2023](https://arxiv.org/abs/2308.07124)
1. [[notebook]](https://github.com/Kirili4ik/OctoCode-eval/blob/main/data_exploration/dataset_exploration_CommitPackFt.ipynb) Data Exploration (basic) for [CommitPackFt](https://huggingface.co/datasets/bigcode/commitpackft)
1. [[notebook]](https://github.com/Kirili4ik/OctoCode-eval/blob/main/eval_reproduction/OctoCoder_eval_reproduce.ipynb) Reproducing evaluation from the paper (using model: Octocoder; data: humanevalfixtests-python, **pass@1: 31.4**) + qualitative analysis
1. [Thoughts and comments on the paper](#Thoughts-and-comments-on-the-paper)
1. [Final thoughts on using commits as instructions](#Final-thoughts-on-using-commits-as-instructions)

### Thoughts and comments on the paper
Authors state the creation of CommitPack(FT), HumanEvalPack and Octocoder model. I feel like CommitPackFT does not bring a lot of value since in the authors' comparison instruct-tuning on OASST vs OASST+CommitPackFT shows almost no difference:
<img src="https://github.com/Kirili4ik/OctoCode-eval/assets/30757466/fcf1976b-dc3a-49f9-8873-c3998126bb7a" width="850" height="300">
<img src="https://github.com/Kirili4ik/OctoCode-eval/assets/30757466/8226e3e5-7254-4f05-a09b-0ad8805f20f8" width="600" height="300">

CommitPackFT does improve the results, but if there was more data from OASST for coding - it could possibly be better without CommitPackFT. **Moreover!** The difference is the most visible on CodeFixing (HUMANEVALFIX) - but it should be noted that this data is only couple of hundred hardcoded(by the authors!) examples. We have to just hope it is a coincidence =)))

I would also like to mention that authors compare models splitting them into non-permissive and permissive models. It is a valid comparison, but in my opinion we should compare instruct-tuned moels with instruct-tuned models (yellow on the graph later). In my opinion there is close to no value in comparison Octocoder to BLOOMZ for example. It should also be noted that authors approach of using OASST+CommitPackFT has the same or worse metrics compared to WizardCoder where the automatically-generated instructions were used.
<img src="https://github.com/Kirili4ik/OctoCode-eval/assets/30757466/afbb3a1f-394d-40a3-a68c-bc870e739999" width="300" height="500">




### Final thoughts on using commits as instructions
Using commits as a source of NL instructions has one clear advantage and disadvantage: while we have lots and lots of data, the quality is questionable. Even after lots of filtering done by the authors of the paper, the data can still be unpredictable and/or completely useless/lies (we have no guarantees or ways to check that, and it is actually seen in the notebooks). We should also compare this approach with 2 different ones being Generating instructions using gpt-4 / self-instruct and scraping people's dialogues with assistants (OASST). Obviously all the approaches have their own advantages and disadvantages, but as we see in the graphs - commits add the least amount of points. I believe that the other approaches have more perspectives.

**Addition--1**, we should note that at least [40% of code is already written by copilot](https://news.ycombinator.com/item?id=35161866). While it is [OpenAI Codex, which is a modified, production version of the GPT-3] (https://www.infoworld.com/article/3629469/openai-offers-api-for-github-copilot-ai-model.html). So basically a lot of code and probably commits are written by OpenAI models meaning that generating instructions and parsing repositories soon will be very similar! 

**Addition--2**, there is no comparison with the new CodeLLama models:

<img src="https://github.com/Kirili4ik/OctoCode-eval/assets/30757466/33f49ad3-4e82-4293-84bd-6cdffb26ce5c" width="250" height="350">

On the [BigCode leaderboard in HumanEval-Python](https://huggingface.co/spaces/bigcode/bigcode-models-leaderboard) CodeLLama-based models are almost twice as good as OctoCoder model being smaller! One might think that CodeLlama models are not available for commercial use, but they actually are before 700mil users:
![image](https://github.com/Kirili4ik/OctoCode-eval/assets/30757466/b0737cfd-6d88-4705-b4e8-b0c4bdb155f9)

**Moreover**, we can see that CodeLLama-Python have not been instruct-tuned, but already shows impressive results!


### References:
- BigCode: [bigcode-project.org](https://www.bigcode-project.org/)
- Paper: [OctoPack: Instruction Tuning Code Large Language Models by N Muennighoff et. al 2023](https://arxiv.org/abs/2308.07124)
- Octopack: [github.com/bigcode-project/octopack](https://github.com/bigcode-project/octopack)
- CommitPackft: [huggingface.co/datasets/bigcode/commitpackft](https://huggingface.co/datasets/bigcode/commitpackft)
