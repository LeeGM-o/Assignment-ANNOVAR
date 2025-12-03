# Assignment-ANNOVAR
## Objective
* By integrating annotation across multiple databases through *ANNOVAR*, we identify the locations and functional impacts of DNA variants in specific populations, along with their allele frequencies, tumor-associated variants, and clinically reported variants.
## ANNOVAR
* ANNOVAR is an efficient software tool to utilize update-to-date information to functionally annotate genetic variants detected from diverse genomes (including human genome hg18, hg19, hg38, hs1 (T2T-CHM13) as well as mouse, worm, fly, yeast, SARS-CoV-2, and many others). Given a list of variants with chromosome, start position, end position, reference nucleotide and observed nucleotides, ANNOVAR can perform:
> 1) **Gene-based annotation**: identify whether SNPs or CNVs cause protein coding changes and the amino acids that are affected. Users can flexibly use RefSeq genes, UCSC genes, Ensembl/Gencode genes, or custom gene definition system.
> 2) **Region-based annotation**: identify variants in specific genomic regions, for example, conserved regions among multiple species, predicted transcription factor binding sites, segmental duplication regions, database of genomic variants, DNAse I hypersensitivity sites, ENCODE H3K4Me1/H3K4Me3/H3K27Ac/CTCF sites, ChIP-Seq peaks, RNA-Seq peaks, ENCODE cCRE sites, or many other annotations on genomic intervals.
> 3) **Filter-based annotation**: identify variants that are documented in specific databases, for example, whether a variant is reported in dbSNP, what is the allele frequency in the 1000 Genome Project, NHLBI-ESP 6500 exomes or Exome Aggregation Consortium (ExAC) or Genome Aggregation Database (gnomAD), calculate the SIFT/PolyPhen/LRT/MutationTaster/MutationAssessor/FATHMM/MetaSVM/MetaLR/MetaRNN scores, find pathogenic mutations from ClinVar, identify recurrent somatic mutations in COSMIC in specific cancer types, or many other annotations on specific mutations.
> 4) **Other functionalities**: Retrieve the nucleotide sequence in any user-specific genomic positions in batch, identify a candidate gene list for Mendelian diseases from exome data, and other utilities.
## Data
* VCF files Human Whole Exome Data via Illumina platform for JAS patients
> P18: JAS_P18.GATK.snp.vcf;JAS_P18.GATK.indel.vcf
> N36: JAS_N36.GATK.snp.vcf;JAS_N36.GATK.indel.vcf
## Processing
#### 1) File format conversion
* Convert VCF files to avinput format.

#### 2) ANNOVAR annotation
#### 3) Downstream analysis
## citation
* [https://annovar.openbioinformatics.org/en/latest/](https://annovar.openbioinformatics.org/en/latest/)
* [https://figshare.com/articles/dataset/Whole_Exome_Data_VCF_files/13696750](https://figshare.com/articles/dataset/Whole_Exome_Data_VCF_files/13696750)
* [Wang K, Li M, Hakonarson H. ANNOVAR: Functional annotation of genetic variants from next-generation sequencing data Nucleic Acids Research, 38:e164, 2010](https://academic.oup.com/nar/article/38/16/e164/1749458)
