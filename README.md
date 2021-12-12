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
- Size allocation για την L1 instruction cache 
- L1 data cache 
- L2 cache 
- Cache line size  ?

There have been multiple tests in order to figure out how these parameters affect the CPI.
Let's take for examble specbzip:

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


**SPECBZIB**



![image](https://user-images.githubusercontent.com/94965416/145718179-47e8a7c0-f0e2-476d-983f-08b25374a9a4.png)


![specbizpl1](https://user-images.githubusercontent.com/94965416/145719647-17589d61-055d-47f1-87b1-542689d3481e.png)



![specbzipl2](https://user-images.githubusercontent.com/94965416/145719659-ff73d52b-7732-4992-971a-12f12119d655.png)




**SPECHMMER**


![image](https://user-images.githubusercontent.com/94965416/145718748-910d8b36-0ec9-4a72-816d-6f8a79057600.png)


![spechmmerl1](https://user-images.githubusercontent.com/94965416/145719761-fc1951d5-2774-423f-bf35-f9eb609986f6.png)


![spechmmerl2](https://user-images.githubusercontent.com/94965416/145719772-f6d7c7ff-0ace-4d2e-97e2-fb0469d1c8a5.png)



**SPECLIBM**


![image](https://user-images.githubusercontent.com/94965416/145718991-72562260-979b-4bc0-a14a-bc8aac902cf7.png)


![spechmmerl1](https://user-images.githubusercontent.com/94965416/145719680-8523a95f-8e16-42f6-97db-1313b033e374.png)


![spechmmerl2](https://user-images.githubusercontent.com/94965416/145719667-044e83d3-0171-4331-9f9b-b5f6c6950b5c.png)


**SPECMCF**


![image](https://user-images.githubusercontent.com/94965416/145719144-201ffcf6-f7b2-411c-8cde-ad34716cc51a.png)


![spemcfl1](https://user-images.githubusercontent.com/94965416/145719735-6fbc67ba-8aca-40a6-a616-4a71e84f60d2.png)


![specmcfl2](https://user-images.githubusercontent.com/94965416/145719746-f781b3ba-d8d8-4e65-80e2-9e1a2db055a5.png)





**SPECSJENG**


![image](https://user-images.githubusercontent.com/94965416/145719248-142d1e49-880b-47b0-b985-2c553780efaa.png)


![specjngl1](https://user-images.githubusercontent.com/94965416/145719797-fea07817-e212-4b6b-8f56-2b9683f6d358.png)


![specjngl2](https://user-images.githubusercontent.com/94965416/145719806-c31ff5db-40a2-4134-b3f2-fbb6c1a769fa.png)



## Part 3

FINDING A FUNCTION WHICH DESCRIBES THE COST (AFTER TAKING INTO CONSIDERATION THE FACTORS IN PART 2)

Our main purpose is to create a CPU with the smallest possible CPI (best performance) that simultaniously has the smallest possible cost.
To achieve that, we will create a function that describes the cost.

Part 2 has shown that the main factor that affects the CPI value is the cacheline. L1 dcache also plays a big role in changing the CPI.After that, l1i slightly changes te CPI (specmcf).Associativities don't seem to play as much role as the other factors.

Taking into consideration the factors that affect the performance , we can put some multipliers to make obvious which show the impact of each parameter.

x,y,z,w,a can only take the values 0 or 1.

cacheline=5 x  (x=1 if cacheline is under 128kB and x=2 if it is over or equal to 128kB)

l1 dcache=3 y (y=1, if dcache<128kB and y=2 if dcache>=128)

l1 icache=1.5 z (z=1, if icache<128kB and y=2 if icache>=128)
 
l2 cache=1 w  (w=1, if l2 cache<1MB and y=2 if dcache>=1MB)

associativity=1 a (a=1, if associativity<2 and y=2 if associativity>=2)

**PERFORMANCE**=5x + 3y + 1.5z +1w +1a


COST function:

We can understand that the bigger the memory is, the  cost is larger. L1 cache has to be quite smaller than l2 cache for a bigger speed. 

So, if we put multipliers in the terms of cost:

l1 dcache =l1 icache = cacheline = 5

l2 cache=3

associativity=1

**COST**=
























































































































 

























 
