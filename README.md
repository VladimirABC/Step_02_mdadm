#######

На основе Vagrant файла разворачивается VM со следующим набором дисков
==
sda         8:0    0   40G  0 disk   
`-sda1      8:1    0   40G  0 part   /
sdb         8:16   0  250M  0 disk   
sdc         8:32   0  250M  0 disk   
sdd         8:48   0  250M  0 disk   
sde         8:64   0  250M  0 disk   
sdf         8:80   0  250M  0 disk   
==
Из которых изначально рабочий только sda1 

В секции postinstall 
1. В систему устанавливаются дополнительные пакеты
yum install -y mdadm smartmontools hdparm gdisk

2. Создаётся RAID Level 10 /dev/md0  из 4-х дисков /dev/sd{b,c,d,e}

3. Созданный том маркируется GPT меткой и создаются 5 разделов с EXT4 FS
Все созданные разделы  присоединяются к системе.
===
/dev/md0p1       91M  1.6M   83M   2% /raid/part1
/dev/md0p2       92M  1.6M   84M   2% /raid/part2
/dev/md0p3       93M  1.6M   85M   2% /raid/part3
/dev/md0p4       92M  1.6M   84M   2% /raid/part4
/dev/md0p5       91M  1.6M   83M   2% /raid/part5
===

#########
