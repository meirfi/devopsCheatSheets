# AWK

## Print Column – Change Field Separator – Linux Bash

The **awk** is a powerful Linux command line tool, that can process the input data as columns.

In the following note i will show how to print columns by numbers – first, second, last, multiple columns etc.

I will show how to change the default field separator in **awk**.

At the end of this article i will also show how to print or exclude specific columns or even ranges of columns using **awk**.

##AWK: Print Columns by Number
Print the all columns:
```bash
$ awk '{print $0}' FILE
```
Print the first column:
```bash
$ awk '{print $1}' FILE
```
Print the second column:
```bash
$ awk '{print $2}' FILE
```
Print the last column:
```bash
$ awk '{print $NF}' FILE
```
Print multiple columns (the first and the third columns):
```bash
$ awk '{print $1 $3}' FILE
```