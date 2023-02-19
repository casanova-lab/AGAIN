# AGAIN
Genome-wide detection of human intronic AG-gain variants between the splicing branchpoint and canonical acceptor site

## Introduction
- Human variants that introduce an AG in the intronic region between the branchpoint (BP) and the canonical acceptor site (ACC) of protein-coding genes can disrupt pre-mRNA splicing.

- Based on our previously developed BPHunter ([github](https://github.com/casanova-lab/BPHunter) and [webserver](https://hgidsoft.rockefeller.edu/BPHunter)), we precisely delineate the BP-ACC segments of all human introns, for the first time. We find an extreme depletion of AG/YAG in the [BP+8, ACC-4] region. 

- AGAIN is a genome-wide approach to pinpoint intronic AG-gain variants (SNVs, insertions, deletions) in the BP-ACC region of human genomes. AGAIN also predicts protein-level outcomes resulting from two major missplicing consequences (new acceptor site & complete exon skipping).

- This standalone version can be easily implemented into NGS analysis by a one-line command. We also provided the [AGAIN webserver](http://hgidsoft.rockefeller.edu/AGAIN) with user-friendly interface.

## News
- Feb 2023: AGAIN webserver & github was launched.
- Sep 2022: AGAIN prototype was completed.
- Jan 2022: Inspired by BPHunter study, AGAIN idea was conceived.

## Usage 
Current version: version-1
### Dependency
The code is written in [python3](https://www.python.org/downloads/), and requires [bedtools](https://bedtools.readthedocs.io/en/latest/) installed.

### Reference datasets
Due to the file size limit in GitHub, please download the [AGAIN reference datasets](http://hgidsoft.rockefeller.edu/AGAIN/standalone.html) and put them into your AGAIN folder.

### File Format
**Input:** Variants in VCF format, with 5 mandatory and tab-delimited fields (CHROM, POS, ID, REF, ALT).
  - The 48 published pathogenic BP variants are provided as the example input. (Example_var_BP.vcf)

**Output:** AGAIN-detected variants will be output with the following annotations.
  - SAMPLE (only for BPHunter_VCF_batch.py)
  - CHROM, POS, ID, REF, ALT (exactly the same as input)
  - STRAND: +/-
  - VAR_TYPE: snv, x-nt del, x-nt ins
  - GENE: gene symbol
  - TRANSCRIPT_IVS: ENST123456789_IVS10
  - CANONICAL: canonical transcript_IVS, or '.'
  - AGAIN_ZONE: ZONE1/ZONE2, ZONE1 is from 1st BP to ACC, ZONE2 is from 2nd BP to 1st BP
  - AGAIN_YAG: YES/NO, if the AG-gain variant also fits YAG
  - AGAIN_BP_DIST: the distance from the created AG to BP
  - AGAIN_ACC_DIST: the distance from the created AG to ACC
  - AGAIN_HIGHRISK: YES/NO, if the AG-gain variant falls inside high-risk [BP+8, ACC-4] region
  - AGAIN_SCORE: score of the AG-gain variant (suggested cutoff >= 3, max = 5)
  - PROT_SEQ_WT: wild-type protein sequence
  - PROT_SEQ_NEW_ACC: consequent protein sequence if new acceptor site is created
  - HGVS_NEW_ACC: protein-level HGVS annotation if new acceptor site is created
  - PROT_SEQ_EXON_SKIP: consequent protein sequence if exon skipping occurs
  - HGVS_EXON_SKIP: protein-level HGVS annotation if exon skipping occurs

### Command & Parameters (AGAIN_VCF.py)
```
python AGAIN_VCF.py -i variants.vcf
```
```
python AGAIN_VCF.py -i variants.vcf -g GRCh37 -t all
```

Parameter | Type | Description | Default
----------|------|-------------|--------------
*-i*|file|variants in VCF format, with 5 fields (CHROM, POS, ID, REF, ALT)|N.A.
*-g*|str|human reference genome assembly (GRCh37 / GRCh38)|GRCh37
*-t*|str|all / canonical transcripts?|all

### Command & Parameters (AGAIN_VCF_batch.py)
```
python AGAIN_VCF_batch.py -d /dir -s samplelist.txt -o output.txt
```
```
python AGAIN_VCF_batch.py -d /dir -s samplelist.txt -o output.txt -g GRCh37 -t all
```

Parameter | Type | Description | Default
----------|------|-------------|--------------
*-d*|str|directory of VCF files|N.A.
*-s*|file|sample list (without .vcf extension) to be screened in the above directory|N.A.
*-o*|str|output filename|N.A.
*-g*|str|human reference genome assembly (GRCh37 / GRCh38)|GRCh37
*-t*|str|all / canonical transcripts?|all

### BPHunter Scoring Scheme
<img src="https://hgidsoft.rockefeller.edu/AGAIN/img/AGAIN_Scoring.jpg" width="50%" height="50%">

## Reference
- ***Zhang P. et al.*** Genome-wide detection of human intronic AG-gain variants between the splicing branchpoint and canonical acceptor site. 2023.

## Contact
> **Developer:** Peng Zhang, Ph.D.

> **Email:** pzhang@rockefeller.edu

> **Laboratory:** St. Giles Laboratory of Human Genetics of Infectious Diseases

> **Institution:** The Rockefeller University, New York, NY, USA
