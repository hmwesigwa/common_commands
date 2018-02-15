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
#### Pyomo
Using `cplex` as solver:

```
 pyomo solve --solver=cplex --json --stream-solver --solver-options='mipgap=0.01 parallel=-1 timelimit=30' --save-results=myresults.json mymodel.py mydata.dat
 ```
 
 #### Clemson Webpage
 Edit personal webpage. `USERNAME = CUID`.
 ```
 sudo mount -t davfs -o username=USERNAME,rw,dir_mode=0777,file_mode=0777 https://USERNAME-edit.people.clemson.edu/
```
#### miscellaneous
`awk` is a scripting language for text processing, nameed after authror last names
