# Real World Bioinformatics with R — course environment (R 4.4 / Bioconductor 3.19, RStudio Server)
FROM bioconductor/bioconductor_docker:RELEASE_3_19

# Course packages (binary installs from Bioconductor's container repo where available), then GitHub-only ones and data packages.
RUN Rscript -e 'BiocManager::install(c("AnnotationDbi", "AnnotationHub", "ComplexHeatmap", "DESeq2", "GEOquery", "GenomicFeatures", "GenomicRanges", "Polychrome", "TxDb.Hsapiens.UCSC.hg19.knownGene", "ChIPseeker", "rtracklayer", "biomaRt", "circlize", "clusterProfiler", "dplyr", "forcats", "ggplot2", "ggrepel", "knitr", "msigdbr", "org.Hs.eg.db", "purrr", "readr", "recount3", "rmarkdown", "stringr", "tibble", "tidyr", "tidyverse", "txdbmaker"), ask = FALSE, update = FALSE, Ncpus = 4)' \
 && Rscript -e 'ok <- vapply(c("AnnotationDbi", "AnnotationHub", "ComplexHeatmap", "DESeq2", "GEOquery", "GenomicFeatures", "GenomicRanges", "Polychrome", "TxDb.Hsapiens.UCSC.hg19.knownGene", "ChIPseeker", "rtracklayer", "biomaRt", "circlize", "clusterProfiler", "dplyr", "forcats", "ggplot2", "ggrepel", "knitr", "msigdbr", "org.Hs.eg.db", "purrr", "readr", "recount3", "rmarkdown", "stringr", "tibble", "tidyr", "tidyverse", "txdbmaker"), requireNamespace, logical(1), quietly = TRUE); if (!all(ok)) stop("missing: ", paste(names(ok)[!ok], collapse = " ")); cat("all course packages installed\n")' \
 && rm -rf /tmp/downloaded_packages /tmp/Rtmp*

# RStudio Server without a login page (rocker's /init configures it from DISABLE_AUTH/USER); open the course folder by default.
RUN { echo; echo "session-default-working-dir=/workspaces/r-course-env"; echo "session-default-new-project-dir=/workspaces/r-course-env"; } >> /etc/rstudio/rsession.conf \
 && echo "rstudio ALL=(ALL) NOPASSWD:ALL" > /etc/sudoers.d/rstudio && chmod 0440 /etc/sudoers.d/rstudio
ENV DISABLE_AUTH=true USER=rstudio
