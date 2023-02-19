# AGAIN
Genome-wide detection of AG-gain variants between the splicing branchpoint and canonical acceptor site in human introns

## Introduction
- Human variants that introduce an AG in the intronic region between the branchpoint (BP) and the canonical acceptor site (ACC) of protein-coding genes can disrupt pre-mRNA splicing. 

- Based on our previously developed BPHunter database and software, we precisely delineate the BP-ACC segments of all human introns, for the first time. We find an extreme depletion of AG/YAG in the [BP+8, ACC-4] region. 

- AGAIN is a genome-wide approach to pinpoint intronic AG-gain variants (SNVs, insertions, deletions) in the BP-ACC region of human genomes. AGAIN also predicts protein-level outcomes resulting from two major missplicing consequences (new acceptor site & complete exon skipping).

- This standalone version can be easily implemented into NGS analysis by a one-line command. We also provided a [AGAIN webserver](http://hgidsoft.rockefeller.edu/AGAIN) with user-friendly interface.

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

To use the latest version-2, please download and replace the reference datasets.

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
  - BP_NAME: m/e/cBP_chrom_pos_strand_nucleotide
  - BP_ACC_DIST: distance from BP to acceptor site
  - BP_RANK: rank of BP in this intron
  - BP_TOTAL: total number of BP in this intron
  - BP_HIT: BP position (-2, -1, 0) hit by the variant 
  - BP_SOURCE: number of sources supporting this BP position
  - CONSENSUS: level of consensus (1:YTNAY, 2:YTNA, 3:TNA, 4:YNA, 0:none)
  - BP/BP2_GERP: conservation score GERP for BP and BP-2 positions
  - BP/BP2_PHYL: conservation score PHYLOP for BP and BP-2 positions
  - BPHunter_HIGHRISK: YES/NO if a BP variant considered as high-risk
  - BPHunter_SCORE: score of a BP variant (suggested cutoff>=3, max=10)

### Command & Parameters (BPHunter_VCF.py)
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

### Command & Parameters (BPHunter_VCF_batch.py)
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
<img src="https://hgidsoft.rockefeller.edu/AGAIN/img/AGAIN_Scoring.jpg" width="70%" height="70%">

## Reference
- ***Zhang P. et al.*** Genome-wide detection of human intronic AG-gain variants between the splicing branchpoint and canonical acceptor site. 2023.

## Contact
> **Developer:** Peng Zhang, Ph.D.

> **Email:** pzhang@rockefeller.edu

> **Laboratory:** St. Giles Laboratory of Human Genetics of Infectious Diseases

> **Institution:** The Rockefeller University, New York, NY, USA
