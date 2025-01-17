


# Spatial transcriptomics

<div class = "warning">
This chapter chapter has currently been written by ChatGPT and has not been verified by experts. We need help writing and reviewing it! If you wish to contribute, please [go to this form](https://forms.gle/dqYgmKH8XXE2ohwD9) or our [GitHub page](https://github.com/fhdsl/Choosing_Genomics_Tools).
</div>

## Learning Objectives

![](resources/images/10c-spatial-transcriptomics_files/figure-docx//1YwxXy2rnUgbx_7B7ENH9wpDX-j6JpJz6lGVzOkjo0qY_g15bed4cad37_396_1.png){width=100%}

## What are the goals of spatial transcriptomic analysis?

Characterize Spatial Gene Expression Patterns: One primary goal of spatial transcriptomic analysis is to characterize gene expression patterns within a tissue or cellular context. By examining gene expression profiles at different locations within the tissue, researchers aim to identify spatially regulated gene expression patterns and understand how gene expression varies across different regions.

1. **Identify Cell Types and Subpopulations:** Spatial transcriptomic analysis helps in the identification and characterization of different cell types and subpopulations within a tissue sample. By examining the gene expression profiles at a spatial resolution, researchers can differentiate and define distinct cell types based on their unique transcriptional signatures. This information contributes to the understanding of cellular heterogeneity and cellular composition within the tissue.
1. **Uncover Spatially Regulated Biological Processes:** Another goal of spatial transcriptomic analysis is to uncover spatially regulated biological processes. By examining gene expression patterns within the tissue context, researchers can identify spatially restricted expression of genes involved in specific biological processes, such as tissue gradients, morphogenesis, cell differentiation, or signaling pathways. This knowledge aids in understanding how spatial organization influences cellular behavior and tissue function.
1. **Investigate Cell-Cell Interactions and Signaling Networks:** Spatial transcriptomic analysis enables the investigation of cell-cell interactions and signaling networks within a tissue. By examining the gene expression profiles of neighboring cells, researchers can identify genes that are specifically expressed in close proximity, indicating potential cell-cell interactions and communication. This information helps in deciphering cellular communication networks and understanding the functional relationships between cells.
1. **Integrate Spatial Transcriptomics with Anatomical or Imaging Data:** Spatial transcriptomic analysis aims to integrate gene expression data with anatomical or imaging data, such as histological images or imaging modalities like fluorescence microscopy. By overlaying gene expression information onto the tissue architecture, researchers can correlate gene expression patterns with tissue morphology, cellular structures, or specific anatomical regions. This integration enhances the interpretation of spatial transcriptomic data and provides a more comprehensive understanding of gene expression within the tissue.
1. **Generate Hypotheses and Identify Biomarkers:** Spatial transcriptomic analysis can generate hypotheses and identify potential biomarkers associated with specific tissue functions or disease states. By examining gene expression patterns in the spatial context, researchers can discover spatially restricted gene signatures and potential diagnostic or prognostic markers. This knowledge has implications for disease research, precision medicine, and therapeutic targeting.

## Spatial transcriptomic general workflow overview

Here are the basic steps involved in collecting spatial transcriptomic data:

1. **Sample Preparation:** The first step is to prepare the tissue sample for spatial transcriptomic analysis. This involves obtaining the tissue of interest, which could be a section from a biopsy, a thin slice from a tissue block, or a whole-mount tissue. The sample should be properly preserved and stabilized to maintain the integrity of RNA molecules.

1. **Spatially Resolved Capture of RNA Molecules:** In this step, the tissue sample is typically placed on a solid substrate, such as a glass slide or a microarray chip. One common approach is to use spatially barcoded arrays or grids, where each region corresponds to a specific spatial location. Alternatively, techniques like in situ sequencing or imaging-based methods can be used. These approaches allow the capture of RNA molecules while retaining spatial information.

1. **RNA Extraction and Amplification:** After spatial capture, the captured RNA molecules need to be extracted and amplified to generate sufficient material for downstream analysis. This step involves lysing the cells, extracting the RNA, and performing reverse transcription to convert RNA into complementary DNA (cDNA). Amplification methods such as PCR or in vitro transcription (IVT) are employed to generate amplified cDNA libraries.

1. **Library Preparation:** The amplified cDNA libraries are then prepared for sequencing. This involves adding specific sequencing adapters and barcodes to each library, which enable sample multiplexing and identification during sequencing.

1. **Sequencing:** The prepared libraries are subjected to high-throughput sequencing using platforms like Illumina or Ion Torrent. The choice of sequencing platform depends on the desired read length, throughput, and cost considerations.

1. **Data Analysis:** After sequencing, the generated data undergoes bioinformatics analysis. This typically includes preprocessing steps such as read alignment or mapping to a reference genome, removing duplicate reads, and quantifying gene expression levels. The spatial coordinates associated with each read are also considered for spatial analysis, which involves assigning gene expression profiles to specific locations within the tissue.

1. **Visualization and Interpretation:** The final step involves visualizing and interpreting the spatial transcriptomic data. Various tools and algorithms are available for spatial visualization, such as generating heatmaps, spatial expression plots, or clustering analysis. The data can be integrated with anatomical or imaging data to gain further insights into cellular organization and interactions within the tissue.

## Spatial transcriptomic data **strengths**:

- **Preservation of Spatial Information:** Spatial transcriptomics allows the investigation of gene expression patterns within the context of tissue or cellular spatial organization. By preserving the spatial information of RNA molecules, it provides insights into how gene expression varies across different regions within a tissue sample.
- **Identification of Cell Types and Subpopulations:** Spatial transcriptomics enables the identification and characterization of different cell types and subpopulations within a tissue sample based on their unique gene expression profiles. This information helps in understanding cellular heterogeneity and cell-cell interactions within the tissue.
- **Visualization of Gene Expression Patterns:** By generating spatially resolved gene expression data, spatial transcriptomics allows for the visualization of gene expression patterns across the tissue sample. This visualization can be in the form of heatmaps, spatial expression plots, or spatially resolved gene expression atlases, providing a comprehensive view of gene expression within the tissue.
- **Integration with Anatomical and Imaging Data:** Spatial transcriptomics data can be integrated with anatomical or imaging data, such as histological images or imaging modalities like fluorescence microscopy. This integration enhances the interpretation of spatial transcriptomic data by correlating gene expression patterns with tissue morphology or specific cellular structures.
- **Discovery of Novel Cell-Cell Interactions and Signaling Pathways:** By examining gene expression profiles in the spatial context, spatial transcriptomics can uncover novel cell-cell interactions and signaling pathways within a tissue. It allows the identification of genes that are specifically expressed in close proximity to each other, revealing potential regulatory relationships and functional interactions between cells.
- **Exploration of Spatially Regulated Biological Processes:** Spatial transcriptomics enables the investigation of spatially regulated biological processes, such as tissue gradients or developmental processes occurring in specific regions. It provides insights into spatially restricted gene expression patterns associated with tissue patterning, morphogenesis, or cellular differentiation.
- **Hypothesis Generation and Biomarker Discovery:** Spatial transcriptomic analysis can generate hypotheses and identify potential biomarkers related to specific tissue functions or disease states. By linking gene expression patterns to tissue organization and pathology, spatial transcriptomics facilitates the discovery of spatially restricted gene signatures and potential diagnostic or prognostic markers.

## Spatial transcriptomic data **weaknesses**:

- **Limited Spatial Resolution:** Spatial transcriptomic techniques have a finite spatial resolution, which determines the level of detail at which gene expression patterns can be analyzed. The resolution is influenced by factors such as the size of capture spots or the resolution of imaging techniques. Obtaining fine-grained spatial information may be challenging, especially in complex tissues or samples with high cellular density.
- **Technical Variability and Experimental Artifacts:** Spatial transcriptomic analysis involves multiple experimental steps, including tissue processing, capture techniques, and sequencing. Each step introduces technical variability and potential experimental artifacts, which can impact the accuracy and reproducibility of the results. Controlling and minimizing these sources of variation is crucial but can be challenging.
- **Limited Coverage of Transcripts:** Spatial transcriptomic methods often have limited coverage of the entire transcriptome. The capture techniques used may bias the representation of certain RNA molecules or favor highly expressed transcripts, potentially leading to a biased view of gene expression. Additionally, spatial transcriptomic methods may have limitations in capturing non-polyadenylated RNAs or low-abundance transcripts.
- **Complex Data Analysis:** Analyzing spatial transcriptomic data requires advanced computational methods and expertise. Data analysis involves multiple steps, including image processing, spatial registration, normalization, and interpretation. The complexity of the data and the need for specialized bioinformatics tools and pipelines can pose challenges, particularly for researchers without extensive computational skills.
- **Validation and Integration Challenges:** Spatial transcriptomic analysis generates hypotheses and provides spatially resolved gene expression information. However, validating the functional significance of identified gene expression patterns or cellular interactions may require additional experiments or techniques. Integrating spatial transcriptomic data with other omics data or imaging modalities can also be complex and may require careful data integration strategies.
- **Cost and Time Considerations:** Spatial transcriptomic analysis can be relatively expensive and time-consuming compared to traditional transcriptomic techniques. The specialized protocols, reagents, and instrumentation required can add to the cost of the analysis. Moreover, the data generation and analysis processes can be time-intensive, which may limit the scalability of studies involving large sample sizes.
- **Limited Accessibility of Techniques:** Some spatial transcriptomic techniques may have limited availability, accessibility, or may require specialized equipment or expertise. This can restrict their widespread use and accessibility to researchers who do not have access to the necessary resources or infrastructure.


### Tools for spatial transcriptomics

#### Seurat:

- **Pros:** Seurat is a widely used R package that offers a comprehensive suite of tools for spatial transcriptomic analysis. It provides a variety of functions for data preprocessing, dimensionality reduction, clustering, and visualization. Seurat has a large user community, extensive documentation, and tutorials, making it accessible to researchers.
- **Cons:** Seurat can be memory-intensive, particularly when working with large datasets. It may require familiarity with R programming and bioinformatics concepts for effective use. Additionally, Seurat's performance can depend on the specific computational resources available.

#### Scanpy:

- **Pros:** Scanpy is a Python-based library specifically designed for single-cell and spatial transcriptomic analysis. It offers a range of functionalities for data preprocessing, clustering, trajectory analysis, and visualization. Scanpy is known for its scalability, efficiency, and flexibility. It integrates well with other Python libraries and frameworks, making it suitable for integration with other analysis pipelines.
- **Cons:** Similar to Seurat, Scanpy may require some familiarity with Python programming and bioinformatics concepts. Users without prior programming experience may need to invest time in learning Python.

#### spaceranger:

- **Pros:** spaceranger is a software package developed by 10x Genomics specifically for processing and analyzing spatial transcriptomic data generated by their platform. It provides a streamlined workflow for processing raw data, including image processing, spot calling, and counting transcripts. spaceranger offers integration with the Seurat R package, enabling downstream analysis using Seurat's extensive tools.
- **Cons:** spaceranger is optimized for 10x Genomics data and may have limited compatibility with other spatial transcriptomic platforms. It may not offer the same level of flexibility as more general-purpose tools like Seurat or Scanpy.

#### ST Pipeline:

- **Pros:** ST Pipeline is an open-source bioinformatics pipeline developed by the Spatial Transcriptomics consortium. It provides a complete workflow for spatial transcriptomic data analysis, including preprocessing, normalization, spot detection, and visualization. ST Pipeline supports various spatial transcriptomic platforms, making it versatile.
- **Cons:** ST Pipeline may require some command-line proficiency and familiarity with Linux environments. Users may need to invest time in setting up the pipeline and configuring parameters based on their specific datasets and platforms.

#### SpatialDE:

- **Pros:** SpatialDE is a Python package designed for detecting spatially variable genes from spatial transcriptomic data. It offers statistical methods to identify genes that exhibit spatial heterogeneity in expression across the tissue. SpatialDE provides a straightforward implementation for identifying spatially variable genes and their spatial patterns.
- **Cons:** SpatialDE focuses on the identification of spatially variable genes and may not provide a comprehensive set of tools for the entire spatial transcriptomic analysis pipeline. Additional tools may be required for preprocessing, visualization, and downstream analysis.

## More tools and tutorials regarding spatial transcriptomics

- [Analysis, visualization, and integration of spatial datasets with Seurat](https://satijalab.org/seurat/articles/spatial_vignette.html)
- [Sheffield Bioinformatics tutorial for spatial transcriptomics](https://github.com/sheffield-bioinformatics-core/spatial_transcriptomics_tutorial)
- [Theis Lab SCOG workshop materials for spatial transcriptomics](https://github.com/theislab/spatial_scog_workshop_2022)
