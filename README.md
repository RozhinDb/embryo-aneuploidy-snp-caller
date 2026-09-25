Detecting chromosomal aneuploidy in embryo biopsies from SNP-array data

This notebook is a small pipeline I built as a code sample for the VUB / UZ Brussel PhD application in Medical Genetics. It takes SNP-array data from an embryo biopsy, B-allele frequency and LogR, together with the genotypes of both parents, and calls whether each chromosome is normal, trisomic, or monosomic, including which parent the extra or missing copy came from.

All data in this notebook are simulated. Real parent-embryo genotype data is clinical and protected, so I generated my own dataset with a known ground truth for every chromosome. This let me measure sensitivity and specificity honestly rather than assume the method works.
The core idea, grouping SNPs by parental genotype to read the expected B-allele signal for each chromosome state, comes from Verdyck et al. (2025), Genes 16:115 (APCAD Part 2). This is my own simplified version of that idea, not a reimplementation.

One result I found worth highlighting: LogR alone gives excellent accuracy per chromosome, but since every embryo has 22 autosomes, even a low false-positive rate per chromosome adds up to a much higher chance that a healthy embryo gets flagged incorrectly. Adding the B-allele evidence brought embryo-level specificity from 0.70 to 1.00 in my simulations.
The notebook also tests how performance changes as biopsy quality worsens, and ends with a section on what the model leaves out and what I would do differently with real data.
