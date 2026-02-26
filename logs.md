setup changes

1. add requiremnts.txt
2. change verbal to deepseek version
   2.1 dotenv
   2.2 using latest openai syntax
3. use ax.bar instead of sns.barplot to match updated matplotlib version
   error:
   ```
   ValueError: 'yerr' (shape: (3,)) must be a scalar or a 1D or (2, n) array-like whose shape matches 'y' (shape: (1,))
   ```
4. change file path to add "../results/" and "../figures/"
   `File Not Found Error'`

modification

1. add aggregate_results.ipynb to aggregate the results from the 3 runs of deepseek-chat-v3 into one file for easier analysis and plotting
2. modify analysis_across_exps.ipynb for compare model performance to include the new deepseek-chat-v3 results and compare the performance with and without distractor in the n-back task
