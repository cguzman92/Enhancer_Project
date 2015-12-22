# Enhancer_Project

## Overview

Goal of the project is to access the enrichment of KEC at enhancers.

After running PARE we had approximately ~8k enhancers identified. Some were in intragenic space so those have to be removed.

Using the BEDOPS toolkit:

1. Make sure TSSs and regions are sorted:

```$ sort-bed TSS.unsorted.bed > TSS.bed
$ sort-bed regions.unsorted.bed > regions.bed```

2. Pad TSSs by 5000 bases and merge them into disjoint regions with bedops --range and --merge. Pipe the result to a filter step using bedops --not-element-of:

```$ bedops --range 5000 --merge TSS.bed | bedops --not-element-of 1 regions.bed - > regions.intergenic.bed```

