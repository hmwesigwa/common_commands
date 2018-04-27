# Important Commands
## Table of Content
[Git](#git)

[Vim](#vim)

[Linux](#linux)

[LaTex](#latex)

[Palmetto](#palmetto)

[Python](#pyhon)

[Pyomo](#pomo)

[Clemson Webpage](#clemson-webpage)

[miscellaneous](#miscellaneous)



### Git 
---
[Git writing and formating](https://help.github.com/articles/basic-writing-and-formatting-syntax/) for README format

`git config --get remote.origin.url` to get git url

If you want to remove a file.txt
```
git rm file1.txt
git commit -m "remove file1.txt
git push
```

### Vim
```
v - select
V - select lines

```

#### Linux
---
 Convert files
`.png` to `.eps`. This converts all `.png` in the current directory to `.eps`
One file:

```
convert-im6 file.png file.eps

convert file.png file.eps  # did not work for me, internet says it should work
```
```
mogrify -format eps *.png
```
This reduces the file size of `.eps`. It first converts to `.pdf`
One file:
```
epstopdf filename.eps
pdftops -eps test.pdf
```
All files in directory:
```
find . -name "*.eps" -exec epstopdf {} ";"
find . -name "*.pdf" -exec pdftops -eps {} ";"

```

#### LaTex
---
Images display in same section use `\usepackage[section]{placeins}`

Adding x-axis and y-axis label to latex:
```
\documentclass{article}
\usepackage{tikz}
\usepackage{graphicx}
\usetikzlibrary{positioning}


\begin{document}

\begin{figure}[htb]
\begin{minipage}{0.4\textwidth}
\begin{tikzpicture}
  \node (img)  {\includegraphics[scale=0.225]{example-image}};
  \node[below=of img, node distance=0cm, yshift=1cm,font=\color{red}] {x-axis};
  \node[left=of img, node distance=0cm, rotate=90, anchor=center,yshift=-0.7cm,font=\color{red}] {y-axis};
 \end{tikzpicture}
\end{minipage}%
\begin{minipage}{0.4\textwidth}
\begin{tikzpicture}
  \node (img)  {\includegraphics[scale=0.225]{example-image}};
  \node[below=of img, node distance=0cm, yshift=1cm,font=\color{red}] {x-axis};
  \node[left=of img, node distance=0cm, rotate=90, anchor=center,yshift=-0.7cm,font=\color{red}] {y-axis};
\end{tikzpicture}
\end{minipage}%
\end{figure}
\end{document}

```

#### Palmetto
---
Get Job on bigmem:
```
qsub -q bigmem -I -X -l  select=1:ncpus=40:mem=1400gb,walltime=72:00:00
```
Delete at most 1000 jobs except `2684729.pbs02`
```
 for i in `qstat -u hushiji | grep hushiji | grep -v 2684729.pbs02 | awk -F" " '{print $1}' | awk -F"." '{print $1}' | head -n 1000 `; do echo $i && qdel $i ;done
```


#### Python
---
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
---
Using `cplex` as solver:

```
 pyomo solve --solver=cplex --json --stream-solver --solver-options='mipgap=0.01 parallel=-1 timelimit=30' --save-results=myresults.json mymodel.py mydata.dat
 ```
 
 Parameter Passing:
 
 [CPLEX Parameters](https://www.ibm.com/support/knowledgecenter/SSSA5P_12.6.3/ilog.odms.studio.help/pdf/paramcplex.pdf)
 
 ```
from pyomo.environ import *
opt = SolverFactory("cplex")
opt.options['mip limits solutions'] = 1
```

 Scripting:
For info like warmstart, see [Pyomo Scripting](https://github.com/Pyomo/pyomo/blob/master/doc/GettingStarted/current/scripts.txt)

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
 ---
 Edit personal webpage. `USERNAME = CUID`, `/webpage = <webpage directory>`
 ```
 sudo mount -t davfs -o username=USERNAME,rw,dir_mode=0777,file_mode=0777 https://USERNAME-edit.people.clemson.edu/ /webpage
```
#### miscellaneous
---
`awk` is a scripting language for text processing, nameed after authror last names


