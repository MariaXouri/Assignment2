# Assignment2

## Part 1

### Question 1 

a. commited instructions

1. **specbzip** : 100000001
2. **spechmmer** : 10000001
3. **speclibm** : 10000000 
4. **specmcf** : 100000000
5. **specsjng** : 100000000

  executed instructions
  
  
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












































































 

























 
