##求从1加到100的和

###使用for循环求和：
```
#!/bin/bash

declare -i sum=0

for ((i=1;i<=100;i++));do

	let sum+=$i

done

echo "sum=$sum"
```
###使用until循环求和：
```
#!/bin/bash

i=1

sum=0

until [ $i -gt 100 ];do

	let sum+=$i

	let i++

done

echo "sum is:$sum"
```
###使用while循环求和：
```
#!/bin/bash

i=1

sum=0

while [ $i -le 100 ];do

	let sum+=$i

	let i++

done

echo "sum is:$sum"
```


##求100以内的偶数之和

###使用for循环求和：
```
#!/bin/bash

i=0

sum=0

for i in `seq 100` ;do

    	if [ $[$i%2] -eq 1 ];then

		continue

	fi	

	let sum+=$i

done

echo "sum is:$sum"
```
###使用while循环求和：
```
#!/bin/bash

i=0

sum=0

while [ $i -le 100 ];do

	let i++

	if [ $[$i%2] -eq 1 ];then

		continue

	fi

	let sum+=$i

done

echo "sum is: $sum"
```
###使用until循环求和：
```
#!/bin/bash

i=0

sum=0

until [ $i -gt 100 ];do

	let i++

	if [ $[ $i%2 ] -eq 1 ];then

		continue

	fi

	let sum+=$i

done

echo "sum is: $sum"
```

##编写一个九九乘法表

###使用for循环：
```
#!/bin/bash

#for i in `seq 9`;do

for ((j=1;j<=9;j++));do

	for ((i=1;i<=j;i++));do

		echo -ne "$i*$j=$(($i*$j))\t"

	done

	echo

done
```
###使用while循环：
```
#!/bin/bash

i=1

j=1

while[ $j -le 9 ];do

	while [ $i -le $j ];do

		echo -ne "$i*$j=$(($i*$j))\t"

		let i++

	done

	echo

	let i=1

	let j++

done
```
###使用until循环：
```
#!/bin/bash

i=1

j=1

until [ $j -gt 9 ];do

	until [ $i -gt $j ];do

		echo -ne "$i*$j=$(($i*$j))\t"

		let i++

	done

	echo

	let i=1

	let j++

done
```


##通过脚本判断用户是否登入系统，如果没有，则每10秒循环一次

###使用while循环：
```
#!/bin/bash

read -p "pls input a username: " username

while ! `who |grep "^$username" &> /dev/null`;do

	sleep 10

done

echo "`date +%F-%H:%M:%S` $username logged on">>/tmp/user.log

```

##使用case循环来获取系统信息
```
#!/bin/bash

cat <<EOF

1) show cpu information;

2) show memory information;

3) show disk information;

4) quit

EOF



cpu_info(){

	lscpu

	}

mem_info(){

	cat /proc/meminfo

	}

disk_info(){

	fdisk -l

	}

quit(){

	echo "quit"

	exit 0

	}	

read -p "pls input a num: " num

if [ $num -ne 1 -a $num -ne 2 -a $num -ne 3 -a $num -ne 4 ];then 

	read -p "pls input a num again: " num

fi



case "$num" in 

1) 

	cpu_info

	;;

2)

	mem_info

	;;

3)

	disk_info

	;;

4)

	quit

esac
```
