# Hidden Markov Models: TPH1 Gene Search in the Gut Microbiome

A team project for the *Grammars, Automata and Biocomputers* course. The goal was to search metagenomic sequences from the human gut microbiome for the **TPH1** gene using profile Hidden Markov Models, and to compare this with a transformer-based approach.

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/NataliaKowal/Ukryte-modele-Markowa/blob/main/Gramatyki%2C_automaty_i_biokomputery.ipynb)

## Background

TPH1 encodes tryptophan hydroxylase, an enzyme that takes part in converting tryptophan into serotonin. TPH1 was chosen over TPH2, which has the same function, because TPH2 is found only in neurons.

Reference sequences from NCBI:

- Protein: [NP_004170](https://www.ncbi.nlm.nih.gov/protein/NP_004170.1)
- Nucleotide: [NM_004179](https://www.ncbi.nlm.nih.gov/nuccore/NM_004179.3)

## Workflow

1. **Fetch the reference sequence** of TPH1 from NCBI Entrez (Biopython).
2. **Build a profile HMM** from the sequence with `pyhmmer`.
3. **Prepare the data**: split sequences longer than 100,000 residues so HMMER can process them.
4. **Iterative HMM search** in metagenome-assembled genomes (MAGs) from the human gut microbiome.
5. **Summarise the hits** in a table (accession, length, e-value, p-value, score, domains) and save them to CSV and pickle files.
6. **Find the source organisms** of the top hits using run metadata from the European Nucleotide Archive.
7. **Visualise** the alignments and the distributions of scores and hit lengths.
8. **Alternative approach**: a transformer neural network (Hugging Face `transformers`, PyTorch) that splits DNA into k-mers and compares sequence embeddings with cosine similarity, followed by an analysis of the model (PCA, t-SNE) and unit tests of the search.

## Tech stack

Python, Google Colab, Biopython, pyhmmer, pandas, NumPy, Matplotlib, seaborn, scikit-learn, PyTorch, Hugging Face Transformers

## How to run

1. Open the notebook in Google Colab with the badge above.
2. Run the first cell to install the packages (`Biopython`, `biotite`, `pyhmmer`).
3. The search cells read the microbiome sequences and save the results to Google Drive (`/content/drive/My Drive/...`), so mount your Drive and adjust the paths to where your data is stored.

## Team and my contribution

Mikołaj Kikolski, Julia Cieszko, Wiktoria Pabiś, Natalia Kowal

My part:

- splitting long sequences so they can be searched with HMMER,
- plots of the search results (scores and hit lengths),
- analysis of the transformer model (`TransformerNNAnalyzer`): k-mer tokenization, distances between embeddings, PCA and t-SNE visualisations, and performance measurements.
