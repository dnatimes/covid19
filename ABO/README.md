# ABO Blood type analysis

Recently, Zhao et al.[1] reported the difference of ABO blood type frequencies between the COVID-19 patients and the control population. To replicate their findings using an independent controls consists of unrelated individuals, and to provide a reference panel for ABO blood type frequencies across diverse populations, we aggregated the ABO blood type information. Given that the haplotype at _ABO_ locus that define the four major ABO antigen is tagged by 3 SNPs[2,3], we extracted the genotype information at those variants, computed the frequencies of the haplotypes and the blood types across 9 population groups (White British, Non-British white, African, South Asian, East Asian, self-reported Chinese, self-reported Indian, self-reported Pakistani, and self-reported Bangladeshi).

Please check out initial draft of host genetics of COVID-19, [Initial review and analysis of COVID-19 host genetics and associated phenotypes](https://tinyurl.com/genes-covid19)(it is now hosted on Google Docs -- we submitted the manuscript to a pre-print server)  for more about our analysis.

| ABO allele | rs8176746 | rs687289 | rs507666 |
|------------|-----------|----------|----------|
| A1         | G         | A        | A        |
| A2         | G         | A        | G        |
| B          | T         | A        | G        |
| O          | G         | G        | G        |

Table: the list of tag SNPs used for the ABO blood type analysis.

## List of files in this directory

### Results files

- [`ABO_external_studies_freq.tsv`](ABO_external_studies_freq.tsv): this file contains the ABO frequency information from a previous study[1].
- [`ABO_UKB_freq.tsv`](ABO_UKB_freq.tsv): this file contains our estimates of the frequencies of ABO blood types (`haplotype`, `ABO_allele`, and `ABO_allele_full` columns) in population groups (`population` column) in UK Biobank. The `n` column is the number of individuals, `frequency` is the estimated frequency, and `SE` represents the standard error.
- [`ABO_combined_freq.tsv`](ABO_combined_freq.tsv): this file contains the ABO blood frequency information for both external studies and UK Biobank.
- [`ABO_OR.tsv`](ABO_OR.tsv): this file contains the results of frequency comparison.

### Scripts and notebook

- [`1_prep_plink_data.sh`](1_prep_plink_data.sh): we extract the three variants (defined in [`1_prep_plink_data.var.lst`](1_prep_plink_data.var.lst)) from the genotype dataset and prepare files for plink version 1.07.  
- [`2_hap_freq.sh`](2_hap_freq.sh): phase (estimate the haplotype) and estimate their frequencies with plink 1.07.
- [`3_compute_hap_freq.R`](3_compute_hap_freq.R) and [`3_compute_hap_freq.sh`](3_compute_hap_freq.sh): compute the estimated blood type frequencies.
- [`4_ABO_freq_combine.R`](4_ABO_freq_combine.R): combine the estimated blood type frequencies into a file ([`ABO_UKB_freq.tsv`](ABO_UKB_freq.tsv)).
- [`5_ABO_comparison.ipynb`](5_ABO_comparison.ipynb): compare the ABO blood type frequencies. The results are written to [`ABO_OR.tsv`](ABO_OR.tsv).
- [`sample_qc_v3.2.self_reported_pop_def.ipynb`](sample_qc_v3.2.self_reported_pop_def.ipynb): this notebook illustrates our procedure to define additional population groups of unrelated invidiuals in UK Biobank using the self-reported ethnicity data. The population size is recorded in [`UKB_population_n.tsv`](UKB_population_n.tsv).
- [`ABO_functions.R`](ABO_functions.R): this file contains functions used in the R scripts.

## Acknowledgement

We thank Mike Inouye ([@minouye271](https://twitter.com/minouye271)) for pointing the reference[3].

## Reference

1. [Zhao, J. et al. Relationship between the ABO Blood Group and the COVID-19 Susceptibility. medRxiv 2020.03.11.20031096 (2020)](https://doi.org/10.1101/2020.03.11.20031096).
2. [Paré, G. et al. Novel Association of ABO Histo-Blood Group Antigen with Soluble ICAM-1: Results of a Genome-Wide Association Study of 6,578 Women. PLOS Genetics 4, e1000118 (2008)](https://doi.org/10.1371/journal.pgen.1000118).
3. [Johansson, Å., Alfredsson, J., Eriksson, N., Wallentin, L. & Siegbahn, A. Genome-Wide Association Study Identifies That the ABO Blood Group System Influences Interleukin-10 Levels and the Risk of Clinical Events in Patients with Acute Coronary Syndrome. PLOS ONE 10, e0142518 (2015)](https://doi.org/10.1371/journal.pone.0142518).
4. [Purcell, S. et al. PLINK: A Tool Set for Whole-Genome Association and Population-Based Linkage Analyses. The American Journal of Human Genetics 81, 559–575 (2007)](https://doi.org/10.1086/519795).