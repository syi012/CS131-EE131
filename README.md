| Jetson Nano Model | Nvidia Jetson Nano Developer Kit |
| :---: | :---: |
| Jetpack version | Jetpack 4.6.1 [L4T 23.7.1] |
| memory storage | 3.9gb max, 2.6 used |
| CPU temperature | 39 degree celsius |
| GPU temperature | 36 degree celsius |
| GPU shared ram | 547mb out of 3.9gb |
| # of ARMv8 Processor cores | 4 total |
| power useage | 2.8W power, 5.4V, 480 mA curr, 32.8A warn, 32.8A crit |

Screenshot of Jetson-stats application:  
![20240117_124428](https://github.com/syi012/CS131-EE131/assets/97487945/95f868d4-e7ae-4076-8d51-e93c5e177d48)

  
Jupyter Questions  
  
Question 1:  
Run the following code and explain its output  
%%time  
total = 0  
for i in range(1000):  
    for j in range(1000):  
        total += i * (-1) ** j  
  
Output:  
CPU times: user 1.48 s, sys: 0 ns, total: 1.48 s  
Wall time: 1.48 s  
  
Answer:  
So in this case, the code just printed out the the time needed to execute the given statement.  
  
Question 2:  
There are two blocks of code below performing the same function on a given input, explain why the second sort is much fast  
import random  
L = [random.random() for i in range(100000)]  
%time L.sort()  
  
%time L.sort()  
  
Answer:  
Basically, the difference is that we are going through the sort on a random unsorted list vs a sorted list which causes the discrepancy  
  
Question 3:  
Use Python memory_profiler to profile your own code and explain the results  
!pip3 install memory_profiler  
  
%load_ext memory_profiler  
  
# Your code goes here:  
def sum_of_lists(N):  
    total = 0  
    for i in range(10):  
        L = [i ^ (i) for i in range(N)]  
        total -= sum(L)  
    return total  
%prun sum_of_lists(300000)  
  
Answer:  
It outputs a table which as the order of total time on each function call, where the execution is spending the most time. in this case its the <ipython-input-19-68e8321615cf>:4(<listcomp>)  
  
Question 4.1:  
Modify each of the above function to capture their execution time (Both CPU and Wall). You can modify the code directly, if required.  
  
Answer:  
  
Execution time 1:  
hello world!  
Filename: /home/eric/Downloads/helloworld.py  
  
Line #    Mem usage    Increment  Occurrences   Line Contents  
=============================================================  
     3  75.6211 MiB  75.6211 MiB           1   @profile(precision=4)  
     4                                         def hello():  
     5  75.6211 MiB   0.0000 MiB           1   	print("hello world!")   

Execution time 2:  
Filename: /home/eric/Downloads/expressions.py  
  
Line #    Mem usage    Increment  Occurrences   Line Contents  
=============================================================  
     2  61.7695 MiB  61.7695 MiB           1   @profile(precision=4)  
     3                                         def my_func():  
     4  69.1094 MiB   7.3398 MiB           1       a = [1] * (10 ** 6)  
     5 221.7344 MiB 152.6250 MiB           1       b = [2] * (2 * 10 ** 7)  
     6  69.2891 MiB -152.4453 MiB           1       del b  
     7  69.2891 MiB   0.0000 MiB           1       return a  
     
Execution time 3:  
Array input elements:  
 [10, 20, 30, 40, 50]  
Applying log function:  
 [ 2.30258509  2.99573227  3.40119738  3.68887945  3.91202301]  
Applying cos function:  
 [-0.83907153  0.40808206  0.15425145 -0.66693806  0.96496603]  
Applying reciprocal function:  
 [0 0 0 0 0]  
Filename: /home/eric/Downloads/math_funcs.py  
  
Line #    Mem usage    Increment  Occurrences   Line Contents  
=============================================================  
     5  75.2500 MiB  75.2500 MiB           1   @profile(precision=4)  
     6                                         def math_funcs():  
     7  75.2500 MiB   0.0000 MiB           1   	inp_arr = [10, 20, 30, 40, 50]   
     8  75.2539 MiB   0.0039 MiB           1   	print ("Array input elements:\n", inp_arr)    
     9                                            
    10  75.2539 MiB   0.0000 MiB           1   	res_arr = np.log(inp_arr)    
    11  75.2539 MiB   0.0000 MiB           1   	print ("Applying log function:\n", res_arr)   
    12                                            
    13  75.2539 MiB   0.0000 MiB           1   	res_arr2 = np.cos(inp_arr)    
    14  75.2539 MiB   0.0000 MiB           1   	print ("Applying cos function:\n", res_arr2)   
    15                                            
    16  75.2539 MiB   0.0000 MiB           1   	res_arr3 = np.reciprocal(inp_arr)    
    17  75.2539 MiB   0.0000 MiB           1   	print ("Applying reciprocal function:\n", res_arr3)   

Execution time 4:  
red apple  
red banana  
red cherry  
big apple  
big banana  
big cherry  
tasty apple  
tasty banana  
tasty cherry  
Filename: /home/eric/Downloads/loops.py  
  
Line #    Mem usage    Increment  Occurrences   Line Contents  
=============================================================  
     7  75.6094 MiB  75.6094 MiB           1   @profile(precision=4)  
     8                                         def my_loops():  
     9  75.6094 MiB   0.0000 MiB           1   	adj = ["red", "big", "tasty"]  
    10  75.6094 MiB   0.0000 MiB           1   	fruits = ["apple", "banana", "cherry"]  
    11                                           
    12  75.6094 MiB   0.0000 MiB           4   	for x in adj:  
    13  75.6094 MiB   0.0000 MiB          12    		 for y in fruits:  
    14  75.6094 MiB   0.0000 MiB           9      			 print(x, y)  
   
Question 4.2:  
What patterns did you notice between each of the above function with respect to latency, memory usage and code ?  
  
Answer:  
When any line of code was called, if the values were already hardcoded, it didnt seem to increment the memory usage at all, but if there was any calculation involved then it would increase the memory usage. Also for the first function there were many instances of memory usage incrementing and decrementing while =he other functions were only incremented at the start for the most part. this matches the pattern in the latency as well. while the cpu times were estimated at a higher value, the functions wall time or time elapsed in real time were lower except for the first one.  
  
Question 4.3:  
Using %time magic command, we can trace overall code execution time. Sometimes, you might have to get deeper insights to identify performance bottlenecks. Write your own code and profile execution time line by line.  
  
Answer:  
Code:  
import random  
%time list = [random.random()-50 for i in range(256)]  
%time list.sort()  
%time list.sort()  
  
CPU times: user 0 ns, sys: 0 ns, total: 0 ns  
Wall time: 186 µs  
CPU times: user 0 ns, sys: 0 ns, total: 0 ns  
Wall time: 143 µs  
CPU times: user 0 ns, sys: 0 ns, total: 0 ns  
Wall time: 50.5 µs  

