# Assignment2



## Question 1 

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

#Question 2

**I) SIMULATION SECONDS**

1. **specbzip** : 0.083664
2. **spechmmer** : 0.006329
3. **speclibm** : 0.017289 
4. **specmcf** : 0.058458
5. **specsjng** : 0.518333


**II) CPI**

1. **specbzip** : 1.673271
2. **spechmmer** :1.265776
3. **speclibm** : 3.457857 
4. **specmcf** : 1.16916
5. **specsjng** : 10.276660

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


[graphh.odt]

[graphh.odt](https://github.com/StellaMaria8/Assignment2/files/7693446/graphh.odt)


![Screenshot from 2021-12-10 16-39-32](https://user-images.githubusercontent.com/94965416/145591381-cb2875b3-cef8-4f63-b0da-3b615aca50fa.png)



















































































 

























 
