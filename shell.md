

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
### **AWK**

#### 输出指定列，并匹配关键字段
```
awk 'NR==1 || $2~/you/ {printf "%-8s %-8s %-8s %-18s\n",$1,$2,$9,$12}' file.txt
```
#### 去掉第一行，只输出第9行消耗大于0的
```
awk 'NR>1 && $9>0 {printf "%-8s,%-8s,%-18s\n",$1,$9,$12}' file.txt
```
#### 输出某个字段字符以k开头的行
```
awk '{if($9>0){printf "%-8s,%-8s,%-18s\n",$1,$9,$12}}' top.txt
```

### 在结尾处输出统计的和
```
awk 'BEGIN {sum=0} {if($9>0){printf "%-8s,%-8s,%-18s\n",$1,$9,$12;sum += $9}} END {printf "sum is: %s\n",sum}' top.txt
```
###输出各个user的进程数
```
awk 'NR!=1{a[$2]++;} END {for (i in a) print i", " a[i];}' top.txt
```

###有序输出数组
```
awk 'BEGIN {into="this is a test";tlen=split(info,arra," ");for(k=1;k<tlen;k++){print k,arra[k];}}' top.txt
```

###判断是否存在key in array
```
awk 'BEGIN{info="it is a test";tlen=split(info,tA," ");for(k=1;k<=tlen;k++){print k,tA[k];}}'
```

###根绝字符匹配来确定文件拆分
```
awk 'NR>1 {if($0~/york/){printf "%-8s %-8s %-8s %-18s\n",$1,$2,$9,$12 > "1.txt"}else if($0~/root/){printf "%-8s %-8s %-8s %-18s\n",$1,$2,$9,$12 > "2.txt"}else{printf "%-8s %-8s %-8s %-18s\n",$1,$2,$9,$12 > "3.txt"}}' top.txt
```

***处理两个文件的格式***
```
awk 'BEGIN{} {} END{}' file1 file2
```
####合并两份文件
NR,表示awk开始执行程序后所读取的数据行数.
FNR,与NR功用类似,不同的是awk每打开一个新文件,FNR便从0重新累计.
```
 awk '{ if (NR==FNR) {arraya[$1]=$2} if (NR!=FNR) { arrayb[$1]=$2}}END{for (i in arraya) {print i,arraya[i],arrayb[i]}} ' file1 file2  > x
sort -n -k 1 -t ' ' x
```

