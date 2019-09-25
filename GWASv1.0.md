# The Variant Call Format (VCF) Version 1.0 Specification For Storing Genome-wide Association Study (GWAS) Summary Statistics

1. The VCF specification

Refer to [hts-specs](https://samtools.github.io/hts-specs/VCFv4.2.pdf) for the VCF specification

1.1 An example

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
##SAMPLE=<ID=IEU-b-1,TotalVariants=9,VariantsNotRead=0,HarmonisedVariants=9,VariantsNotHarmonised=0,SwitchedAlleles=9,StudyType=Continuous>
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
##gwas_harmonisation_command=--data /data/cromwell-executions/qc/7652b1ae-ea51-44f9-8bd7-b78aba59de01/call-vcf/inputs/1864913356/upload.txt.gz --id IEU-b-1 --json /data/cromwell-executions/qc/7652b1ae-ea51-44f9-8bd7-b78aba59de01/call-vcf/inputs/1864913356/upload.json --ref /data/cromwell-executions/qc/7652b1ae-ea51-44f9-8bd7-b78aba59de01/call-vcf/inputs/1899004205/human_g1k_v37.fasta --out /data/igd/IEU-b-1/IEU-b-1_harm.vcf.gz --rm_chr_prefix; 1.1.1
##file_date=2019-09-25T13:42:05.896004
##bcftools_normVersion=1.9+htslib-1.9
##bcftools_normCommand=norm -f /data/cromwell-executions/qc/7652b1ae-ea51-44f9-8bd7-b78aba59de01/call-combine_multiallelics/inputs/1899004205/human_g1k_v37.fasta -m +any -O z -o /data/igd/IEU-b-1/IEU-b-1_norm.vcf.gz /data/cromwell-executions/qc/7652b1ae-ea51-44f9-8bd7-b78aba59de01/call-combine_multiallelics/inputs/44387763/IEU-b-1_harm.vcf.gz; Date=Wed Sep 25 13:42:10 2019
##bcftools_annotateVersion=1.9+htslib-1.9
##bcftools_annotateCommand=annotate -a /data/cromwell-executions/qc/7652b1ae-ea51-44f9-8bd7-b78aba59de01/call-annotate_dbsnp/inputs/-307190728/dbsnp.v153.b37.vcf.gz -c ID -o /data/igd/IEU-b-1/IEU-b-1_dbsnp.vcf.gz -O z /data/cromwell-executions/qc/7652b1ae-ea51-44f9-8bd7-b78aba59de01/call-annotate_dbsnp/inputs/44387763/IEU-b-1_norm.vcf.gz; Date=Wed Sep 25 13:42:19 2019
##INFO=<ID=EAS_AF,Number=A,Type=Float,Description="Allele frequency in the EAS populations calculated from AC and AN, in the range (0,1)">
##INFO=<ID=EUR_AF,Number=A,Type=Float,Description="Allele frequency in the EUR populations calculated from AC and AN, in the range (0,1)">
##INFO=<ID=AFR_AF,Number=A,Type=Float,Description="Allele frequency in the AFR populations calculated from AC and AN, in the range (0,1)">
##INFO=<ID=AMR_AF,Number=A,Type=Float,Description="Allele frequency in the AMR populations calculated from AC and AN, in the range (0,1)">
##INFO=<ID=SAS_AF,Number=A,Type=Float,Description="Allele frequency in the SAS populations calculated from AC and AN, in the range (0,1)">
##bcftools_annotateCommand=annotate -a /data/cromwell-executions/qc/7652b1ae-ea51-44f9-8bd7-b78aba59de01/call-annotate_af/inputs/-1558081897/ALL.wgs.phase3_shapeit2_mvncall_integrated_v5b.20130502.sites.vcf.gz -c AF,EAS_AF,EUR_AF,AFR_AF,AMR_AF,SAS_AF -o /data/igd/IEU-b-1/IEU-b-1_data.vcf.gz -O z /data/cromwell-executions/qc/7652b1ae-ea51-44f9-8bd7-b78aba59de01/call-annotate_af/inputs/44387763/IEU-b-1_dbsnp.vcf.gz; Date=Wed Sep 25 13:55:49 2019
#CHROM	POS	ID	REF	ALT	QUAL	FILTER	INFO	FORMAT	IEU-b-1
10	9960129	rs4747841	A	G	.	PASS	AF=0.460264;EAS_AF=0.6032;EUR_AF=0.495;AFR_AF=0.3434;AMR_AF=0.4164;SAS_AF=0.4663	ES:SE:LP:AF:SS:ID	-0.0037:0.0052:0.145208:0.5092:89138:rs4747841
10	9960259	rs4749917	C	T	.	PASS	AF=0.459665;EAS_AF=0.6032;EUR_AF=0.495;AFR_AF=0.3434;AMR_AF=0.415;SAS_AF=0.4642	ES:SE:LP:AF:SS:ID	-0.0033:0.0052:0.11081:0.5092:89138:rs4749917
10	9960453	rs12219605	G	T	.	PASS	AF=0.459665;EAS_AF=0.6032;EUR_AF=0.495;AFR_AF=0.3434;AMR_AF=0.415;SAS_AF=0.4642	ES:SE:LP:AF:SS:ID	-0.0035:0.0052:0.131179:0.5092:89138:rs12219605
10	100012739	rs737656	A	G	.	PASS	AF=0.573482;EAS_AF=0.5278;EUR_AF=0.672;AFR_AF=0.416;AMR_AF=0.6398;SAS_AF=0.6851	ES:SE:LP:AF:SS:ID	-0.0099:0.0054:1.39794:0.6794:89888:rs737656
10	100012890	rs737657	A	G	.	PASS	AF=0.572684;EAS_AF=0.5268;EUR_AF=0.671;AFR_AF=0.416;AMR_AF=0.6383;SAS_AF=0.684	ES:SE:LP:AF:SS:ID	-0.0084:0.0054:1.07428:0.6794:89888:rs737657
10	100013563	rs7086391	C	T	.	PASS	AF=0.132788;EAS_AF=0.0288;EUR_AF=0.2187;AFR_AF=0.1589;AMR_AF=0.1484;SAS_AF=0.1053ES:SE:LP:AF:SS:ID	-0.0075:0.0067:0.570409:0.219:89888:rs7086391
10	100013815	rs878177	C	T	.	PASS	AF=0.360224;EAS_AF=0.6062;EUR_AF=0.341;AFR_AF=0.0522;AMR_AF=0.5231;SAS_AF=0.4274	ES:SE:LP:AF:SS:ID	-0.0073:0.0055:0.861382:0.3483:89888:rs878177
10	100015603	rs3763689	G	T	.	PASS	AF=0.13139;EAS_AF=0.0288;EUR_AF=0.2207;AFR_AF=0.152;AMR_AF=0.1484;SAS_AF=0.1053	ES:SE:LP:AF:SS:ID	-0.0066:0.0063:0.489187:0.2203:89888:rs3763689
10	100016339	rs1983865	C	T	.	PASS	AF=0.507588;EAS_AF=0.752;EUR_AF=0.4503;AFR_AF=0.2474;AMR_AF=0.6167;SAS_AF=0.589	ES:SE:LP:AF:SS:ID	-0.0037:0.0052:0.469288:0.4591:89888:rs1983865
```
