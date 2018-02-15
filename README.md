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


#### Other
