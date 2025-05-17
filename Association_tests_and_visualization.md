## Association Testing with Imputed Alleles

```bash
plink --dosage hla_4digit.dosage.gz format=1 \
      --pheno phenotype.txt \
      --logistic \
      --covar covariates.txt \
      --out hla_assoc
```

## Visualization 

### 1. Dosage Distribution

Using R:
```R
hla_dosages <- read.table("hla_4digit.dosage.gz", header=TRUE)
hla_A_02_01 <- hla_dosages$HLA_A_02_01

hist(hla_A_02_01, breaks=50, main="HLA-A*02:01 Dosage Distribution",
     xlab="Dosage", col="skyblue")
```

### 2. Association Plot (Manhattan Plot)

Using `qqman` in R:
```R
library(qqman)
hla_assoc <- read.table("hla_assoc.assoc.logistic", header=TRUE)
manhattan(hla_assoc, chr="CHR", bp="BP", snp="SNP", p="P",
          main="HLA Association Results", col=c("blue4", "orange3"))
```

### 3. Heatmap of Imputed Alleles

Using `pheatmap`:
```R
library(pheatmap)
allele_matrix <- as.matrix(hla_dosages[,2:ncol(hla_dosages)])
pheatmap(allele_matrix, scale="none", show_rownames=FALSE,
         main="Heatmap of Imputed HLA Alleles")
```
