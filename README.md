# Assignment2

## Part 1

### Question 1 

a. commited instructions

1. **specbzip** : 100000001
2. **spechmmer** : 10000001
3. **speclibm** : 10000000 
4. **specmcf** : 100000000
5. **specsjng** : 100000000

  The executed instructions are not equal to commited instructions because after the execution the instructions stay in the buffer which has to check if the orders are speculative. If they are , they commit to memory (committed instructions).
 
  execute--> re order buffer--> check if speculative---> commited instructions
  
Non-Speculative :  If we don't need the result of the instruction the instruction is non-speculative.
  
  -------------------------------------------------------------------------------------------------




b. REPLACEMENTS (L1 DATA CACHE) :

1. **specbzip** : 681759
2. **spechmmer** : 10275
3. **speclibm** : 147631 
4. **specmcf** : 55092
5. **specsjng** : 5262346

---------------------------------------------------------------------------------------------

c. NUMBER OF ACCESSESS (L2 CACHE) :

*system.l2.overall_accesses :: total*
1. **specbzip** : 683562
2. **spechmmer** : 13327
3. **speclibm** : 149222 
4. **specmcf** : 190604
5. **specsjng** : 5264008

We can estimate the number of l2 cache accesses by these two metrics:

system.cpu.dcache.overall_mshr_misses::total + system.cpu.icache.overall_mshr_misses::total

number of overall MSHR misses + number of overall MSHR misses 

*MSHR* : miss status holding register

--------------------------------------------------------------------------------------------------------------

## Question 2

**I) SIMULATION SECONDS**

1. **specbzip** : 0.083664
2. **spechmmer** : 0.006329
3. **speclibm** : 0.017289 
4. **specmcf** : 0.058458
5. **specsjng** : 0.518333



![image](https://user-images.githubusercontent.com/94965416/145594680-263d3518-00e7-4c03-b6c7-ed58eefe76d7.png)




**II) CPI**

1. **specbzip** : 1.673271
2. **spechmmer** :1.265776
3. **speclibm** : 3.457857 
4. **specmcf** : 1.16916
5. **specsjng** : 10.276660


![image](https://user-images.githubusercontent.com/94965416/145595307-dbcb074d-1265-4a3c-87cc-69c372058eb8.png)


**III) MISS RATES**

- L1 ICACHE

1. **specbzip** : 0.000076
2. **spechmmer** : 0.001121
3. **speclibm** : 0.000928
4. **specmcf** : 0.004844
5. **specsjng** : 0.000015


- L1 DCACHE


1. **specbzip** : 0.014311
2. **spechmmer** : 0.003436
3. **speclibm** : 0.060934 
4. **specmcf** : 0.002124
5. **specsjng** : 0.121831


- L2 CACHE


1. **specbzip** : 0.295248
2. **spechmmer** : 0.348466
3. **speclibm** : 0.999430 
4. **specmcf** : 0.209015
5. **specsjng** : 0.999978


![image](https://user-images.githubusercontent.com/94965416/145598984-5b673afc-fd17-4bfb-9ca3-a205147a376b.png)


**Conclusuion** : 
- After taking into consideration the three charts, we can understand that there isn't a significant analogy  between the CPI  and the simulation seconds between the benchmarks.Additionally, there is no obvious analogy between the CPI and the miss rates of L1 icache and dcache because of their inconsiderable miss rates. On the contrary,we observe that the CPI is highly affected by miss rate in l2 cache. L2 cache has bigger miss penalty which justifies the fact that it affects the CPI more than the L1 cache.

- We can also observe that _specsjng_ benchmark has much bigger metrics in all aspects in comparison to the other benchmarks.

----------------------------------------------------------------------------------------------------------------------------------------------------------


## Question 3 

system_clk.domain -DEFAULT ----- system_cpu_clk_domain.clock -DEFAULT = 1 / ticks(ps) = 1/500ps = 1/0.5 ns = 2GHz

1. **specbzip** : 1000   -----   1. **specbzip** : 500          

2. **spechmmer** : 1000  -----   2. **spechmmer** : 500  

3. **speclibm** : 1000   -----   3. **speclibm** : 500

4. **specmcf** : 1000    -----   4. **specmcf** : 500

5. **specsjng** : 1000   -----   5. **specsjng** : 500


system_clk.domain -1.5GHz ---- system_cpu_clk_domain.clock -1.5GHz = 1 / ticks(ps) = 1/667ps = 1/0.667 ns = 1.5GHz

1. **specbzip** : 1000  ------ 1. **specbzip** : 667          

2. **spechmmer** : 1000 ------ 2. **spechmmer** :667 

3. **speclibm** : 1000  ------ 3. **speclibm** : 667

4. **specmcf** : 1000   ------ 4. **specmcf** : 667

5. **specsjng** : 1000  ------ 5. **specsjng** : 667


The cpu clock is being affected by the frequency change and it is set to 1.5GHz. The system cock remains the same.

The config.json file shows this difference in this following script.


"cpu_clk_domain": {
            "type": "SrcClockDomain",
            "cxx_class": "SrcClockDomain",
            "name": "cpu_clk_domain",
            "path": "system.cpu_clk_domain",
            "clock": [
                667 
                ]
                
If we have N CPUs then  the instructions will be executed in X time.

If we have N+1 CPUs then the instructions will be executed in (X*N)/(N+1) time.

So, if we put 2 CPUs the estimated time will be 667/2 ps. Which means that  the frequency will be 3GHz.


**SCALING**

Due to the cpu frequency change from 2GHz to 1.5GHz (1.5 = 3/4 x 2) the simulation seconds must be 4/3 x B (B:default sim_seconds). N = new sim_seconds/default sim_seconds


1. **specbzip** : 0.109329 , **N**=1.307
2. **spechmmer** : 0.008370 , **N**=1.322
3. **speclibm** : 0.020359, **N**=1.177
4. **specmcf** : 0.077242  , **N**=1.321
5. **specsjng** : 0.582132 , **N**=1.12

![image](https://user-images.githubusercontent.com/94965416/145613973-b0cc159f-8456-4ccc-be82-76ff230a2960.png)


*SCALING ORDER* spechmmer>specmcf>specbzip>speclibm>specsjng


Why is the scaling not perfect?

We can understand that there are mismatching values between the N parameter and 4/3.The pipeline has some stalls or accelerations which can cause different values in simulation seconds.

------------------------------------------------------------------------------------------------------------------------------------

## Part 2

### Question 1 

*How can we achieve bigger CPI value by changing

- Associativity 
- Block size 
- Size allocation for L1 instruction cache 
- L1 data cache 
- L2 cache 
- Cache line size  ?

There have been multiple tests in order to figure out how these parameters affect the CPI.
Let's take for examble SPECBZIP:

We tried different sizes in l1_dcache:

**SIZE**---**CPI**
        
default: 1.673271

16kB:    1.706060

32kB:    1.672933

64kB:    1.639115


_So we concluded that as the size increases, the CPI becomes smaller._


We also tried different sizes in l1_icache:

default : 1.673271

16kB : 1.639097

64kB : 1.638997

_So we concluded that as the size increases, the CPI becomes smaller._

Then we tried changing the l2 cache. 

default : 1.673271

540kB :  1.702099

2MB : 1.638

_So we concluded that as the l2 size increases, the CPI becomes smaller._

Different associativities:

default : 1.673271

l1i=1 l1d=1 l2=2 

CPI=1.661490

----------------

l1i=1 l1d=1 l2=1 

CPI=1.673903

-----------------

l1i=2 l1d=2 l2=4 

CPI=1.6381

*So we concluded that as the associativity increases, the CPI becomes smaller.

---------------------------

Different cacheline size:

cachline_size=64 

CPI=1.61

---------------------------

cachline_size=128  

CPI=1.595917

----------------------------------

_So we realized that as we increase the cacheline size, the CPI has a smaller value._

Finally, we put the maximum values so as to achieve a smaller CPI.

L1i cache=256kB
L1d cache=256kB
L2 cache=4MB
associativity=2,2,4
cachline_size=256

So the CPI is 1.539.

We understand that the higher the caches' size the smaller the CPI value is. The same happens with associativity. 
It is quite logical because as we increase associativity the miss_rates become smaller and these can cause CPI to have a smaller value. 

## Question 2

How each parameter affects CPI ,l1 miss rate and l2 miss rate in every benchmark?

(Miss rates of l1 cache are multiplied with  10^(-4))

**SPECBZIP**


<img width="454" alt="image" src="https://user-images.githubusercontent.com/94965416/145879571-e76d6f05-d1c8-4c9f-9be6-314e84fd4fa2.png">


<img width="454" alt="image" src="https://user-images.githubusercontent.com/94965416/145879509-f1812a3f-28d2-44d8-ba61-754799cdef81.png">


<img width="454" alt="image" src="https://user-images.githubusercontent.com/94965416/145879352-32bdad36-ed1d-4256-ac05-3bdc39d82743.png">




**SPECHMMER**



<img width="454" alt="image" src="https://user-images.githubusercontent.com/94965416/145879686-5a518c90-d2bf-46fc-afb2-63b88f953823.png">


<img width="454" alt="image" src="https://user-images.githubusercontent.com/94965416/145879741-7c79d051-8ab3-47dc-8f18-78d9b413fad2.png">


<img width="454" alt="image" src="https://user-images.githubusercontent.com/94965416/145869804-b701ddb7-1ab1-4e61-bb3b-6957092b5cc1.png">



**SPECLIBM**


<img width="454" alt="image" src="https://user-images.githubusercontent.com/94965416/145879803-c58cd7c5-4a5c-4503-b635-583eaefe1765.png">


<img width="454" alt="image" src="https://user-images.githubusercontent.com/94965416/145879828-ba1f721d-6b12-420c-93e6-2992939c45bd.png">


<img width="454" alt="image" src="https://user-images.githubusercontent.com/94965416/145869961-74ddd5af-fc2b-492b-9cfd-dbf3a7c3ff63.png">



**SPECMCF**



<img width="454" alt="image" src="https://user-images.githubusercontent.com/94965416/145879905-c023b500-6cfa-4e1a-b5df-1968c4f80ff3.png">


<img width="454" alt="image" src="https://user-images.githubusercontent.com/94965416/145879945-08d74afe-f6f0-4eab-950d-76b3f099a904.png">


<img width="454" alt="image" src="https://user-images.githubusercontent.com/94965416/145870143-f26759e1-530b-4af8-b1c6-32d99959f5ad.png">



**SPECSJNG**



<img width="454" alt="image" src="https://user-images.githubusercontent.com/94965416/145880044-7ce3c61f-55ec-4827-bbfc-08a6d8a79994.png">


<img width="454" alt="image" src="https://user-images.githubusercontent.com/94965416/145880140-742489f7-8fa7-4048-8406-1d5c93e5df7c.png">


<img width="454" alt="image" src="https://user-images.githubusercontent.com/94965416/145870277-73c2ee0b-d901-43d9-b88c-063d4fa605c0.png">



## Part 3

FINDING A FUNCTION WHICH DESCRIBES THE COST (AFTER TAKING INTO CONSIDERATION THE FACTORS IN PART 2)

Our main purpose is to create a CPU with the smallest possible CPI (best performance) that simultaniously has the smallest possible cost.
To achieve that, we will create a function that describes the cost.

Part 2 has shown that the main factor that affects the CPI value is the cacheline. L1 dcache also plays a big role in changing the CPI.After that, l1i slightly changes te CPI (specmcf).Associativities don't seem to play as much role as the other factors.

Taking into consideration the factors that affect the performance , we can put some multipliers to make obvious which show the impact of each parameter.


x: cacheline size/ maximum cacheline size

y: l1 dcache size/maximum l1 dcache size

z: l1 icache size/maximum l1 icache size

w: l2 cache size/maximum l2 cache size

q: associativity/maximum associativity


- cacheline=5 x 

- l1 dcache=3 y 

- l1 icache=1.5 z 
 
- l2 cache=1 w  

- associativity=1 q 

**PERFORMANCE** =5x + 3y + 1.5z +1w +1q
-----------------------------------------
COST function:

We can understand that the bigger the memory is, the  cost is larger. L1 cache has to be quite smaller than l2 cache for a bigger speed. 

So, if we put multipliers in the terms of cost:

- cacheline=5 x 

- l1 dcache=5 y 

- l1 icache=5 z 

- l2 cache=3 w

- associativity=1 q  
 
**COST = 5x + 5y + 5z + 3w + 1q**

------------------------------------------

The cost has to be as low as possible and the performance has to be as big as possible.


**EFFECTIVENESS=PERFORMANCE/COST** we want this fraction to be as big as possible (small cost and high performance)...

**EFFECTIVENESS=5x + 3y + 1.5z +1w +1q / 5x + 5y + 5z + 3w + 1q**



Some of the values that we tried are:

1) cacheline size = 16

   l1 dcache size = 32 kB

   l1 icache size = 16 kB

   l2 cache size = 1 MB

   associativity = 1
  
   EFFECTIVENESS = 0.56944
  
2) cacheline size = 32

   l1 dcache size = 64 kB

   l1 icache size = 32 kB

   l2 cache size = 2 MB

   associativity = 2
   
   EFFECTIVENESS = 0.788461
   
3) cacheline size = 32

   l1 dcache size = 256 kB

   l1 icache size = 32 kB

   l2 cache size = 2 MB

   associativity = 4
   
   EFFECTIVENESS = 0.607142 
   
   
 
 
 
 <img width="454" alt="image" src="https://user-images.githubusercontent.com/94965416/146065659-f9442bb2-fb10-4d31-a822-df8cc6ecbc50.png">
 
   
  
According to the type, the most efficient cpu comes from small l1i cache like 32kB or 64kB,
small associativities like 2 , mediocre l2 cache like 2MB and big l1d cache like 128kB.


















































































































 

























 
