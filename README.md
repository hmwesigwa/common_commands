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
