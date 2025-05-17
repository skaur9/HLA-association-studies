## Association Testing with Imputed 4digit Alleles

```bash
plink --dosage hla_4digit.dosage.gz format=1 \
      --pheno phenotype.txt \
      --logistic \
      --covar covariates.txt \
      --out hla_assoc
```

## Amino Acid Association Testing

Extract amino acid polymorphisms using awk as described before. You can test each amino acid residue for association with your phenotype.

```bash
plink --dosage mydata_hla_imputed.HLA.aa format=1 \
      --pheno phenotype.txt \
      --logistic \
      --covar covariates.txt \
      --out hla_amino_assoc
```

## Multi-Allelic Logistic Regression

HLA amino acid positions can be treated as categorical variables with multiple residues. To perform multi-allelic testing, use a custom R script with `nnet::multinom` or `glm` with dummy coding.

Example in R:
```R
library(nnet)
amino_data <- read.table("mydata_hla_imputed.HLA.aa", header=TRUE)
phenotype <- read.table("phenotype.txt", header=TRUE)

# Merge and reshape data
data <- merge(phenotype, amino_data, by="FID")
position_11 <- as.factor(data$AA_DRB1_11)
model <- multinom(case_control ~ position_11 + covariate1 + covariate2, data=data)
summary(model)
```

Alternatively, use `logistic regression with contrasts` to compare specific residues to a reference.


