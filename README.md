# HLA-association-studies

HLA polymorphisms are very different from the rest of the genome. Unlike the biallelic variants (SNPs) that are common throughout most of the genome, the majority of HLA variants are multiallelic and involve changes at multiple base pairs. This means that for each HLA gene, there are numerous possible alleles involving sequence changes at multiple base pairs.

In other words, in the HLA field, the term "allele" refers to the specific combination of point mutations, insertions, and deletions present in a single phased sequence of a given gene. As a result, each allele can encompass multiple variant positions when compared to a reference sequence. Due to this complexity, HLA results are not typically defined by individual SNPs.

To identify these multiallelic variations, HLA alleles are categorized using two levels of nomenclature, neither of which typically represent a single base pair change:
2-Digit HLA Alleles: The 2-digit code (e.g., HLA-A*01) refers to a broad group of HLA alleles that share a similar sequence but can differ by multiple base pairs across the HLA gene.
4-Digit HLA Alleles: The 4-digit code (e.g., HLA-A*01:01) provides more specificity, representing a subgroup of alleles that are more closely related in sequence. However, even at the 4-digit level, these alleles can differ by several base pairs and across multiple regions of the gene.

This is why we also look at the amino acid polymorphisms (that is another form of HLA allele nomenclature) which offers higher resolution. By examining these specific amino acid changes, we can better understand which variations may be driving associations with specific traits or diseases.

You can find more information about HLA alleles here:
- https://www.ebi.ac.uk/ipd/imgt/hla/


This repository provides examples of association studies using 2 and 4 digit HLA alleles as well as amino-acid-polymorphisms derived after HLA imputation using SNP2HLA

SNP2HLA is a widely used tool that imputes classical HLA alleles (2-digit and 4-digit resolution), amino acid polymorphisms, and intragenic SNPs from SNP genotype data.

## Notes

- Use high-quality genotype data (QC is crucial).
- Ensure SNPs in your dataset overlap well with the reference panel.
- Beagle 3 is required for SNP2HLA and must be in the working directory or specified via `-bgl`.

## References

- Jia X, et al. (2013). "Imputing amino acid polymorphisms in human leukocyte antigens." *PLoS ONE*.
- SNP2HLA: https://github.com/immunogenomics/snp2hla

---

For questions or contributions, feel free to open an issue or submit a pull request!
