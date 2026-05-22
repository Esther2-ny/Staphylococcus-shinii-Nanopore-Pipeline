# Staphylococcus shinii Nanopore Pipeline
# Staphylococcus shinii Nanopore Sequencing & Assembly Pipeline

A complete, reproducible bioinformatics pipeline for processing raw long-read sequencing data from an Oxford Nanopore platform to species identification and reference genome validation.

##  Project Overview & Dataset
- **Sample ID:** Barcode02
- **Raw Input:** Split Nanopore FASTQ pass files (5,630 raw reads total)
- **Organism Identified:** *Staphylococcus shinii* (Novel, non-pathogenic bacterial species)
- **Assembly Profile:** Reconstructed 2.7 Million base pair genome across 32 continuous contigs.
- **Validation Audit:** Coordinate alignment mapped 5,554 reads successfully, verifying a near ~100% true mapping match to the official NCBI reference genome.

##  Pipeline Roadmap & Tools Used

### Phase 1: Environment Setup & Pre-processing
- **Environment Bridging:** WSL2 (Windows Subsystem for Linux) running Ubuntu to manage Linux-native tools over shared Windows drives.
- **Package Management:** Conda environments (`trimming`, `assembly`) used to prevent conflicting system and Python dependencies.
- **File Consolidation:** Merged split-run files using native Linux stream processing (`cat`).

### Phase 2: Read Quality Control & Trimming
- **Tool:** `Porechop`
- **Action:** Scanned long-reads to locate and cleanly trim down synthetic chemical adapters and native sequencing barcodes off over 3,000 biological reads.

### Phase 3: De Novo Genome Assembly
- **Tool:** `Flye`
- **Action:** Executed de novo structural assembly by mathematically overlapping matching long-read sequence ends, producing a final `assembly.fasta` sequence blueprint.

### Phase 4: Taxonomic Species Identification
- **Tool:** `NCBI BLAST` (Global Public Sequence Repository)
- **Action:** Cross-matched local contigs against public sequence databases. Found a definitive hit to *Staphylococcus shinii* (Identity: 93.11%, E-value: 0.0), matching known chromosomal and structural plasmid rings.

### Phase 5: Reference Mapping & Sorting
- **Tools:** `Minimap2` & `Samtools`
- **Action:** Aligned trimmed reads against the official downloaded NCBI *Staphylococcus shinii* reference sequence (`minimap2`), compressed and indexed coordinate files to highly structured, sorted binary alignment configurations (`samtools`).


*Environments used to build this pipeline are documented explicitly within the included `.yml` package configuration sheets.*

