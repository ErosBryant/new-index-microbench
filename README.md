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

4. Generate

   ## Need ***Make*** file in masstree & pcm & rotate-skiplist

   ```sh
   mkdir workloads
   make generate_workload
   ```

5. If you use Python3

Change code in YCSB/bin/ycsb line 206:
- except subprocess.CalledProcessError, err:
  - except subprocess.CalledProcessError as err:

Change all print in YCSB/bin/ycsb：
- print >>
  - print (  )

```sh
sudo ln -s /usr/bin/python3 /usr/bin/python
```

The generated workload files will be in ./workloads

1. NOTE: To generate email-key workloads, you need an email list (list.txt)# index-microbench 


### INSTALL NOTES

- Install papi
- Install tbb
- Install atomic from package manager
- Install libnuma-dev
- Install Java 8
- Install Pythone(3)
etc. 