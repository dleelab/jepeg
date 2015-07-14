##What's New?
**[04/29/2015]** A pre-compiled executable for JEPEG (v0.2.0) built under Linux is available now! Please see the updated output format.

**[07/22/2014]** A pre-compiled executable for JEPEG (v0.1.0) built under Linux is available now!

##Introduction

"JEPEG is a novel software which uses only summary statistics and correlation structures estimated from a reference popluation, to i) impute the summary statistics at unmeasured eQTLs and ii) test for the joint effect of measured and imputed all eQTLs affecting a gene function/expression on a phenotype. JEPEG is useful when i) the subject-level genotype is not available and ii) fast and accurate access to gene-based p-values, pooling all association signals of unmeasured as well as measured eQTLs/functional SNPs, is required. Notably, because JEPEG uses only correlation structure estimated from a reference panel, it can be used as-is to analyze summary data coming from large pedigree studies."

##Citing JEPEG

**_JEPEG: a summary statistics based tool for gene-level joint testing of functional variants_**, Donghyung Lee; Vernell S. Williamson; Tim B. Bigdeli; Brien P. Riley; Ayman H. Fanous; Vladimir I. Vladimirov; Silviu-Alin Bacanu; **_Bioinformatics_** (2014), [doi:10.1093/bioinformatics/btu816](http://bioinformatics.oxfordjournals.org/content/31/8/1176.long).

##Acknowledgement
**This work is supported by the National Institutes of Health with grants R25DA26119, R21MH100560 and R21AA022717.**

<img src="http://upload.wikimedia.org/wikipedia/commons/thumb/6/6a/US-NIH-NIDA-Logo.svg/440px-US-NIH-NIDA-Logo.svg.png" height="100px">
<img src="http://upload.wikimedia.org/wikipedia/commons/thumb/4/4d/US-NIH-NIMH-Logo.svg/280px-US-NIH-NIMH-Logo.svg.png" height="100px">
<img src="http://upload.wikimedia.org/wikipedia/commons/thumb/7/72/US-NIH-NIAAA-Logo.svg/440px-US-NIH-NIAAA-Logo.svg.png" height="100px">


##Download JEPEG
The current release (Version 0.2.0) of JEPEG is for a Linux user. The pre-compiled executables for other operating systems (e.g.,  Windows, MacOS) will be available soon. The latest source codes of JEPEG are available upon request (dustorm_at_gmail_dot_com)

|**Direct download link**|**Version**|**Release Date**|
|:---|:---|:---|
|[JEPEG for a Linux user](https://drive.google.com/file/d/0B8CSKKDoI0UmV1Y3YVpqWlloaWs/view?usp=sharing)|v0.2.0|04/29/2015|
   

##Download Reference Panels
|**Direct download link**|**Number of Samples**|**NCBI build**|**Release Date**|
|:---|:---|:---|:---|
|[1000 Genomes AFR Phase1 Release3](https://drive.google.com/file/d/0B8CSKKDoI0UmZDczT0w5OFVKSHc/edit?usp=sharing)|246|build 37 (hg19)|Nov. 23 2010|
|[1000 Genomes AMR Phase1 Release3](https://drive.google.com/file/d/0B8CSKKDoI0UmdVNlcUZFbVdFNVU/edit?usp=sharing)|181|build 37 (hg19)|Nov. 23 2010|
|[1000 Genomes ASN Phase1 Release3](https://drive.google.com/file/d/0B8CSKKDoI0UmRjdhVks2YjNVaGs/edit?usp=sharing)|286|build 37 (hg19)|Nov. 23 2010|
|[1000 Genomes EUR Phase1 Release3](https://drive.google.com/file/d/0B8CSKKDoI0UmQWF5MkRySDYyQjA/edit?usp=sharing)|379|build 37 (hg19)|Nov. 23 2010|
|[UK10K (ALSPAC and TWINSUK)]()|2432|build 37 (hg19)| |

##Download SNP Annotation Data

|**Direct download link**|**Version**|**Release Date**|
|:---|:---|:---|
|[SNP annotations](https://drive.google.com/file/d/0B8CSKKDoI0UmNVdNenRPNmtYbkk/view?usp=sharing)|v0.2.0|11/20/2014|
|[SNP annotations](https://drive.google.com/file/d/0B8CSKKDoI0UmYjM1eUxMVWFiRGc/edit?usp=sharing SNP annotations)|v0.1.0      |07/22/2014|

##JEPEG input file format

JEPEG takes as input a plain text file with rows and columns denoting SNPs and variables, respectively. The first line of the input file should be column names/headers. Data entries on each line should be separated by white space. 


If your summary data set was generated based on non-imputed genotypic data and you want to impute the summary statistics of all unmeasured eQTLs based on an external reference panel (e.g. 1000 Genomes or UK10K) using DIST before JEPEG analysis, your input data must contains six columns (DIST input format): 1) rsid, 2) chromosome number, 3) base pair position, 4) reference allele, 5) alternative allele and 6) normally distributed GWAS/meta-analysis summary statistic (Z-score). JEPEG does not require the input data to be sorted in ascending order by chromosome number and base pair position or rsid. Here is a sample JEPEG input file, with 5 SNPs:

```
rsid        chr  bp         a1  a2   z

rs1000109   9    117908733  C   T   -0.714464

rs10001109  4    44904653   C   T    0.721919

rs1000112   22   28273339   C   G   -0.583666

rs10001127  4    130547376  T   C    0.069329

rs1000113   5    150240076  T   C   -1.447288
```

If your input data is generated on the basis of already imputed genotype data by using genotype imputation methods such as IMPUTE2, MACH, BEAGLE, etc., you may not want to impute your data again by using DIST. You can run JEPEG without DIST imputation. In this case, you must add one more column for imputation information (info) in your input data. Here is a sample input file for this case, with 5 SNPs:

```
rsid        chr  bp         a1  a2   z         info 

rs1000109   9    117908733  C   T   -0.714464  0.998

rs10001109  4    44904653   C   T    0.721919  0.731

rs1000112   22   28273339   C   G   -0.583666  0.445

rs10001127  4    130547376  T   C    0.069329  0.899

rs1000113   5    150240076  T   C   -1.447288  1
```

  
**Note:** If the input data comes from a different genome assembly (e.g. NCBI build 36 (hg18)) than NCBI build 37 (hg19), it must be converted to NCBI build 37 (hg19) using a software, called [liftover](https://genome.ucsc.edu/cgi-bin/hgLiftOver), from UCSC.   


##JEPEG output file format

The JEPEG output file has nine columns: 1)  gene name (geneid), 2) chi-square test statistic value (chisq), 3) degrees of freedom (df), 4) JEPEG p-value (jepeg_pval), 5) number of functional SNPs associated with gene (num_snp), 6) top functional category (top_categ), 7) top category p-value (top_categ_pval), 8) top functional SNP ID (top_snp) and 9) top SNP p-value (top_snp_pval). The first line of the output file is column names/headers.  Here is a sample JEPEG output file, with 5 genes:

```
geneid    chisq    df  jepeg_pval   num_snp   top_categ   top_categ_pval   top_snp      top_snp_pval

FCGR3B    14.926   1   1.80E-05     2         PFS         1.10E-04         rs5030738    5.08E-05
 
CSPG4P2Y  14.774   2   3.29E-05     5         TRN         1.21E-04         rs10828664   5.55E-05
		
SLC7A7    19.902   3   3.40E-05     33        TRN         3.51E-04         rs9304810    1.07E-03

EDARADD   13.957   2   3.93E-05     2         PFS         1.86E-04         rs966365     7.80E-06
 
FAM71D    13.026   1   4.34E-05     26        TAR         3.07E-04         rs45515505   1.53E-04
```


##Options

|**Option**|**Short Flag**|**Parameter**|**Default**|**Description**|
|:---|:---|:---|:---|:---|
|--version|-v|none|none|Prints version information.|
|--help|-h|none|none|Outputs a full description of all JEPEG options.|
|--impute|none|none|none|Imputes summary statistics of unmeasured functional SNPs using DIST before JEPEG analysis.|
|--reference|-r|filename|none|The filename of the reference population data.|
|--referenceIndex|-i|filename|none|The filename of the reference population index data.|
|--annotation|-a|filename|none|The filename of the SNP annotation data set.|
|--output|-o|filename|out.jepeg|The filename of JEPEG output|
|--windowSize|-n|decimal|1.0|The size of the DIST prediction window (Mb).|
|--wingSize|-m|decimal|0.5|The size of the wing padded on the left and right of the DIST prediction window (Mb).|
|--impInfoCutoff|none|decimal|0.3|The imputation information cutoff.|

##Getting started with examples

The users are required to download a pre-compiled JEPEG executable (jepeg) and a sample input file (sample.pgc1.scz.txt) from the **Download JEPEG** section above. The SNP annotation data set should be downloaded from **Download SNP annotation data** section above. A tgz-compressed directory with 1000 Genomes or UK10K reference panel datasets also should be downloaded and can be uncompressed using **tar** with the **-zxvf** options. Let’s assume that the reference panel data file and its index file named as "1kg.eur.geno.gz" and "1kg.eur.index.gz" respectively are stored in a directory /path/to/reference/ and the annotation dataset named as "jepeg.snp.annotations.v0.2.0.txt" are stored in a directory /path/to/annotation/. 


**Scenario 1:** Let's assume that we want to conduct JEPEG analysis after imputing unmeasured functional SNPs in our input data using DIST and then store all JEPEG results in a text file named as "jepeg.pgc1.scz.output.txt". The following command can be used for this scenario.

```shell
>> ./jepeg --impute sample.pgc1.scz.txt -o jepeg.pgc1.scz.output.txt -i /path/to/reference/1kg.eur.index.gz -r /path/to/reference/1kg.eur.geno.gz -a /path/to/annotation/jepeg.snp.annotations.v0.2.0.txt
```

Here, we didn't set the size of the prediction window and wing by using options "--windowSize" and "--wingSize", so JEPEG will use the default size (1 Mb for the DIST prediction window and 0.5 Mb for the wing).


**Scenario 2:** Here, we want to set **the size of the DIST prediction window (--windowSize or -n)** to be 0.6 Mb and **the size of the wing padded each side of the prediction window (--wingSize or -m)** to be 0.2 Mb. For this scenario, we can use the following command.

```shell
>> ./jepeg -o jepeg.pgc1.scz.output.txt -i /path/to/reference/1kg.eur.index.gz sample.pgc1.scz.txt -r /path/to/reference/1kg.eur.geno.gz --impute -a /path/to/annotation/jepeg.snp.annotations.v0.2.0.txt -n 0.6 -m 0.2
```
 
**Scenario 3:** Let's assume that our input data (summary statistics) are generated from genotype data already imputed by IMPUTE2 using 1000 Genomes European panel so we don't want to impute our input using DIST. By removing "--impute" option from the command, we can skip DIST imputation.

```shell
>> ./jepeg sample.input.txt -o sample.jepeg.output.txt -i /path/to/reference/1kg.eur.index.gz  -r /path/to/reference/1kg.eur.geno.gz -a /path/to/annotation/jepeg.snp.annotations.v0.2.0.txt 
```
