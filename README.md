# Assignment-ANNOVAR
*ANNOVAR* is an efficient software tool to utilize update-to-date information to functionally annotate genetic variants detected from diverse genomes (including human genome hg18, hg19, hg38, hs1 (T2T-CHM13) as well as mouse, worm, fly, yeast, SARS-CoV-2, and many others). Given a list of variants with chromosome, start position, end position, reference nucleotide and observed nucleotides, ANNOVAR can perform:
* **Gene-based annotation**: identify whether SNPs or CNVs cause protein coding changes and the amino acids that are affected. Users can flexibly use RefSeq genes, UCSC genes, Ensembl/Gencode genes, or custom gene definition system.
* **Region-based annotation**: identify variants in specific genomic regions, for example, conserved regions among multiple species, predicted transcription factor binding sites, segmental duplication regions, database of genomic variants, DNAse I hypersensitivity sites, ENCODE H3K4Me1/H3K4Me3/H3K27Ac/CTCF sites, ChIP-Seq peaks, RNA-Seq peaks, ENCODE cCRE sites, or many other annotations on genomic intervals.
* **Filter-based annotation**: identify variants that are documented in specific databases, for example, whether a variant is reported in dbSNP, what is the allele frequency in the 1000 Genome Project, NHLBI-ESP 6500 exomes or Exome Aggregation Consortium (ExAC) or Genome Aggregation Database (gnomAD), calculate the SIFT/PolyPhen/LRT/MutationTaster/MutationAssessor/FATHMM/MetaSVM/MetaLR/MetaRNN scores, find pathogenic mutations from ClinVar, identify recurrent somatic mutations in COSMIC in specific cancer types, or many other annotations on specific mutations.
* **Other functionalities**: Retrieve the nucleotide sequence in any user-specific genomic positions in batch, identify a candidate gene list for Mendelian diseases from exome data, and other utilities.
  
## Objective
By integrating annotation across multiple databases through *ANNOVAR*, we identify the locations and functional impacts of DNA variants in specific populations, along with their allele frequencies, tumor-associated variants, and clinically reported variants.
  
## Data
VCF files Human Whole Exome Data via Illumina platform for JAS patients
* P18: JAS_P18.GATK.snp.vcf;JAS_P18.GATK.indel.vcf   
* N36: JAS_N36.GATK.snp.vcf;JAS_N36.GATK.indel.vcf

## Processing
#### 1) File format conversion
Convert VCF files to avinput format.
```
convert2annovar.pl -format vcf4 SNP/Indel.vcf > SNP/Indel.avinput
```
![annovar1](https://github.com/user-attachments/assets/2a7f4abc-dbfb-419e-950a-f03005a9408a)

#### 2) ANNOVAR annotation
Annotation DB:
* **refGene**: Classification of variant locations and functions
* **gnomAD**: frequency of alleles by population
* **ClinVar**: Disease association, clinical interpretation
* **COSMIC**: Cancer-derived mutation information
```
# Create TXT file
annotate_variation.pl -buildver hg38
   -downdb
   -webfrom annovar refGeneWithVer humandb/
annotate_variation.pl -buildver hg38
   -downdb
   -webfrom annovar gnomad47_exome humandb/ 
annotate_variation.pl -buildver hg38
   -downdb
   -webfrom annovar clinvar_20240917 humandb/ 
annotate_variation.pl -buildver hg38
   -downdb
   -webfrom annovar cosmic70 humandb/

# Create annotation CSV file
table_annovar.pl JAS_GATK.avinput humandb/ 
  -buildver hg38 
  -out JAS_anno 
  -protocol refGeneWithVer,gnomad47_exome,clinvar_20240917,cosmic70 
  -operation g,f,f,f 
  -xref example/gene_xref.txt 
  -remove -nastring . -csvout -polish
```
![annovar2](https://github.com/user-attachments/assets/523239dd-524d-4ea3-b8be-d9472b8736d6)  
Downstream analysis was performed by extracting only the variation in the exon site (exonic, splicing, exonic; splicing).

#### 3) Downstream analysis
![annovar3](https://github.com/user-attachments/assets/7d400031-0b16-4225-804a-8d7eaea5639b)
**a)** Variations were highest in chromosomes 1 and 19.  
**b)** It was confirmed that the gene with the most mutations was the *MUC3A*(mucus-related) gene group.  
**c)** When comparing the allele frequencies of two exonic mutations(synonic SNVs, non-synonic SNVs) related to protein amino acid sequences, they tend to show a similar distribution.  
**d)** When comparing allele frequencies by race for specific gene *NRXN2* registered in the main DB and mentioned in the ANNOVAR tutorial, it was found that allele frequencies were relatively low in African and African American and East Asian races.  
**e)** When tumor-related mutations were identified with the COSMIC DB, the mutations derived from large intestine tissue were the most common.  
**f)** When we checked what mutations were reported clinically through the ClinVar DB, Benign was the most common, which is likely a normal mutation that does not cause disease.

## citation
* Wang K, Li M, Hakonarson H. [ANNOVAR: Functional annotation of genetic variants from next-generation sequencing data Nucleic Acids Research](https://academic.oup.com/nar/article/38/16/e164/1749458), 38:e164, 2010
* [https://annovar.openbioinformatics.org/en/latest/](https://annovar.openbioinformatics.org/en/latest/)
* [https://figshare.com/articles/dataset/Whole_Exome_Data_VCF_files/13696750](https://figshare.com/articles/dataset/Whole_Exome_Data_VCF_files/13696750)
