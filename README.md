# one-liners
Just a collection of usefull one-liners, often a bit too long to remember


## awk

### Get column by its name
Pretty useful for big tables ([source](https://stackoverflow.com/a/24118223/6554591)):

```
awk -F'\t' -v c='colname' 'NR==1{for (i=1; i<=NF; i++) if ($i==c){p=i; break}; next} {print $p}' myfile.tsv
```
