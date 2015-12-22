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

The result is 2,448 proposed enhancer regions in intergenic space.

Preliminary analysis: Generate heatmaps and metagene plots to test for enrichment and de-enrichment. Done using deeptools for visualization.

`computeMatrix reference-point --regionsFileName /Users/Carlos/Desktop/Projects/Enhancer_Project/enhancers.intergenic.bed --scoreFileName /Users/Carlos/Dropbox/ChIP-Seq/hg19/old_data/Sample_H3K1/Tracks/H3K1.normalized.bigWig --referencePoint center --beforeRegionStartLength 1000 --afterRegionStartLength 1000 --numberOfProcessors "max" --outFileName computematrix.h3k1.refpoint --outFileSortedRegions sortedregions.h3k1.refpoint.bed`

Generate heatmap + metagene

H3K1
`heatmapper --matrixFile /Users/Carlos/Desktop/Projects/Enhancer_Project/computematrix.h3k1.refpoint --outFileName heatmapper.h3k1.refpoint.pdf --colorMap hot --heatmapHeight 15 --refPointLabel "Enhancer Center" --regionsLabel "Enhancers" --plotTitle "H3K1 Signal at Enhancers"`
