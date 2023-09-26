
# TROP : Tandem Repeat Overlap Parser

from a nanopore flongle run
memory

The script requires the ```.dat``` file produced by TRF. 

Here, we use the example file indicated further above
NA_all.fasta.2.5.7.80.10.50.2000.dat


# Prerequisites
**1) Running TRF to produce a ```.dat``` file**

For the present tutorial, TRF was run with the following options on a fasta file of R9.4 nanopore reads (fasta file ```NA_all.fasta``` not provided)

```trf NA_all.fasta 2 5 7 80 10 50 2000```, which produces ```NA_all.fasta.2.5.7.80.10.50.2000.dat``` for later parsing by TROP

Please visit TRF's github repository for further information on TRF installation and running options (https://github.com/Benson-Genomics-Lab/TRF)

**2) Preparing a tabulated sequence length file**

There are a number of ways this can be done, for instance, you could use the awk command below (one-liner) on linux platform with the raw fasta reads:

```
awk '/^>/{if (l!="") print l; print; l=0; next}{l+=length($0)}END{print l}' NA_all.fasta | cut -d ' ' -f 1 | paste - - | sed -r 's/^>//g' > NA_all_tabulated_lengths.txt
```

Note that here, we split the nanopore sequence title to only keep the main identifier. The resulting tabulated file should be as below to be processed by TROP
(The first column is the sequence name, second column is the sequence length in bp)

```
80800063-c64b-4493-a80c-6e2c6bfbe01a	823
a9fc5d29-acd8-4858-81c0-5cf6434708c0	894
66c1ef31-ac67-447a-ad27-4fdb74f47c74	2845
9cbcb1ea-5ae0-4333-a6f6-fcca75430742	3096
12ede4c6-f934-4566-bdd3-dc0e8efa004b	4402
3fa38391-78fc-47de-927d-1b806dc12ac9	456
7a5fe376-fa8b-4552-8803-04015cab89bd	2961
...
```

# Running TROP

**1) Open R and set your working directory**
```
setwd("C:/Users/tomsauv/my_R_analyses")
``` 
Place all files necessary in this folder on your computer (above is an example, adjust to the folder path on your computer)

**2) Load the ```data.table```  R package (install it prior)**
```
require(data.table)
```

**3) Load the script (after you download it from this repository and place it your working directory)**
```
source("trop.r")
```

**4) Run the script by filling the name of files to be parsed as below**

trop


**X) Load the above ```.dat``` file with R function ```scan```**
```
mydf <- scan("NA_all.fasta.2.5.7.80.10.50.2000.dat", what = "", sep = "\n")
```



# How to cite TROP

Sauvage T, Cormic A, Passerini D. A comparison of Oxford nanopore library strategies for bacterial genomics. BMC Genomics. 2023 xxxxxxxxxx

or directly

Sauvage T. TROP : Tandem Repeat Overlap Parser. https://github.com/tomsauv/TROP-Tandem-Repeat-Overlap-Parser. Accessed September XX, 2023. DOI XXXXXXXXXXXXXXXXXXX

# Additional references

Benson G. Tandem Repeats Finder: a program to analyze DNA sequences. Nucleic Acids Res. 1999; 27(2):573–580. doi:10.1093/nar/27.2.573
