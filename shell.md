

### 流程控制语句

#### for
```
#!/bin/bash
#for(( i=1;i<10;i++ ))
for i in {094,356} {098..099} {369..380}
do
    sbatch hpl.slurm;
done
```
#### while
```
while read line
do 
    size=$(echo $line | awk '{print $1}')
    echo $size
done < file.txt
```

#### while 
colurm seprated by blank
```
while IFS=" ", read first second
do
    echo "$first"
done < file.txt
```

### 使用POSIX ACL控制对目录，文件的读写权限
#### setfacl
```
#!/bin/bash
for i in `cat name`
do
   cd /dssg/shake
   setfacl -m u:$i:rx vasp
   cd /dssg/vasp.6.2.1/bin
   setfacl -m u:$i:rx *
done


setfacl -x u:hpc vasp
```

#### sed替换文件中的目录
```
sed -i  "s:/lustre/home/acct-hpc/hpchgc/software/BTE/test/install/hypre/include:/hu/hu:g" CMakeLists.txt
```

#### sed替换文件中的字符串
```
sed -i  's/hu/ma/g' 1
```
### ***AWK***


