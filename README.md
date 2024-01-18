| Jetson Nano Model |  |
| :---: | :---: |
| Jetpack version |  |
| memory storage |  |
| CPU temperature |  |
| GPU temperature |  |
| GPU shared ram |  |
| # of ARMv8 Processor cores |  |
| power useage |  |

Jupyter Questions

Question 1:
Run the following code and explain its output
%%time
total = 0
for i in range(1000):
    for j in range(1000):
        total += i * (-1) ** j

Answer:

Question 2:
There are two blocks of code below performing the same function on a given input, explain why the second sort is much fast
import random
L = [random.random() for i in range(100000)]
%time L.sort()

%time L.sort()

Answer:

Question 3:
Use Python memory_profiler to profile your own code and explain the results
!pip3 install memory_profiler

%load_ext memory_profiler

# Your code goes here

Answer:

Question 4.1:
Modify each of the above function to capture their execution time (Both CPU and Wall). You can modify the code directly, if required.

Answer: 

Question 4.2:
What patterns did you notice between each of the above function with respect to latency, memory usage and code ?

Answer:

Question 4.3:
Using %time magic command, we can trace overall code execution time. Sometimes, you might have to get deeper insights to identify performance bottlenecks. Write your own code and profile execution time line by line.

Answer:

