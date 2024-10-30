### Question 3 :  By default do django signals run in the same database transaction as the caller? Please support your answer with a code snippet that conclusively proves your stance. The code does not need to be elegant and production ready, we just need to understand your logic

### Note : Originally, I did not know this answer. I read the documentation (I assure you I am not copying this from ChatGpt) and am typing this answer from my gained understanding. I am still not well versed with this topic I 
### Answer :
By default, Django signals do not run in the same database transaction as the caller. 
This means that if you trigger a signal, any database changes made by that signal won't affect the original operation if the caller's transaction is rolled back.

### Code Snippet : 

