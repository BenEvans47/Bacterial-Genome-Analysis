# Bacterial Genome Analysis

Bacterial genome analysis involves the use of bioinformatic methods to examine and interpret genomic sequence data. Advances in whole-genome sequencing technologies have made it possible to rapidly generate complete or draft bacterial genomes, providing valuable insights into the biology, evolution, and epidemiology of bacterial species.

Genome analyses are performed to investigate a wide range of biological questions, including the identification of genes, antimicrobial resistance determinants, virulence factors, metabolic capabilities, and evolutionary relationships between strains. These analyses are widely used in research, clinical microbiology, public health surveillance, and outbreak investigations.

A typical bacterial genome analysis pipeline begins with the acquisition of sequencing data, followed by quality control and genome assembly. The assembled genome is then annotated to identify genes and predict their functions. Subsequent analyses may include strain typing, detection of antimicrobial resistance and virulence genes, comparative genomics, and phylogenetic analysis. Results are often visualised using genome browsers and other bioinformatic tools to facilitate interpretation.

Together, these approaches transform raw sequence data into biologically meaningful information, enabling researchers to better understand bacterial diversity, evolution, and pathogenic potential.

#

This module follows on from the 'Mammalian sequence analysis' module (https://github.com/UEA-Cancer-Genetics-Lab/MHC_RNA-seq_Workshop), which covered:

1.	The terminal and bash
2.	R
3.	FastQ files
4.	QC of fastQ files using FastQC
5.	Aligning reads to a reference
6.	RNAseq read counts
7.	Differential gene expression
8.	Functional analyses (KEGG, GO, Reactome)

This module will complement these topics and skills, and will focus on the following:

1. Downloading a genome from NCBI
2. Genome annotation with Bakta (https://bakta.computational.bio/)
3. Typing with MLST (https://genepi.food.dtu.dk/mlstfinder)
4. Genome browsers
5. Identifying specific genome features
6. Identifying protein motifs (uniprot - alphafold)


## NCBI Datasets CLI on Windows

The National Center for Biotechnology Information (NCBI) Genomes database is a comprehensive public repository of genome sequence data from a wide range of organisms, including bacteria, archaea, viruses, and eukaryotes. It provides access to assembled genome sequences, associated annotations, metadata, and supporting information submitted by researchers worldwide.

The database serves as an important resource for genomic research by enabling users to search for, view, and download genome assemblies and their annotations. For bacterial genomics, the NCBI Genomes database facilitates comparative analyses, strain typing, gene identification, and evolutionary studies by providing access to both reference and newly sequenced genomes.

In addition to genome sequences, NCBI integrates related resources such as gene, protein, taxonomy, and literature databases, allowing researchers to explore genomic data within a broader biological context. The availability of standardised genome records and command-line tools for data retrieval has made the NCBI Genomes database a widely used resource in modern bioinformatics and microbial genomics.

### Activity

1. **Download the Datasets executable**
   - Go to: [NCBI Datasets CLI Downloads](https://www.ncbi.nlm.nih.gov/datasets/docs/v1/download-and-install/)
   - Download the Windows version (`datasets.exe`)
   - Place it somewhere convenient, for example a working directory, your downloads folder, or add it to your PATH

2. **Test the installation**
   - Open Command Prompt:
   ```
   datasets version
   ```
   or in your working directory/downloads folder
   ```
   .\datasets version
   ```

3. **Download a genome**
   - For example, the human reference genome:
   ```
   datasets download genome accession GCF_000001405.40
   ```
   - This creates: `ncbi_dataset.zip`
   - We are going to download `GCF_000021245.2`
   ```
   datasets download genome accession GCF_000021245.2
   ```

4. **Extract the ZIP file**
   - Using built-in PowerShell from Command Prompt:
   ```powershell
   powershell -command "Expand-Archive -Path ncbi_dataset.zip -DestinationPath genome"
   ```
   - You can then find the genome as a FASTA file:
   ```
   genome\ncbi_dataset\data\GCF_000021245.2\GCF_000021245.2_ASM2124v2_genomic.fna
   ```

5. **Alternative approach: Download by species name**  
   To download the *Acinetobacter baumannii* reference genome:
   ```
   datasets download genome taxon "Acinetobacter baumannii" --reference
   ```
   or to download all *Acinetobacter baumannii* genomes:  (WANINING: do not actually run this command - it is provided for example only)
   ```
   datasets download genome taxon "Acinetobacter baumannii"
   ```

## Genome Annotation

Bacterial genome annotation is the process of identifying genes and other biologically relevant features within a genome sequence and assigning functions to them. Following genome assembly, annotation converts a raw DNA sequence into a biologically interpretable resource by locating coding sequences, RNA genes, and other genomic elements.

The main aim of genome annotation is to determine the genetic potential of an organism. Annotated genomes allow researchers to investigate metabolic pathways, antimicrobial resistance, virulence factors, and evolutionary relationships, making annotation an essential step in bacterial genomics.

Genome annotation typically consists of two stages: structural annotation and functional annotation. Structural annotation identifies features such as coding sequences (CDSs), transfer RNAs (tRNAs), and ribosomal RNAs (rRNAs). Functional annotation predicts the biological role of these features, usually through comparison with databases of previously characterised genes and proteins.

Different annotation programs use a range of approaches to perform these tasks. Gene prediction tools identify coding regions based on sequence characteristics such as start and stop codons and codon usage patterns. Functional annotation is commonly achieved through sequence similarity searches or the identification of conserved protein domains using profile-based methods.

Several annotation pipelines are widely used for bacterial genomes. Prokka provides rapid annotation using curated protein databases, while Bakta uses a large collection of validated protein sequences and identifiers. The NCBI Prokaryotic Genome Annotation Pipeline (PGAP) employs a highly curated reference database and standardised annotation methods. As different tools use different algorithms and databases, annotations may vary between pipelines, making tool selection an important consideration in genomic analyses.

### Activity

1. In your web browser, navigate to [Bakta](https://bakta.computational.bio/)
2. Upload your genome in FASTA format
3. What do you think the most appropriate settings to use might be?
4. Once you are happy with the settings press "Submit"

## Strain Typing

Bacterial strain typing is the process of distinguishing between different strains of the same bacterial species. While isolates may belong to the same species, they can differ significantly in characteristics such as virulence, antimicrobial resistance, and epidemiological origin. Strain typing is therefore an important tool in public health, clinical microbiology, and microbial ecology, enabling researchers to investigate disease outbreaks, track pathogen transmission, and study bacterial population structure.

A widely used method for bacterial strain typing is Multi-Locus Sequence Typing (MLST). MLST characterises isolates based on the DNA sequences of a small number of conserved housekeeping genes, typically seven. For each gene, unique sequence variants are assigned allele numbers, and the combination of allele numbers across all loci defines the isolate's Sequence Type (ST).

Because housekeeping genes evolve relatively slowly, MLST provides a standardised and highly reproducible method for comparing bacterial isolates between laboratories and across studies. The resulting sequence types can be compared against curated databases to identify related strains and infer evolutionary relationships. Although whole-genome sequencing now offers higher-resolution approaches to strain typing, MLST remains a widely used and valuable method due to its simplicity, portability, and extensive historical databases.

### Activity

1. In your web browser, navigate to [Galaxy](https://usegalaxy.eu/)
2. Upload your genome in FASTA format using the 'upload' button in the top left corner
3. In the 'Tools' menu, go to 'Annotation' > 'MLST'
4. Select your uploaded genome as the input file, then click 'Run tool'
5. Wait for the tool to finish running - you will see it on the right under the history tab. Once it turns green, it has finished.
6. Go to the [PubMLST site](https://pubmlst.org/bigsdb?db=pubmlst_abaumannii_seqdef&page=profiles)
7. Under 'Schemes', select 'MLST (Pasteur)'
8. Enter the allelic profile obtained from the output of the Galaxy MLST job, and click 'Search'

## Viewing Your Genome

Genome browsers are graphical tools that allow researchers to visualise and explore genomic data in an interactive manner. Rather than examining genome sequences and annotations as text files, genome browsers display genomic features such as genes, coding sequences, regulatory elements, and sequence variants along a reference genome, making complex datasets easier to interpret.

Genome browsers are useful because they provide a visual representation of the organisation and context of genomic features. Researchers can examine the location, orientation, and relationships between genes, assess annotation quality, and compare different datasets within the same genomic region. Many genome browsers also support the integration of additional data types, such as transcriptomic, proteomic, or comparative genomics data, allowing multiple layers of information to be analysed simultaneously.

As genome sequencing projects continue to generate increasingly large and complex datasets, genome browsers have become essential tools for genome exploration, annotation validation, and the interpretation of biological findings.

### Activity

1. In your web browser, navigate to [Proksee](https://proksee.ca/)
2. Upload your genome in FASTA format
3. Consider what you might you want to identify in your genome?
4. Annotate antibiotic resistance genes with the 'CARD Resistance Gene Identifier'. Add these to the genome map. Do you notice anything about the results?

## Identifying protein structure and function

A protein's function is closely linked to its structure, as the three-dimensional arrangement of amino acids determines how the protein interacts with other molecules and carries out its biological role. Consequently, analysing both protein sequence and structure is an important aspect of modern bioinformatics and molecular biology.
Protein structure and function analyses are used to predict the roles of newly identified proteins, identify conserved domains and functional motifs, investigate evolutionary relationships, and assess the potential effects of sequence variation. These analyses are particularly valuable when studying proteins that have not yet been experimentally characterised.
A key resource for protein analysis is the UniProt database, which provides a comprehensive collection of protein sequences and functional annotations. UniProt integrates information from experimental studies, computational predictions, and cross-references to other biological databases, making it a widely used resource for protein identification and functional interpretation. Combined with structural prediction and visualisation tools, databases such as UniProt enable researchers to gain deeper insights into protein biology and function.

### Activity

1.	In your web browser, navigate to UniProt BLAST
https://www.uniprot.org/blast
2.	Find the ‘oxa-23’ gene in the genome using your genome browser, and copy the nucleotide sequence.
3.	Paste the sequence into UniProt BLAST, and as the database select ‘UniProtKB with 3D structure predictions (AlphaFold)’

