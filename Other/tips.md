

- kill grep 

```
ps -ef | grep artisan | grep -v grep|awk -F " " '{printf $2"\n"}'|xargs kill -9

```