# Six-Frame Translation and ORF Finder

A beginner-to-intermediate dry-lab bioinformatics project for exploring possible coding regions in a DNA sequence using six-frame translation and simple ORF detection.

## Project Overview

An open reading frame (ORF) is a sequence region that can potentially encode a protein. This project demonstrates the basic computational steps used to examine a DNA sequence in all six possible reading frames.

The workflow is:

**DNA sequence → validation → reverse complement → six reading frames → translation → candidate ORF detection → nucleotide coordinates → Biopython validation**

The project uses the human **HBB (hemoglobin beta)** coding sequence as a controlled test case.

> **Important:** This is an educational ORF-finding pipeline. A candidate ORF is not automatically a confirmed functional gene.

## Objectives

- Implement a standard genetic code in Python.
- Validate a DNA sequence before analysis.
- Generate the reverse-complement sequence.
- Translate the three forward and three reverse-complement reading frames.
- Detect simple ATG-to-stop candidate ORFs.
- Record nucleotide and amino-acid lengths.
- Record start and end nucleotide coordinates.
- Validate the expected HBB translation using Biopython.
- Practice interpreting computational results without overclaiming biological function.

## Reading Frames

The six reading frames examined are:

- `+1`, `+2`, `+3` — forward strand
- `-1`, `-2`, `-3` — reverse-complement strand

For each frame, the sequence is divided into complete codons and translated using the standard genetic code.

## ORF Detection Logic

The current implementation uses a simple rule:

1. Search a reading frame for an `ATG` start codon.
2. Translate codons in the same reading frame.
3. Stop at the first in-frame stop codon (`TAA`, `TAG`, or `TGA`).
4. Keep complete start-to-stop candidates that meet the selected minimum peptide length.
5. Report their strand, frame, nucleotide coordinates, nucleotide length, peptide length, start codon, stop codon, and peptide sequence.

The minimum length is used as a simple filtering criterion for this learning project. It is **not** a biological proof of gene function.

## Test Dataset: Human HBB

The notebook uses a known human **HBB** coding sequence as a controlled test case.

The expected HBB coding frame is `+1`, and the custom translation is compared with Biopython to check the translation result.

This example is intended for learning and validation of the pipeline rather than novel gene discovery.

## Tools and Technologies

- **Python 3**
- **Jupyter Notebook**
- **Biopython**
- Basic DNA sequence analysis
- Six-frame translation
- ORF detection

## Repository Contents

```text
orf-finder/
│
├── orf_finder_pipeline_v2.ipynb
└── README.md
```

## How to Run

### 1. Clone the repository

```bash
git clone https://github.com/Junaidomics/six-frame-orf-finder.git
cd six-frame-orf-finder
```

### 2. Install the required package

```bash
pip install biopython
```

### 3. Open the notebook

```bash
jupyter notebook orf_finder_pipeline_v2.ipynb
```

Run the cells from top to bottom.

## Expected Analysis

The notebook produces a table of candidate ORFs containing:

| Field | Description |
|---|---|
| Strand | Forward or reverse |
| Frame | One of the six reading frames |
| Start | Start nucleotide position |
| End | End nucleotide position |
| Length (nt) | ORF nucleotide length |
| Length (aa) | Translated peptide length |
| Start codon | ORF start codon |
| Stop codon | ORF termination codon |

The known HBB `+1` translation is also compared directly with the Biopython translation.

## Validation

The project includes a custom translation implementation and an independent Biopython comparison for the expected HBB coding frame.

A matching result supports the correctness of the translation step for the tested sequence.

It should not be interpreted as independent validation of every aspect of the ORF detection algorithm.

## Limitations

This is a learning-focused implementation and has several limitations:

- It uses a simple ATG-to-stop ORF definition.
- It does not perform full gene prediction.
- It does not score ORFs using biological evidence.
- It does not perform protein similarity searches.
- It does not perform functional annotation.
- Alternative start codons are not considered.
- Ambiguous bases may be translated as `X`.
- Reverse-strand coordinates are reported relative to the reverse-complement sequence rather than converted to original genomic coordinates.

These limitations are intentional and define the current scope of the project.

## Future Development

Possible extensions include:

- Applying the pipeline to unknown FASTA sequences.
- Adding FASTA file input instead of using a hard-coded test sequence.
- Improving reverse-strand genomic coordinate handling.
- Adding protein similarity-search evidence.
- Integrating sequence annotation.
- Comparing candidate ORFs using additional biological evidence.
- Expanding the workflow toward a more reproducible genomics pipeline.

## Skills Demonstrated

This project demonstrates practice with:

- Python functions and dictionaries
- DNA sequence validation
- Reverse-complement generation
- Six-frame translation
- Basic ORF detection
- Sequence coordinates
- Biopython
- Computational validation
- Biological interpretation
- Documenting limitations and reproducibility

## Author

**Muhammad Junaid**  
BS Biotechnology | Bioinformatics & Dry-Lab Learning

This project was developed as part of a growing computational biology portfolio focused on building practical skills in sequence analysis and genomics.

## Disclaimer

This repository is intended for educational and portfolio purposes. The ORFs identified by this simple pipeline are computational candidates and should not be interpreted as experimentally confirmed genes or functional annotations.
