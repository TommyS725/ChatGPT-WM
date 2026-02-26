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
