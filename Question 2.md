### Question 2 : Do django signals run in the same thread as the caller? Please support your answer with a code snippet that conclusively proves your stance. The code does not need to be elegant and production ready, we just need to understand your logic
### Answer :
Yes. Django signals run in the same thread as the caller. 
When a signal is triggered, the function connected to that signal will run in the same thread that sent the signal.

### Code Snippet :

Step 1: Importing necessary modules
```
from django.dispatch import Signal, receiver
import threading
```


Step 2: Create a signal
```
my_signal = Signal()
```

Step 3: Create a function that will be called when the signal is sent
```
@receiver(my_signal)
def my_signal_handler(sender, **kwargs):
    print(f"Signal received from: {sender}")
    print(f"Current Thread: {threading.current_thread().name}")
```

Step 4: Create a function that sends the signal
```
def send_signal():
    print(f"Sending signal from thread: {threading.current_thread().name}")
    my_signal.send(sender="MySender")
```

Step 5: Main Function
```
if __name__ == "__main__":
    print("Starting main thread:")
    send_signal()
```



### Explanation :
- We define a receiver function my_signal_handler that listens for my_signal. It prints who sent the signal and which thread is running.
- In the send_signal function, we send the signal. It also prints the name of the thread that is sending the signal.
- Main Execution
  - When you call send_signal, it will print the thread name from which it is sent.
  - The receiver function my_signal_handler will also print the thread name when it handles the signal.
