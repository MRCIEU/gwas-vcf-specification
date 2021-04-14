# The Variant Call Format Summary Statistics Specification v1.2

## Rationale

Specifying a format to store GWAS summary data is necessary to aid with data sharing and tool development. Using the VCF format can fulfill the following requirements

- It uses a pre-existing, well known and well defined format
- Aligning against the reference genome and handling various difficulties such as indels, build differences and multi-allelic variants has been solved by the htslib library.
- Many tools exist that can be used for manipulation
- The file format is relatively small
- Indexing makes looking up by chromosome and position extremely fast
- Indexing time is very fast
- We can treat each GWAS as a distinct unit rather than storing everything in a database which is less nimble
- We can store multiple traits from a GWAS (e.g., multi-trait GWAS or eQTL analysis) in a single file by using one sample column for each trait/gene
- It is easy to export the data into other tabular formats
- Initial tests indicate it could translate directly to distributed databases that sit on top of vcf e.g <https://github.com/GenomicsDB/GenomicsDB>

## Existing tools

- [gwas2vcf](https://github.com/mrcieu/gwas2vcf) - open source software to convert plain text GWAS summary statistics to VCF
- [gwas2vcfweb](https://github.com/mrcieu/gwas2vcfweb) - open source front/back-end for gwas2vcf running at <http://vcf.mrcieu.ac.uk/>
- [bcftools](https://samtools.github.io/bcftools/bcftools.html) - can be used to manipulate, align with genome references, query, as it is in standard vcf format
- [R/gwasvcf](https://github.com/MRCIEU/gwasvcf) - wrapper around [bioconductor/VariantAnnotation](https://bioconductor.org/packages/release/bioc/html/VariantAnnotation.html) package for performing natural GWAS queries in R. Includes LD proxy functionality
- [pygwasvcftools](https://github.com/MRCIEU/pygwasvcf) - wrapper around [pysam](https://pysam.readthedocs.io/en/latest/index.html) package for performing natural GWAS queries in python
- [R/TwoSampleMR](https://github.com/MRCIEU/TwoSampleMR/) - can use GWAS vcf files directly for summary data based Mendelian randomization analysis
- [ldsc](https://github.com/explodecomputer/ldsc) - a fork of the LD score regression programme that allows reading in data directly from GWAS vcf format.

## Guides

- [Basic file manipulation](https://github.com/mrcieu/gwas2vcf#working-with-gwas-vcf)
- [Analytical workflows](https://mrcieu.github.io/gwasglue/)

## 1. The VCF specification

The VCF format specification is available from [hts-specs](https://samtools.github.io/hts-specs/VCFv4.2.pdf).

### 1.1 VCF example storing GWAS summary statistics

A broad overview:

- the **header** describes the harmonisation, study and trait(s) in the file.
- each row of the **body** contains information about a variant
  - variant information (e.g. chromosome, id, position, alleles, annotations) are represented in the first few columns
  - the **sample** section (which would normally represent the genotype information of one column per individual) is used to store variant-trait association summary statistics data. Each sample column represents one trait.

#### 1.1.1 Header

The VCF header contains metadata describing the study, trait(s), genome build and other information. It also defines fields found in the body including the format for the trait field(s) which contain the variant-trait association summary statistics data.

An example is given below. It has the following main meta data sections:

- INFO - describes the annotations included for the variants
- FORMAT - describes the fields included for the variant-trait association summary statistics (e.g. ES = effect size etc)
- study - describes metadata about the study i.e. publication
- trait - describes metadata about the trait i.e. phenotype that is tested for association with the variant
- contig - descriptions of the chromosomes
- bcftools - list of commands used to create the file

```text
##fileformat=VCFv4.2
##fileurl=https://github.com/MRCIEU/gwas-vcf-specification/blob/master/example.vcf.txt
##filedate="07/09/2020"
##gwasformat=GWAS-VCFv1.2
##source=Gwas2VCFv1.2.0
##reference=ftp://ftp.broadinstitute.org/bundle/b37/human_g1k_v37.fasta.gz
##contig=<ID=1,length=249250621,assembly=GRCh37.p13>
##contig=<ID=2,length=243199373,assembly=GRCh37.p13>
##contig=<ID=3,length=198022430,assembly=GRCh37.p13>
##contig=<ID=4,length=191154276,assembly=GRCh37.p13>
##contig=<ID=5,length=180915260,assembly=GRCh37.p13>
##contig=<ID=6,length=171115067,assembly=GRCh37.p13>
##contig=<ID=7,length=159138663,assembly=GRCh37.p13>
##contig=<ID=8,length=146364022,assembly=GRCh37.p13>
##contig=<ID=9,length=141213431,assembly=GRCh37.p13>
##contig=<ID=10,length=135534747,assembly=GRCh37.p13>
##contig=<ID=11,length=135006516,assembly=GRCh37.p13>
##contig=<ID=12,length=133851895,assembly=GRCh37.p13>
##contig=<ID=13,length=115169878,assembly=GRCh37.p13>
##contig=<ID=14,length=107349540,assembly=GRCh37.p13>
##contig=<ID=15,length=102531392,assembly=GRCh37.p13>
##contig=<ID=16,length=90354753,assembly=GRCh37.p13>
##contig=<ID=17,length=81195210,assembly=GRCh37.p13>
##contig=<ID=18,length=78077248,assembly=GRCh37.p13>
##contig=<ID=19,length=59128983,assembly=GRCh37.p13>
##contig=<ID=20,length=63025520,assembly=GRCh37.p13>
##contig=<ID=21,length=48129895,assembly=GRCh37.p13>
##contig=<ID=22,length=51304566,assembly=GRCh37.p13>
##contig=<ID=X,length=155270560,assembly=GRCh37.p13>
##contig=<ID=Y,length=59373566,assembly=GRCh37.p13>
##FILTER=<ID=PASS,Description="All filters passed">
##INFO=<ID=RSID,Number=1,Type=String,Description="dbSNP identifier",Source="https://ftp.ncbi.nih.gov/snp/latest_release/VCF/GCF_000001405.25.gz",Version="153">
##FORMAT=<ID=NS,Number=A,Type=Float,Description="Variant-specific number of samples/individuals with called genotypes used to test association with specified trait">
##FORMAT=<ID=EZ,Number=A,Type=Float,Description="Z-score provided if it was used to derive the ES and SE fields">
##FORMAT=<ID=SI,Number=A,Type=Float,Description="Accuracy score of summary association statistics imputation">
##FORMAT=<ID=NC,Number=A,Type=Float,Description="Variant-specific number of cases used to estimate genetic effect (binary traits only)">
##FORMAT=<ID=ES,Number=A,Type=Float,Description="Effect size estimate relative to the alternative allele">
##FORMAT=<ID=SE,Number=A,Type=Float,Description="Standard error of effect size estimate">
##FORMAT=<ID=LP,Number=A,Type=Float,Description="-log10 p-value for effect estimate">
##FORMAT=<ID=AF,Number=A,Type=Float,Description="Alternative allele frequency in trait subset">
##FORMAT=<ID=AC,Number=A,Type=Float,Description="Alternative allele count in the trait subset">
##study=<ID="PMID:12345678",Source="PubMed">
##trait=<ID=EFO0004340,Description="Body mass index",Source="EFO",Version="3.14.0",Type="continuous",Test="linear",Unit="SD",Population="European",TotalSamples=461460,TotalVariants=9851866,VariantsNotRead=0,HarmonisedVariants=9851866,VariantsNotHarmonised=0,SwitchedAlleles=9851866,FileUrl="https://gwas.mrcieu.ac.uk/files/ukb-b-19953/ukb-b-19953.vcf.gz",FileDate="24/04/2020">
##trait=<ID=EFO0001360,Description="type II diabetes mellitus",Source="EFO",Version="3.14.0",Type="binary",Test="logistic",Population="European",TotalSamples=462933,TotalCases=2972,TotalVariants=9851866,VariantsNotRead=0,HarmonisedVariants=9851866,VariantsNotHarmonised=0,SwitchedAlleles=9851866,FileUrl="https://gwas.mrcieu.ac.uk/files/ukb-b-13806/ukb-b-13806.vcf.gz",FileDate="24/04/2020">
```

#### 1.1.2 Body

| #CHROM | POS    | ID | REF | ALT | QUAL | FILTER | INFO            | FORMAT               | EFO0004340                                                | EFO0001360                                                   |
|--------|--------|----|-----|-----|------|--------|-----------------|----------------------|-----------------------------------------------------------|--------------------------------------------------------------|
| 1      | 49298  | .  | T   | C   | .    | PASS   | RSID=rs10399793 | NS:NC:ES:SE:LP:AF:AC | 463005:0:0.00103892:0.0034984:0.113509:0.613764:568351    | 463005:2972:9.098e-05:0.000294716:0.119186:0.613764:568351   |
| 1      | 49298  | .  | T   | A   | .    | PASS   | RSID=rs10399793 | NS:NC:ES:SE:LP:AF:AC | 463005:0:0.00214602:0.00346583:0.267606:0.011:4630        | 463005:2972:0.000102689:0.00029197:0.136677:0.012:4630       |
| 1      | 91536  | .  | GTC | G   | .    | PASS   | RSID=rs6702460  | NS:NC:ES:SE:LP:AF:AC | 463005:0:0.00410514:0.0034125:0.638272:0.456845:423042    | 463005:2972:0.000329732:0.000287485:0.60206:0.456851:423042  |
| 1      | 534192 | .  | C   | T   | .    | PASS   | RSID=rs6680723  | NS:NC:ES:SE:LP:AF:AC | 463005:0:0.000334321:0.0038979:0.0315171:0.24094:223131   | 463005:2972:0.000106473:0.000328379:0.124939:0.24096:223131  |
| 1      | 706368 | .  | A   | AAA | .    | PASS   | RSID=rs12029736 | NS:NC:ES:SE:LP:AF:AC | 463005:0:-0.00030371:0.00241981:0.0457575:0.515705:477487 | 463005:2972:7.16085e-06:0.000203854:0.0132283:0.51565:477487 |

The first row represents a biallelic variant (rs10399793). The reference allele (T) is always the non-effect allele and must match the reference genome sequence. The alternative allele (C) is always the effect allele and often (but not always) the minor allele. The final column contains the effect size (ES), standard error (SE), P value on -log10 scale (LP), study allele frequency (AF) and sample size (NS). Some fields are optional others required, refer to the header and section 2 (below) for details.

## 2. Reserved keys

| Field | Description                                                                                                          | Required |
|-------|----------------------------------------------------------------------------------------------------------------------|----------|
| NS    | Variant-specific number of samples/individuals with called genotypes used   to test association with specified trait | FALSE    |
| EZ    | Z-score provided if it was used to derive the ES and SE fields                                                       | FALSE    |
| SI    | Accuracy score of association statistics imputation                                                                  | FALSE    |
| NC    | Variant-specific number of cases used to estimate genetic effect (binary   traits only)                              | FALSE    |
| ES   | Effect size estimate relative to the alternative allele                                                              | TRUE     |
| SE   | Standard error of effect size estimate                                                                               | TRUE     |
| LP   | -log10 p-value for effect estimate                                                                                   | TRUE     |
| AF    | Alternative allele frequency in trait subset                                                                         | FALSE    |
| AC    | Alternative allele count in the trait subset                                                                         | FALSE    |

## 3. Multi-allelic variants

Genomic positions with more than one variant should be stored on individual rows as shown above (rs10399793)

## Citation

```
Lyon, M.S., Andrews, S.J., Elsworth, B. et al. The variant call format provides efficient and robust storage of GWAS summary statistics. Genome Biol 22, 32 (2021). https://doi.org/10.1186/s13059-020-02248-0
```

```
The Variant Call Format (VCF) Version 4.2 Specification. (2020).
Available from: https://samtools.github.io/hts-specs/VCFv4.2.pdf
```
