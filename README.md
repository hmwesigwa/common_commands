## Important Commands
### Git 

`https://help.github.com/articles/basic-writing-and-formatting-syntax/` for README format

`git config --get remote.origin.url` to get git url

If you want to remove a file.txt
```
git rm file1.txt
git commit -m "remove file1.txt
git push
```
#### Linux


#### Palmetto

Get Job on bigmem:
```
qsub -q bigmem -I -X -l  select=1:ncpus=40:mem=1400gb,walltime=72:00:00
```
Delete at most 1000 jobs except `2684729.pbs02`
```
 for i in `qstat -u hushiji | grep hushiji | grep -v 2684729.pbs02 | awk -F" " '{print $1}' | awk -F"." '{print $1}' | head -n 1000 `; do echo $i && qdel $i ;done
```


#### Python
Read all `.txt` files in `mydir`
```
import os
mydir = '../'
mymodels = {}
for myfile in os.listdir(mydir):
  if myfile.endswith(".txt"):
    print(myfile)
```

Regular Expressions:
```
>>> import re
>>> re.findall(r'\d+', 'hello 42 I\'m a 32 string 30')
['42', '32', '30']
```
### Pyomo
Using `cplex` as solver:

```
 pyomo solve --solver=cplex --json --stream-solver --solver-options='mipgap=0.01 parallel=-1 timelimit=30' --save-results=myresults.json mymodel.py mydata.dat
 ```
 
 Scripting:
More info on scripting, e.g, warmstart, `https://github.com/Pyomo/pyomo/blob/master/doc/GettingStarted/current/scripts.txt`

Cplex solver options via pyomo:
```
from pyomo.environ import *
import maxflow  # model file is maxflow.py

instance = maxflow.model.create_instance('mydata.dat')  # data file
instance.f['A','C'] = 0
solver = SolverFactory('cplex')
solver.options['timelimit'] = 5
results = solver.solve(model, warmstart=True, tee=True)  #
instance.solutions.load_from(results)

```

 #### Clemson Webpage
 Edit personal webpage. `USERNAME = CUID`.
 ```
 sudo mount -t davfs -o username=USERNAME,rw,dir_mode=0777,file_mode=0777 https://USERNAME-edit.people.clemson.edu/
```
#### miscellaneous
`awk` is a scripting language for text processing, nameed after authror last names

### Parameters
#### CPLEX Parmaters
```
Available Parameters:

advance          set indicator for advanced starting information
barrier          set parameters for barrier optimization
clocktype        set type of clock used to measure time
conflict         set parameters for finding conflicts
cpumask          set cpubinding mask (off, auto, or a hex mask)
defaults         set all parameter values to defaults
dettimelimit     set deterministic time limit in ticks
distmip          set distributed parallel mixed integer optimization
emphasis         set optimization emphasis
feasopt          set parameters for feasopt
logfile          set file to which results are printed
lpmethod         set method for linear optimization
mip              set parameters for mixed integer optimization
network          set parameters for network optimizations
optimalitytarget set type of solution CPLEX will attempt to compute
output           set extent and destinations of outputs
parallel         set parallel optimization mode
preprocessing    set parameters for preprocessing
qpmethod         set method for quadratic optimization
randomseed       set seed to initialize the random number generator
read             set problem read parameters
sifting          set parameters for sifting optimization
simplex          set parameters for primal and dual simplex optimizations
solutiontype     set solution information CPLEX will attempt to compute
solutiontarget   set type of solution CPLEX will attempt to compute
threads          set default parallel thread count
timelimit        set time limit in seconds
tune             set parameters for parameter tuning
workdir          set directory for CPLEX working files
workmem          set memory available for working storage (in megabytes)

```
