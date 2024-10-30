### Question 1 : By default are django signals executed synchronously or asynchronously? Please support your answer with a code snippet that conclusively proves your stance. The code does not need to be elegant and production ready, we just need to understand your logic

### Answer :
By default, Django signals are synchronous. Signals allow certain senders to notify a set of receivers when some action has taken place.
This means that the sender will wait for all the receiver functions to finish their execution before continuing.

In the simplest of the terms, it means that when one thing happens, the next thing waits until the first thing is done before it starts. 

### Code Snippet :

Step 1: Importing necessary modules
```
# Import necessary modules
from django.db.models.signals import post_save
from django.dispatch import receiver
from django.contrib.auth.models import User
```


Step 2: Create a signal that triggers when a new user is saved
```
@receiver(post_save, sender=User)
def user_created(sender, instance, created, **kwargs):
    if created:
        print(f"User {instance.username} has been created!")  # This runs immediately


```

Step 3: Create a new user to see the signal working
```
# In a django shell 
new_user = User.objects.create(username='new_user', password='password123')
```

### Explanation :
- When we create a new user with User.object.create(), Django sends a post_save signal.
- The user_created function is called right away. it checkes if the user was just created and prints a message immediately.
