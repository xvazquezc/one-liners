# one-liners
Just a collection of usefull one-liners, often a bit too long to remember


## awk

### Get column by its name
Pretty useful for big tables ([source](https://stackoverflow.com/a/24118223/6554591)):

```bash
awk -F'\t' -v c='colname' 'NR==1{for (i=1; i<=NF; i++) if ($i==c){p=i; break}; next} {print $p}' myfile.tsv
```

### Extract fasta sequences by name
[Source](https://stackoverflow.com/a/49737831/6554591).
```bash
awk -F'>' 'NR==FNR{ids[$0]; next} NF>1{f=($2 in ids)} f' ids.txt myseqs.fasta
```
> Where `ids.txt` is a list of the names of the sequences to extract from `myseqs.fasta`

### Remove empty fasta sequences
[Source](https://www.biostars.org/p/78786/#78849)
```bash
awk 'BEGIN {RS = ">" ; FS = "\n" ; ORS = ""} $2 {print ">"$0}' myseqs.fasta
```
> Useful to do any work from the exported amino acid gene calls from `anvi-get-sequences-for-gene-calls` as it keeps the non-protein coding gene headers with no sequence.

### Sum values based on category of another column
This will add up the values of column 2, giving the total sum for each unique value in column 1 ([source](https://unix.stackexchange.com/a/242972)).
```bash
awk -F "\t" '{a[$1] += $2; OFS="\t"} END {for (i in a) print i, a[i]}' myfile.tsv
```

### Simplify fasta headers (remove anything after first space)
[Source](https://www.biostars.org/p/336428/#336431)
```bash
awk 'BEGIN{OFS=FS=" "}{if(/^>/){NF--}}{print $1}' myseqs.fasta
```
> Change the `OFS=FS=" "` to the character marking where you want to delete from.
> Convenient for cleaning fasta headers for phylo work.

This is another alternative that should work in most cases:
```bash
cut -f1 -d " " myseqs.fasta
```

## BASH

### Complex sorting

```bash
sort -k1,1n -k 2,2 -k5,5gr myfile.tsv
```
> Sort first based on number on column 1, then standard (alphabetic) sorting of column 2, and finally do "general numeric sort" in reverse order of column 5 (i.e. recognises scientific notation and sorts high to low).

## Other similar repos and resources

https://github.com/stephenturner/oneliners

https://devhints.io/
