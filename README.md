# Assessing Working Memory Capacity of Large Language Models (LLMs) Using N-back Tasks

![image](https://github.com/user-attachments/assets/f968575a-00be-4453-bc62-5d9237fa26fe)

This is a code and dataset repository for the paper "**[Working Memory Capacity of ChatGPT: An Empirical Study](https://arxiv.org/abs/2305.03731)**", which has been accepted by AAAI 2024 Conference on Artificial Intelligence.

Here we created a dataset to test the working memory capacity of language models. We choose the N-back task because it is widely used in cognitive science as a measure of working memory capacity. To create the N-back task dataset, we generated 30 blocks of trials for $N = \{1, 2, 3\}$, respectively. Each block contains 30 trials, including 10 match trials and 20 nonmatch trials. The dataset for each block is stored in a text file. The first line in the text file is the letter presented on every trial. The second line is the condition corresponding to every letter in the first line ('m':this is a match trial; '-': this is a nonmatch trial). We have created many versions of the N-back task, including verbal ones and spatial ones.

**Prompt Example.** Here we only focus on the base version of verbal N-back tasks. We use the following format of prompts for $N = \{1, 2, 3\}$:

```
User:
Instruction: as a language model, you are asked to perform a 1-back task. A letter will be presented on every trial. Your task is to respond with 'm' whenever the letter presented is the same as the previous letter, and '-' whenever the letter presented is different from the previous letter. A strict rule is that you must not output anything other than 'm' or '-'. Now begins the task.

User:
{letter}
Model:
{-}(because this is the first letter)

User:
{letter}
Model:
{m/-}

...
```

```
User:
Instruction: as a language model, you are asked to perform a 2-back task. A letter will be presented on every trial. Your task is to respond with 'm' whenever the letter presented is the same as the letter two trials ago, and '-' whenever the letter presented is different from the letter two trials ago. A strict rule is that you must not output anything other than 'm' or '-'. Now begins the task.

User:
{letter}
Model:
{-}(because this is the first letter)

User:
{letter}
Model:
{m/-}

...
```

```
User:
Instruction: as a language model, you are asked to perform a 3-back task. A letter will be presented on every trial. Your task is to respond with 'm' whenever the letter presented is the same as the letter three trials ago, and '-' whenever the letter presented is different from the letter three trials ago. A strict rule is that you must not output anything other than 'm' or '-'. Now begins the task.

User:
{letter}
Model:
{-}(because this is the first letter)

User:
{letter}
Model:
{m/-}

...
```

**Metrics.** We use exact match of the extraction results to calculate the hit rate, false alarm rate, and accuracy. $d'$ (detection sensitivity) is calculated as the $z$ score of hit rate minus the $z$ score of false alarm rate. In the case where the hit rate or false alarm rate is equal to either 0 or 1, they will be adjusted by 0.01 to handle the problem of $z$ score being infinite.

## Setup notes for Reproducibility using Deepseek API

### Prerequisites:

- Python 3.13.5
- Deepseek API key (you can apply for one at [Deepseek](https://platform.deepseek.com/), and you will need to top-up your account or link to a payment method to run the experiments)

### Instructions:

To reproduce the results in report using the Deepseek API, please follow the instructions below:

1. **Prepare the repository**: Clone this repository to your local machine, by running `git clone https://github.com/TommyS725/ChatGPT-WM.git`. And navigate to the project directory
2. **Install dependencies**: Install the required dependencies by running `pip install -r requirements.txt` in your terminal. Recommend to install under a virtual environment.
3. **Setup .env file**: Copy the `.env.example` file to `.env` and fill in your Deepseek API key.
4. **Run Verbal N-Back Test**: Run the notebook [verbal_deepseek.ipynb](experiments/verbal_deepseek.ipynb) to test the working memory capacity of language models on the base version of verbal N-back tasks.
   **Variables**:
   - `file`: the path of output file to save the results.
   - `blocks`: the number of blocks to run for each N-back condition (N = 1, 2, 3), default is 50.

5. **Run Verbal Test with Distractors**: Run the notebook [verbal_deepseek_distractor.ipynb](experiments/verbal_deepseek_distractor.ipynb) to test the working memory capacity of language models on verbal N-back tasks with distractors.
   **Variables**:
   - `file`: the path of output file to save the results.
   - `blocks`: the number of blocks to run for each N-back condition (N = 1, 2, 3), default is 50.
   - `distractor_freq`: the frequency of distractor trials, if set to `k`, then there will be one distractor trial every `k` trials.
6. **Run Verbal Test with Specific Temeperature**: Run the notebook [verbal_deepseek_temperature.ipynb](experiments/verbal_deepseek_temperature.ipynb) to test the working memory capacity of language models on verbal N-back tasks with specific temperature settings.
   **Variables**:
   - `file`: the path of output file to save the results.
   - `blocks`: the number of blocks to run for each N-back condition (N = 1, 2, 3), default is 50.
   - `temperature`: the temperature setting for the language model, it is set to 1.0 in base test.
7. **Aggregate Results**: If you have run the **same** test multiple times and want to combine the results, you can run the notebook [aggregate_result.ipynb](aggregate_result.ipynb) to aggregate the results across multiple runs. You need to specify the list of files to aggregate and the output file to save the aggregated results.
   **Variables**:
   - `files`: a list of file paths to the result files that you want to aggregate.
   - `new_file`: the path of output file to save the aggregated results.
8. **Analysis Across Experiments**: If you want to analyze the results across different experiments, you can run the notebook [analysis_across_exps.ipynb](analysis_across_exps.ipynb) to analyze the results across different experiments. To reproduce the results in the report, go to sections below and set the `exps` variable to the list of experiments you want to analyze, and set the `labels` variable to the corresponding labels for the experiments.
   **Sections**:
   - `Compare verbal n-back performance across different models`: Showing the performance of different models on verbal N-back tasks.
   - `Compare performance across verbal experiments with distractor n-back`: Showing the performance on verbal N-back tasks with different distractors.
   - `Compare verbal n-back performance across different temperature settings`: Showing the performance on verbal N-back tasks with different temperature settings.
