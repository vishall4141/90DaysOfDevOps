task-1  Check running processes

vish@DESKTOP-05GB0:~$ ps aux | head -n 5
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root           1  0.2  0.1  21896 13280 ?        Ss   08:59   0:01 /sbin/init
root           2  0.0  0.0   3180  2204 hvc0     Sl+  08:59   0:00 /init
root           7  0.0  0.0   3196  2124 hvc0     Sl+  08:59   0:00 plan9 --control-socket 7 --log-level 4 --server-fd 8 --pipe-fd 10 --log-truncate
root          56  0.0  0.2  50460 16276 ?        S<s  08:59   0:00 /usr/lib/systemd/systemd-journald

ps aux lists every process. PID 1 is the first process the kernel starts. Names in [brackets] are kernel threads.

vish@DESKTOP-05GB0:~$ ps aux | grep nginx
root         277  0.0  0.0  11172  1808 ?        Ss   08:59   0:00 nginx: master process /usr/sbin/nginx -g daemon on; master_process on;
www-data     279  0.0  0.0  12896  4516 ?        S    08:59   0:00 nginx: worker process
www-data     280  0.0  0.0  12896  4516 ?        S    08:59   0:00 nginx: worker process
www-data     281  0.0  0.0  12896  4516 ?        S    08:59   0:00 nginx: worker process
www-data     282  0.0  0.0  12896  4484 ?        S    08:59   0:00 nginx: worker process
www-data     283  0.0  0.0  12896  4492 ?        S    08:59   0:00 nginx: worker process
www-data     284  0.0  0.0  12896  4516 ?        S    08:59   0:00 nginx: worker process
www-data     285  0.0  0.0  12896  4516 ?        S    08:59   0:00 nginx: worker process
www-data     290  0.0  0.0  12896  4516 ?        S    08:59   0:00 nginx: worker process
www-data     293  0.0  0.0  12896  4516 ?        S    08:59   0:00 nginx: worker process
www-data     294  0.0  0.0  12896  4516 ?        S    08:59   0:00 nginx: worker process
www-data     295  0.0  0.0  12896  4516 ?        S    08:59   0:00 nginx: worker process
www-data     296  0.0  0.0  12896  4516 ?        S    08:59   0:00 nginx: worker process
www-data     297  0.0  0.0  12896  4516 ?        S    08:59   0:00 nginx: worker process
www-data     299  0.0  0.0  12896  4516 ?        S    08:59   0:00 nginx: worker process
www-data     301  0.0  0.0  12896  4516 ?        S    08:59   0:00 nginx: worker process
www-data     302  0.0  0.0  12896  4452 ?        S    08:59   0:00 nginx: worker process
vishal       825  0.0  0.0   4100  2092 pts/0    S+   09:03   0:00 grep --color=auto nginx

In the context of checking processes, grep acts as a text filter that strips away everything except the specific process you are looking for

vish@DESKTOP-05GB0:~/script$ free -h
               total        used        free      shared  buff/cache   available
Mem:           7.5Gi       594Mi       6.8Gi       3.9Mi       250Mi       6.9Gi
Swap:          2.0Gi          0B       2.0Gi

