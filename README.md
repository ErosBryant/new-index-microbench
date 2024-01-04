# index-microbench

## Generate Workloads ## 

1. Download [YCSB](https://github.com/brianfrankcooper/YCSB/releases/latest)

   ```sh
   curl -O --location https://github.com/brianfrankcooper/YCSB/releases/download/0.11.0/ycsb-0.11.0.tar.gz
   tar xfvz ycsb-0.11.0.tar.gz
   mv ycsb-0.11.0 YCSB
   ``` 


2. Create Workload Spec 
 
   The default workload a-f are in ./workload_spec 
 
   You can of course generate your own spec and put it in this folder. 

3. Modify workload_config.inp

   1st arg: workload spec file name
   2nd arg: key type (randint = random integer; monoint = monotonically increasing integer; email = email keys with host name reversed)

4. Make (dependency)

   - **masstree** and **pcm** need to run make command individually

   - MassTree
  
   ```sh
   cd masstree
   make
   ```

   - PCM

   ```sh
   cd pcm
   make
   ```

5. Generate Workloads
   
   ```sh
   mkdir workloads
   make generate_workload
   ```

6. Make (Benchmakr Tool)

   - Before doing make commands, your current path must be a /new-index-microbench

   ```sh
   make
   ```

(Optional) 7. If you use Python3

Change code in YCSB/bin/ycsb line 206:
   
   - except subprocess.CalledProcessError, err:
   - except subprocess.CalledProcessError as err:

Change all print in YCSB/bin/ycsb：
- print >>
  - print (  )

```sh
sudo ln -s /usr/bin/python3 /usr/bin/python
```

### Usage

The generated workload files will be in ./workloads

**NOTE** To generate email-key workloads, you need an email list (list.txt)# index-microbench 

**Usage**
   Example: ./workload a rand bwtree 1

   - Parameter (1)
      - workload type: a, c, e, none
      - none: it means we just load the file and exit 
   - Parameter (2)
      - key distribution: rand, mono 
   - Parameter (3)
      - index type: bwtree, skiplist, masstree, artolc, btreeolc, btreertm
   - Parameter (4)
      - number of threads (integer)
   
   - --hyper: Whether to pin all threads on NUMA node 0
   - --mem: Whether to monitor memory access
   - --numa: Whether to monitor NUMA throughput
   - --insert-only: Whether to only execute insert operations 

### INSTALL NOTES (DEPENDENCIES)

- Install papi
- Install tbb
- Install atomic from package manager
- Install libnuma-dev
- Install Java 8
- Install Python(or Python3)
