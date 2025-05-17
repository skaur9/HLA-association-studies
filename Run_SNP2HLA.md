## Installation

```bash
# Clone SNP2HLA from GitHub
https://github.com/immunogenomics/snp2hla
cd snp2hla
```

## Requirements

- Java 1.6 or later
- PLINK 1.9
- Beagle 3.0.4
- SNP2HLA pipeline
- Reference panel (e.g., T1DGC panel)

## Input Files

1. **PLINK format genotype data** (`.bed`, `.bim`, `.fam`)
2. **HLA reference panel** (e.g., T1DGC available from the Broad Institute)

## Preparing Data

Ensure your genotype data is in PLINK binary format and extract chr 6:

```bash
plink --bfile mygenotypes --chr 6 --from-kb 25000 --to-kb 35000 --make-bed --out chr6_mhc
```

## Running SNP2HLA

```bash
java -Xmx4g -jar SNP2HLA.jar \
  --bfile chr6_mhc \
  --reference T1DGC_reference \
  --out mydata_hla_imputed
```

- `--bfile`: Input PLINK file
- `--reference`: Path to the reference panel
- `--out`: Prefix for output files

## Output Files

- `*.HLA.alleles`: Imputed classical HLA alleles (2-digit and 4-digit)
- `*.HLA.aa`: Imputed amino acid polymorphisms
- `*.HLA.snp`: Imputed SNPs in the HLA region

## Example: Extracting 4-digit Alleles

```bash
awk '$2 ~ /HLA/ && $2 ~ /:/ { print $2 }' mydata_hla_imputed.HLA.alleles > hla_4digit.list
plink --dosage mydata_hla_imputed.HLA.alleles format=1 \
      --extract hla_4digit.list \
      --out hla_4digit
```

## Example: Extracting Amino Acid Alleles

```bash
awk '$2 ~ /AA/ && $2 ~ /:/ { print $2 }' mydata_hla_imputed.HLA.alleles > hla_aa_alleles.list
plink --dosage mydata_hla_imputed.HLA.alleles format=1 \
      --extract hla_aa_alleles.list \
      --out hla_aa_alleles
```

## Example: Association Testing with Imputed Alleles

```bash
plink --dosage hla_4digit.dosage.gz format=1 \
      --pheno phenotype.txt \
      --logistic \
      --covar covariates.txt \
      --out hla_assoc
```
