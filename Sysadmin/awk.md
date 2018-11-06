# AWK

## Print Column – Change Field Separator – Linux Bash

The **awk** is a powerful Linux command line tool, that can process the input data as columns.
In the following note i will show how to print columns by numbers – first, second, last, multiple columns etc.
I will show how to change the default field separator in **awk**.
At the end of this article i will also show how to print or exclude specific columns or even ranges of columns using **awk**.

## Awk Internal Variables and Expanded Format
Awk uses some internal variables to assign certain pieces of information as it processes a file.

The internal variables that awk uses are:

- **FILENAME**: References the current input file.
- **FNR**: References the number of the current record relative to the current input file. For instance, if you have two input files, this would tell you the record number of each file instead of as a total.
- **FS**: The current field separator used to denote each field in a record. By default, this is set to whitespace.
- **NF**: The number of fields in the current record.
- **NR**: The number of the current record.
- **OFS**: The field separator for the outputted data. By default, this is set to whitespace.
- **ORS**: The record separator for the outputted data. By default, this is a newline character.
- **RS**: The record separator used to distinguish separate records in the input file. By default, this is a newline character.
## Awk: Print Columns by Number
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

```bash
awk 'BEGIN { FS=":"; } { print $1; }' /etc/passwd
```