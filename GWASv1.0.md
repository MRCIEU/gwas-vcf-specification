### The Variant Call Format (VCF) Genome-wide Association Study (GWAS) Summary Statistics Specification v1.0

#### 1. The VCF specification

The VCF format will not be covered here. Refer to [hts-specs](https://samtools.github.io/hts-specs/VCFv4.2.pdf) for the VCF v4.2 specification.

##### 1.1 VCF example storing GWAS summary statistics

###### 1.1.1 Header

The VCF header defines fields found in the body including META fields which contain information about the GWAS study.

```
##fileformat=VCFv4.2
##FILTER=<ID=PASS,Description="All filters passed">
##INFO=<ID=AF,Number=A,Type=Float,Description="Allele Frequency">
##FORMAT=<ID=ES,Number=A,Type=Float,Description="Effect size estimate relative to the alternative allele">
##FORMAT=<ID=SE,Number=A,Type=Float,Description="Standard error of effect size estimate">
##FORMAT=<ID=LP,Number=A,Type=Float,Description="-log10 p-value for effect estimate">
##FORMAT=<ID=AF,Number=A,Type=Float,Description="Alternate allele frequency in the association study">
##FORMAT=<ID=SS,Number=A,Type=Float,Description="Sample size used to estimate genetic effect">
##FORMAT=<ID=EZ,Number=A,Type=Float,Description="Z-score provided if it was used to derive the EFFECT and SE fields">
##FORMAT=<ID=SI,Number=A,Type=Float,Description="Accuracy score of summary data imputation">
##FORMAT=<ID=NC,Number=A,Type=Float,Description="Number of cases used to estimate genetic effect">
##FORMAT=<ID=ID,Number=1,Type=String,Description="Study variant identifier">
##META=<ID=TotalVariants,Number=1,Type=Integer,Description="Total number of variants in input">
##META=<ID=VariantsNotRead,Number=1,Type=Integer,Description="Number of variants that could not be read">
##META=<ID=HarmonisedVariants,Number=1,Type=Integer,Description="Total number of harmonised variants">
##META=<ID=VariantsNotHarmonised,Number=1,Type=Integer,Description="Total number of variants that could not be harmonised">
##META=<ID=SwitchedAlleles,Number=1,Type=Integer,Description="Total number of variants strand switched">
##META=<ID=TotalControls,Number=1,Type=Integer,Description="Total number of controls in the association study">
##META=<ID=TotalCases,Number=1,Type=Integer,Description="Total number of cases in the association study">
##META=<ID=StudyType,Number=1,Type=String,Description="Type of GWAS study [Continuous or CaseControl]">
##SAMPLE=<ID=IEU-b-1,TotalVariants=9851866,VariantsNotRead=0,HarmonisedVariants=9851866,VariantsNotHarmonised=0,SwitchedAlleles=9851866,StudyType=Continuous>
##contig=<ID=1,length=249250621,assembly=HG19/GRCh37>
##contig=<ID=2,length=243199373,assembly=HG19/GRCh37>
##contig=<ID=3,length=198022430,assembly=HG19/GRCh37>
##contig=<ID=4,length=191154276,assembly=HG19/GRCh37>
##contig=<ID=5,length=180915260,assembly=HG19/GRCh37>
##contig=<ID=6,length=171115067,assembly=HG19/GRCh37>
##contig=<ID=7,length=159138663,assembly=HG19/GRCh37>
##contig=<ID=8,length=146364022,assembly=HG19/GRCh37>
##contig=<ID=9,length=141213431,assembly=HG19/GRCh37>
##contig=<ID=10,length=135534747,assembly=HG19/GRCh37>
##contig=<ID=11,length=135006516,assembly=HG19/GRCh37>
##contig=<ID=12,length=133851895,assembly=HG19/GRCh37>
##contig=<ID=13,length=115169878,assembly=HG19/GRCh37>
##contig=<ID=14,length=107349540,assembly=HG19/GRCh37>
##contig=<ID=15,length=102531392,assembly=HG19/GRCh37>
##contig=<ID=16,length=90354753,assembly=HG19/GRCh37>
##contig=<ID=17,length=81195210,assembly=HG19/GRCh37>
##contig=<ID=18,length=78077248,assembly=HG19/GRCh37>
##contig=<ID=19,length=59128983,assembly=HG19/GRCh37>
##contig=<ID=20,length=63025520,assembly=HG19/GRCh37>
##contig=<ID=21,length=48129895,assembly=HG19/GRCh37>
##contig=<ID=22,length=51304566,assembly=HG19/GRCh37>
##contig=<ID=X,length=155270560,assembly=HG19/GRCh37>
##contig=<ID=Y,length=59373566,assembly=HG19/GRCh37>
##contig=<ID=MT,length=16569,assembly=HG19/GRCh37>
##contig=<ID=GL000207.1,length=4262,assembly=HG19/GRCh37>
##contig=<ID=GL000226.1,length=15008,assembly=HG19/GRCh37>
##contig=<ID=GL000229.1,length=19913,assembly=HG19/GRCh37>
##contig=<ID=GL000231.1,length=27386,assembly=HG19/GRCh37>
##contig=<ID=GL000210.1,length=27682,assembly=HG19/GRCh37>
##contig=<ID=GL000239.1,length=33824,assembly=HG19/GRCh37>
##contig=<ID=GL000235.1,length=34474,assembly=HG19/GRCh37>
##contig=<ID=GL000201.1,length=36148,assembly=HG19/GRCh37>
##contig=<ID=GL000247.1,length=36422,assembly=HG19/GRCh37>
##contig=<ID=GL000245.1,length=36651,assembly=HG19/GRCh37>
##contig=<ID=GL000197.1,length=37175,assembly=HG19/GRCh37>
##contig=<ID=GL000203.1,length=37498,assembly=HG19/GRCh37>
##contig=<ID=GL000246.1,length=38154,assembly=HG19/GRCh37>
##contig=<ID=GL000249.1,length=38502,assembly=HG19/GRCh37>
##contig=<ID=GL000196.1,length=38914,assembly=HG19/GRCh37>
##contig=<ID=GL000248.1,length=39786,assembly=HG19/GRCh37>
##contig=<ID=GL000244.1,length=39929,assembly=HG19/GRCh37>
##contig=<ID=GL000238.1,length=39939,assembly=HG19/GRCh37>
##contig=<ID=GL000202.1,length=40103,assembly=HG19/GRCh37>
##contig=<ID=GL000234.1,length=40531,assembly=HG19/GRCh37>
##contig=<ID=GL000232.1,length=40652,assembly=HG19/GRCh37>
##contig=<ID=GL000206.1,length=41001,assembly=HG19/GRCh37>
##contig=<ID=GL000240.1,length=41933,assembly=HG19/GRCh37>
##contig=<ID=GL000236.1,length=41934,assembly=HG19/GRCh37>
##contig=<ID=GL000241.1,length=42152,assembly=HG19/GRCh37>
##contig=<ID=GL000243.1,length=43341,assembly=HG19/GRCh37>
##contig=<ID=GL000242.1,length=43523,assembly=HG19/GRCh37>
##contig=<ID=GL000230.1,length=43691,assembly=HG19/GRCh37>
##contig=<ID=GL000237.1,length=45867,assembly=HG19/GRCh37>
##contig=<ID=GL000233.1,length=45941,assembly=HG19/GRCh37>
##contig=<ID=GL000204.1,length=81310,assembly=HG19/GRCh37>
##contig=<ID=GL000198.1,length=90085,assembly=HG19/GRCh37>
##contig=<ID=GL000208.1,length=92689,assembly=HG19/GRCh37>
##contig=<ID=GL000191.1,length=106433,assembly=HG19/GRCh37>
##contig=<ID=GL000227.1,length=128374,assembly=HG19/GRCh37>
##contig=<ID=GL000228.1,length=129120,assembly=HG19/GRCh37>
##contig=<ID=GL000214.1,length=137718,assembly=HG19/GRCh37>
##contig=<ID=GL000221.1,length=155397,assembly=HG19/GRCh37>
##contig=<ID=GL000209.1,length=159169,assembly=HG19/GRCh37>
##contig=<ID=GL000218.1,length=161147,assembly=HG19/GRCh37>
##contig=<ID=GL000220.1,length=161802,assembly=HG19/GRCh37>
##contig=<ID=GL000213.1,length=164239,assembly=HG19/GRCh37>
##contig=<ID=GL000211.1,length=166566,assembly=HG19/GRCh37>
##contig=<ID=GL000199.1,length=169874,assembly=HG19/GRCh37>
##contig=<ID=GL000217.1,length=172149,assembly=HG19/GRCh37>
##contig=<ID=GL000216.1,length=172294,assembly=HG19/GRCh37>
##contig=<ID=GL000215.1,length=172545,assembly=HG19/GRCh37>
##contig=<ID=GL000205.1,length=174588,assembly=HG19/GRCh37>
##contig=<ID=GL000219.1,length=179198,assembly=HG19/GRCh37>
##contig=<ID=GL000224.1,length=179693,assembly=HG19/GRCh37>
##contig=<ID=GL000223.1,length=180455,assembly=HG19/GRCh37>
##contig=<ID=GL000195.1,length=182896,assembly=HG19/GRCh37>
##contig=<ID=GL000212.1,length=186858,assembly=HG19/GRCh37>
##contig=<ID=GL000222.1,length=186861,assembly=HG19/GRCh37>
##contig=<ID=GL000200.1,length=187035,assembly=HG19/GRCh37>
##contig=<ID=GL000193.1,length=189789,assembly=HG19/GRCh37>
##contig=<ID=GL000194.1,length=191469,assembly=HG19/GRCh37>
##contig=<ID=GL000225.1,length=211173,assembly=HG19/GRCh37>
##contig=<ID=GL000192.1,length=547496,assembly=HG19/GRCh37>
##gwas_harmonisation_command=--data /data/cromwell-executions/qc/03aa2581-76e0-4544-b393-f2ee8ca2cfa6/call-vcf/inputs/1864913356/upload.txt.gz --id IEU-b-1 --json /data/cromwell-executions/qc/03aa2581-76e0-4544-b393-f2ee8ca2cfa6/call-vcf/inputs/1864913356/upload.json --ref /data/cromwell-executions/qc/03aa2581-76e0-4544-b393-f2ee8ca2cfa6/call-vcf/inputs/1899004205/human_g1k_v37.fasta --out /data/igd/IEU-b-1/IEU-b-1_harm.vcf.gz --rm_chr_prefix; 1.1.1
##file_date=2019-09-30T16:01:42.712147
##bcftools_normVersion=1.9+htslib-1.9
##bcftools_normCommand=norm -f /data/cromwell-executions/qc/03aa2581-76e0-4544-b393-f2ee8ca2cfa6/call-combine_multiallelics/inputs/1899004205/human_g1k_v37.fasta -m +any -O z -o /data/igd/IEU-b-1/IEU-b-1_norm.vcf.gz /data/cromwell-executions/qc/03aa2581-76e0-4544-b393-f2ee8ca2cfa6/call-combine_multiallelics/inputs/44387763/IEU-b-1_harm.vcf.gz; Date=Mon Sep 30 16:16:12 2019
##bcftools_annotateVersion=1.9+htslib-1.9
##bcftools_annotateCommand=annotate -a /data/cromwell-executions/qc/03aa2581-76e0-4544-b393-f2ee8ca2cfa6/call-annotate_dbsnp/inputs/-307190728/dbsnp.v153.b37.vcf.gz -c ID -o /data/igd/IEU-b-1/IEU-b-1_dbsnp.vcf.gz -O z /data/cromwell-executions/qc/03aa2581-76e0-4544-b393-f2ee8ca2cfa6/call-annotate_dbsnp/inputs/44387763/IEU-b-1_norm.vcf.gz; Date=Mon Sep 30 16:17:59 2019
##INFO=<ID=EAS_AF,Number=A,Type=Float,Description="Allele frequency in the EAS populations calculated from AC and AN, in the range (0,1)">
##INFO=<ID=EUR_AF,Number=A,Type=Float,Description="Allele frequency in the EUR populations calculated from AC and AN, in the range (0,1)">
##INFO=<ID=AFR_AF,Number=A,Type=Float,Description="Allele frequency in the AFR populations calculated from AC and AN, in the range (0,1)">
##INFO=<ID=AMR_AF,Number=A,Type=Float,Description="Allele frequency in the AMR populations calculated from AC and AN, in the range (0,1)">
##INFO=<ID=SAS_AF,Number=A,Type=Float,Description="Allele frequency in the SAS populations calculated from AC and AN, in the range (0,1)">
##bcftools_annotateCommand=annotate -a /data/cromwell-executions/qc/03aa2581-76e0-4544-b393-f2ee8ca2cfa6/call-annotate_af/inputs/-1558081897/ALL.wgs.phase3_shapeit2_mvncall_integrated_v5b.20130502.sites.vcf.gz -c AF,EAS_AF,EUR_AF,AFR_AF,AMR_AF,SAS_AF -o /data/igd/IEU-b-1/IEU-b-1_data.vcf.gz -O z /data/cromwell-executions/qc/03aa2581-76e0-4544-b393-f2ee8ca2cfa6/call-annotate_af/inputs/44387763/IEU-b-1_dbsnp.vcf.gz; Date=Mon Sep 30 16:34:22 2019
```

###### 1.1.2 Body

| #CHROM | POS     | ID          | REF | ALT | QUAL | FILTER | INFO                                                                                                 | FORMAT            | IEU-b-1                                                                                                          | 
|--------|---------|-------------|-----|-----|------|--------|------------------------------------------------------------------------------------------------------|-------------------|------------------------------------------------------------------------------------------------------------------| 
| 1      | 49298   | rs10399793  | T   | C   | .    | PASS   | AF=0.782149;EAS_AF=0.9633;EUR_AF=0.8936;AFR_AF=0.5204;AMR_AF=0.7104;SAS_AF=0.8855                    | ES:SE:LP:AF:SS:ID | -0.00457955:0.00443769:0.522879:0.623804:49298:rs10399793                                                        | 
| 1      | 54676   | rs2462492   | C   | T   | .    | PASS   | AF=0.39915                                                                                           | ES:SE:LP:AF:SS:ID | -0.00650213:0.00442478:0.853872:0.39915:54676:rs2462492                                                          | 
| 1      | 86028   | rs114608975 | T   | C   | .    | PASS   | AF=0.0277556;EAS_AF=0;EUR_AF=0.0606;AFR_AF=0.0015;AMR_AF=0.013;SAS_AF=0.0685                         | ES:SE:LP:AF:SS:ID | 0.0100214:0.0070434:0.823909:0.10354:86028:rs114608975                                                           | 
| 1      | 91536   | rs6702460   | G   | T   | .    | PASS   | AF=0.420727;EAS_AF=0.4891;EUR_AF=0.6362;AFR_AF=0.0787;AMR_AF=0.3141;SAS_AF=0.6667                    | ES:SE:LP:AF:SS:ID | -0.00580607:0.00435212:0.744727:0.455906:91536:rs6702460                                                         | 
| 1      | 234313  | rs8179466   | C   | T   | .    | PASS   | AF=0.074456                                                                                          | ES:SE:LP:AF:SS:ID | 0.00336766:0.00860662:0.154902:0.074456:234313:rs8179466                                                         | 
| 1      | 534192  | rs6680723   | C   | T   | .    | PASS   | AF=0.242057                                                                                          | ES:SE:LP:AF:SS:ID | -0.00336995:0.00495674:0.30103:0.242057:534192:rs6680723                                                         | 
| 1      | 546697  | rs12025928  | A   | G   | .    | PASS   | AF=0.912867                                                                                          | ES:SE:LP:AF:SS:ID | -5.98981e-05:0.00615052:0.00436481:0.912867:546697:rs12025928                                                    | 
| 1      | 693731  | rs12238997  | A   | G   | .    | PASS   | AF=0.141773;EAS_AF=0.1111;EUR_AF=0.1123;AFR_AF=0.208;AMR_AF=0.0504;SAS_AF=0.1789                     | ES:SE:LP:AF:SS:ID | -0.00302668:0.00413341:0.337242:0.117294:693731:rs12238997                                                       | 
| 1      | 705882  | rs72631875  | G   | A   | .    | PASS   | AF=0.0315495;EAS_AF=0;EUR_AF=0.0775;AFR_AF=0.003;AMR_AF=0.0706;SAS_AF=0.0276                         | ES:SE:LP:AF:SS:ID | 0.00302199:0.006025:0.207608:0.067689:705882:rs72631875                                                          | 
| 1      | 706368  | rs12029736  | A   | G   | .    | PASS   | AF=0.27516;EAS_AF=0.2788;EUR_AF=0.5139;AFR_AF=0.0295;AMR_AF=0.4035;SAS_AF=0.2669                     | ES:SE:LP:AF:SS:ID | -0.0042266:0.00306793:0.769551:0.513298:706368:rs12029736                                                        | 
| 1      | 1097335 | rs9442385   | T   | A,G | .    | PASS   | AF=0.013379,0.834665;EAS_AF=.,0.6339;EUR_AF=.,0.9553;AFR_AF=.,0.8192;AMR_AF=.,0.9035;SAS_AF=.,0.8896 | ES:SE:LP:AF:SS:ID | 0.00308509,0.00224527:0.0152548,0.00492936:0.0757207,0.187087:0.013379,0.93076:1.09734e+06,1.09734e+06:rs9442385 | 


The first row represents a biallelic variant (rs10399793). The reference allele (T) is always the non-effect allele and must match the reference genome sequence. The alternative allele (C) is always the effect allele and often (but not always) the minor allele. The final column contains the effect size (ES), standard error (SE), P value on -log10 scale (LP), study allele frequency (AF), sample size (SS) and study variant identifier (ID). Some fields are optional others required, refer to the header for details.

##### 2 Reserved keys

| Field | Description                                                        | Required | 
|-------|--------------------------------------------------------------------|----------| 
| ES    | Effect size estimate relative to the alternative allele            | YES      | 
| SE    | Standard error of effect size estimate                             | YES      | 
| LP    | -log10 p-value for effect estimate                                 | NO       | 
| AF    | Alternate allele frequency in the association study                | NO       | 
| SS    | Sample size used to estimate genetic effect                        | NO       | 
| EZ    | Z-score provided if it was used to derive the EFFECT and SE fields | NO       | 
| SI    | Accuracy score of summary data imputation                          | NO       | 
| NC    | Number of cases used to estimate genetic effect                    | NO       | 
| ID    | Study variant identifier                                           | NO       | 
