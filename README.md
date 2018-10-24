# one-liners
Just a collection of usefull one-liners, often a bit too long to remember


## awk

### Get column by its name
Pretty useful for big tables ([source](https://stackoverflow.com/a/24118223/6554591)):

```
awk -F'\t' -v c='colname' 'NR==1{for (i=1; i<=NF; i++) if ($i==c){p=i; break}; next} {print $p}' myfile.tsv
```

## BASH

### Complex sorting

```
sort -k1,1n -k 2,2 -k5,5gr myfile.tsv
```
> Sort first based on number on column 1, then standard (alphabetic) sorting of column 2, and finally do "general numeric sort" in reverse order of column 5 (i.e. recognises scientific notation and sorts high to low).
