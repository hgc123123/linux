

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
