


# Bulk RNA-seq

<div class = "warning">
This chapter is in a beta stage. If you wish to contribute, please [go to this form](https://forms.gle/dqYgmKH8XXE2ohwD9) or our [GitHub page](https://github.com/fhdsl/Choosing_Genomics_Tools).
</div>


## Learning Objectives

![](resources/images/10a-bulk-RNA-seq_files/figure-docx//1YwxXy2rnUgbx_7B7ENH9wpDX-j6JpJz6lGVzOkjo0qY_g12890ae15d7_0_56.png){width=100%}

## Where RNA-seq data comes from

![](resources/images/10a-bulk-RNA-seq_files/figure-docx//1YwxXy2rnUgbx_7B7ENH9wpDX-j6JpJz6lGVzOkjo0qY_g142c259a793_0_5.png){width=100%}

## RNA-seq workflow

In a very general sense, RNA-seq workflows involves first quantification/alignment. You will also need to conduct quality control steps that check the quality of the sequencing done. You may also want to trim and filter out data that is not trustworthy. After you have a set of reliable data, you need to normalize your data. After data has been normalized you are ready to conduct your downstream analyses. This will be highly dependent on the original goals and questions of your experiment. It may include dimension reduction, differential expression, or any number of other analyses.

![](resources/images/10a-bulk-RNA-seq_files/figure-docx//1YwxXy2rnUgbx_7B7ENH9wpDX-j6JpJz6lGVzOkjo0qY_g161687fdf93_0_23.png){width=100%}

In this chapter we will highlight some of the more popular RNA-seq tools, that are generally suitable for most experiment data but there is no "one size fits all" for computational analysis of RNA-seq data [@Conesa2016]. You may find tools out there that better suit your needs than the ones we discuss here.

## RNA-seq data **strengths**  

- RNA-seq can give you an idea of the transcriptional activity of a sample.
- RNA-seq has a more dynamic range of quantification than gene expression microarrays are able to measure.
- RNA-seq is able to be used for transcript discovery unlike gene expression microarrays.

## RNA-seq data **limitations**  

RNA-seq suffers from a lot of the common sequence biases which are further worsened by PCR amplification steps. We discussed some of the sequence biases in the [previous sequencing chapter]().

![](resources/images/10a-bulk-RNA-seq_files/figure-docx//1YwxXy2rnUgbx_7B7ENH9wpDX-j6JpJz6lGVzOkjo0qY_g142e3de7ce8_0_19.png){width=100%}

These biases are nicely covered in [this blog by Mike Love](https://mikelove.wordpress.com/2016/09/26/rna-seq-fragment-sequence-bias/) and we'll summarize them here:

- **Fragment length**: Longer transcripts are more likely to be identified than shorter transcripts because there's more material to pull from.  
- **Positional bias**: 3' ends of transcripts are more likely to be sequenced due to faster degradation of the 5' end.
- **Fragment sequence bias**: The complexity and GC content of a sequence influences how often primers will bind to it (which influences PCR amplification steps as well as the sequencing itself).
- **Read start bias**: Certain reads are more likely to be bound by random hexamer primers than others.

_Main Takeaway_: When looking for tools, you will want to see if the algorithms or options available attempt to account for these biases in some way.

![](resources/images/10a-bulk-RNA-seq_files/figure-docx//1YwxXy2rnUgbx_7B7ENH9wpDX-j6JpJz6lGVzOkjo0qY_g15bed4cad37_396_65.png){width=100%}

## RNA-seq data considerations

### Ribo minus vs poly A selection

Most of the RNA in the cell is not mRNA or noncoding RNAs of interest, but instead loads of ribosomal RNA a. So before you can prepare and sequence your data you need to isolate the RNAs to those you are interested in. There are two major methods to do this:

- **Poly A selection** - Keep only RNAs that have poly A tails -- remember that mRNAs and some kinds of noncoding RNAs have poly A tails added to them after they are transcribed. A drawback of this method is that transcripts that are not generally polyadenylated: microRNAs, snoRNAs, certain long noncoding RNAs, or immature transcripts will be discarded. There is also generally a worse 3' bias with this method since you are selecting based on poly A tails on the 3' end.
- **Ribo-minus** - Subtract all the ribosomal RNA and be left with an RNA pool of interest. A drawback of this method is that you will need to use greater sequencing depths than you would with poly A selection (because there is more material in your resulting transcript pool).

[This blog by Sitools Biotech does a good summary](https://blog.sitoolsbiotech.com/2019/08/ribo-depletion-rna-seq-ribosomal-rna-depletion-method-works-best/) of the pros and cons of either selection method.

![](resources/images/10a-bulk-RNA-seq_files/figure-docx//1YwxXy2rnUgbx_7B7ENH9wpDX-j6JpJz6lGVzOkjo0qY_g15bed4cad37_396_47.png){width=100%}

### Transcriptome mapping

How do you know which read belongs to which transcript? This is where alignment comes into play for RNA-seq There are two major approaches we will discuss with examples of tools that employ them.

- **Traditional aligners** - Align your data to a reference using standard alignment algorithms. Can be very computationally intensive. Traditional alignment is the original approach to alignment which takes each read and finds where and how in the genome/transcriptome it aligns. If you are interested in identifying the intracacies of different splices and their boundaries, you may need to use one of these traditional alignment methods. But for common quantification purposes, you may want to look into pseudo alignment to save you time.
_Examples of traditional aligners_:   
  - [STAR](https://github.com/alexdobin/STAR/blob/master/doc/STARmanual.pdf)
  - [HISAT2](http://daehwankimlab.github.io/hisat2/manual/)

- This blog compares some of the traditional alignment tools

- [**Pseudo aligners**](https://tinyheero.github.io/2015/09/02/pseudoalignments-kallisto.html) - much faster and the trade off for accuracy is often negligible (but as always, this is likely dependent on the data you are using). The biggest drawback to pseudoaligners is that if you care about local alignment (e.g. perhaps where splice boundaries occur) instead of just transcript identification then a traditional alignment may be better for your purposes. These pseudo aligners often include a verification step where they compare a subset of the data to its performance to a traditional aligner (and for most purposes they usually perform well). Pseudo aligners can potentially save you hours/days/weeks of processing time as compared to traditional aligners so are worth looking into.
_Examples of pseudo aligners_:   
  - [Salmon](https://salmon.readthedocs.io/en/latest/salmon.html#using-salmon)
  - [Kallisto](https://pachterlab.github.io/kallisto/)

- **Reference free assembly** - The first two methods we've discussed employ aligning to a reference genome or transcriptome. But alternatively, if you are much more interested in transcript identification or you are working with a model organism that doesn't have a well characterized reference genome/transcriptome, then de novo assembly is another approach to take. As you may suspect, this is the most computationally demanding approach and also requires deeper sequencing depth than alignment to a reference. But depending on your goals, this may be your preferred option.

These strategies are discussed at greater length [in this excellent manuscript by Conesa et al, 2016](https://genomebiology.biomedcentral.com/articles/10.1186/s13059-016-0881-8).

![](resources/images/10a-bulk-RNA-seq_files/figure-docx//1YwxXy2rnUgbx_7B7ENH9wpDX-j6JpJz6lGVzOkjo0qY_g15bed4cad37_396_72.png){width=100%}

### Abundance measures

If your RNA-seq data has already been processed, it may have abundance measure reported with it already. But there are various types of abundance measures used -- what do they represent?

- **raw counts** - this is a raw number of how many times a transcript was counted in a sample.

Two considerations to think of:  
1. **Library sizes**: Raw counts does not account for differences between samples' library sizes. In other words, how many reads were obtained from each sample? Because library sizes are not perfectly equal amongst samples and not necessarily biologically relevant, its important to account for this if you wish to compare different samples in your set.  
2. **Gene length**: Raw counts also do not account for differences in gene length (remember how we discussed longer transcripts are more likely to be counted).

Because of these items, some sort of transformation needs to be done on the raw counts before you can interpret your data.

These other abundance measures attempt to account for library sizes and gene length. [This blog and video by StatQuest](https://www.rna-seqblog.com/rpkm-fpkm-and-tpm-clearly-explained/) does an excellent job summarizing the differences between these quantifications and we will quote from them:

- **Reads per kilobase million (RPKM)**  

> 1. Count up the total reads in a sample and divide that number by 1,000,000 – this is our “per million” scaling factor.
2. Divide the read counts by the “per million” scaling factor. This normalizes for sequencing depth, giving you reads per million (RPM)
3. Divide the RPM values by the length of the gene, in kilobases. This gives you RPKM.

- **Fragments per kilobase million (FPKM)**  

> FPKM is very similar to RPKM. RPKM was made for single-end RNA-seq, where every read corresponded to a single fragment that was sequenced. FPKM was made for paired-end RNA-seq. With paired-end RNA-seq, two reads can correspond to a single fragment, or, if one read in the pair did not map, one read can correspond to a single fragment. The only difference between RPKM and FPKM is that FPKM takes into account that two reads can map to one fragment (and so it doesn’t count this fragment twice).

- **Transcripts per million (TPM)**  

> 1. Divide the read counts by the length of each gene in kilobases. This gives you reads per kilobase (RPK).
2. Count up all the RPK values in a sample and divide this number by 1,000,000. This is your “per million” scaling factor.
3. Divide the RPK values by the “per million” scaling factor. This gives you TPM.

TPM has gained a popularity in recent years because it is more intuitive to understand:

> When you use TPM, the sum of all TPMs in each sample are the same. This makes it easier to compare the proportion of reads that mapped to a gene in each sample. In contrast, with RPKM and FPKM, the sum of the normalized reads in each sample may be different, and this makes it harder to compare samples directly.

![](resources/images/10a-bulk-RNA-seq_files/figure-docx//1YwxXy2rnUgbx_7B7ENH9wpDX-j6JpJz6lGVzOkjo0qY_g15bed4cad37_396_59.png){width=100%}

### RNA-seq downstream analysis tools

![](resources/images/10a-bulk-RNA-seq_files/figure-docx//1YwxXy2rnUgbx_7B7ENH9wpDX-j6JpJz6lGVzOkjo0qY_g15bed4cad37_396_80.png){width=100%}

- [ComplexHeatmap](https://bioconductor.org/packages/release/bioc/html/ComplexHeatmap.html#:~:text=Complex%20heatmaps%20are%20efficient%20to,and%20supports%20various%20annotation%20graphics.) is great for visualizations
- [DESEq2](https://www.bioconductor.org/packages/release/bioc/html/DESeq2.html) and [edgeR](https://www.bioconductor.org/packages/release/bioc/html/edgeR.html) are great for differential expression analyses.
- [CTAT](https://github.com/NCIP/Trinity_CTAT/wiki) - Using RNA-seq as input, CTAT modules enable detection of mutations, fusion transcripts, copy number aberrations, cancer-specific splicing aberrations, and oncogenic viruses including insertions into the human genome.
- [Gene Set Enrichment Analysis (GSEA)](https://www.gsea-msigdb.org/gsea/index.jsp) is a method to identify the coordinate activation or repression of groups of genes that share common biological functions, pathways, chromosomal locations, or regulation, thereby distinguishing even subtle differences between phenotypes or cellular states.
- [Gene Pattern's RNA-seq tutorials](https://www.genepattern.org/rna-seq-analysis#gsc.tab=0) - an open software environment providing access to hundreds of tools for the analysis and visualization of genomic data. 

## Visualization GUI tools

- [WebMeV](https://webmev.tm4.org) uniquely provides a user-friendly, intuitive, interactive interface to processed analytical data uses cloud-computing elasticity for computationally intensive analyses and is compatible with single cell or bulk RNA-seq input data.
- [UCSC Xena](http://xena.ucsc.edu/) is a web-based visualization tool for multi-omic data and associated clinical and phenotypic annotations. It can be used with single cell RNA-seq data.
- [Integrative Genomics Viewer (IGV)](https://software.broadinstitute.org/software/igv/) is a track-based browser for interactively exploring genomic data mapped to a reference genome.
- [Network Data Exchange (NDEx)](https://www.ndexbio.org/#/) is a project that provides an open-source framework where scientists and organizations can store, share and publish biological network knowledge.

## RNA-seq data resources

- [ARCHS4](https://maayanlab.cloud/archs4/) (All RNA-seq and ChIP-seq sample and signature search) is a resource that provides access to gene and transcript counts uniformly processed from all human and mouse RNA-seq experiments from GEO and SRA.
- [Refine.bio](https://www.refine.bio/) - a repository of uniformly processed and normalized, ready-to-use transcriptome data from publicly available sources.

## More reading about RNA-seq data

- [Refine.bio's introduction to RNA-seq](https://alexslemonade.github.io/refinebio-examples/03-rnaseq/00-intro-to-rnaseq.html)
- [StatQuest: A gentle introduction to RNA-seq](https://www.youtube.com/watch?v=tlf6wYJrwKY) [@Starmer2017-rnaseq].
- [A general background on the wet lab methods of RNA-seq](https://bitesizebio.com/13542/what-everyone-should-know-about-rna-seq/) [@Hadfield2016].
- [Modeling of RNA-seq fragment sequence bias reduces systematic errors in transcript abundance estimation](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC5143225/) [@Love2016].
- [Mike Love blog post about sequencing biases]( https://mikelove.wordpress.com/2016/09/26/rna-seq-fragment-sequence-bias/) [@bias-blog]
- [Biases in Illumina transcriptome sequencing caused by random hexamer priming](https://pdfs.semanticscholar.org/9d16/997f5de72d6c606fef3d673db70e5d1d8e1e.pdf?_ga=2.131436679.965169313.1600175795-124991789.1600175795) [@Hansen2010].
- [Computation for RNA-seq and ChIP-seq studies](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4121056/) [@Pepke2009].