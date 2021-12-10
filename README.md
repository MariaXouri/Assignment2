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
 
