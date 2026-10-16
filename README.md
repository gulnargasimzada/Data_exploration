# Exploratory Text Analysis: Political Economy Corpus

## Overview
This repository contains the computational text analysis pipeline developed for the **IDS 570: Text as Data** course project ("Putting it all together on larger corpus"). The project conducts an empirical text exploration across 23 Early Modern texts addressing political economy, international trade, and public finance.

The objective is to evaluate how these texts relate to or diverge from one another by triangulating three complementary quantitative frameworks: lexical distinctiveness (TF–IDF), vector space correlation (Pearson similarity), and dependency-based syntactic complexity.

## Analytical Workflow & Methodology

### 1. Ingestion & Typography Normalization (Step 0)
- Ingested 23 `.txt` files into a structured tibble.
- Systematically normalized Early Modern typography by replacing the long S (`ſ`) with standard `s` via regex.
- Preserved historical spelling variations (e.g., `u/v`, `i/j`) to prevent artificial lexical distortion, opting to manage typesetting noise downstream via feature frequency thresholding.

### 2. Lexical Distinctiveness (Approach 1: TF–IDF)
- Tokenized texts with punctuation, numeric characters, symbols, and standard English stopwords removed.
- Constructed a Document-Feature Matrix (DFM) and calculated TF–IDF weights across the corpus.
- Extracted top 10 distinctive features per document to evaluate topical specialization, technical mercantile vocabulary, and OCR/orthographic noise.

### 3. Vector Similarity & Clustering (Approach 2: Pearson Correlation)
- Trimmed idiosyncratic and low-frequency terms (`dfm_trim(min_termfreq = 5)`) to eliminate non-informative noise.
- Calculated pairwise Pearson correlation coefficients (r) across all 253 unique document pairs.
- Visualized global relational patterns using a symmetric heatmap and identified extreme similarity pairs (most and least similar texts).

### 4. Syntactic Complexity Profile (Approach 3: Week 05 Framework)
- Selected the empirically least similar text pair (`A93819` vs. `B14801__Free_Trade`, r = 0.170) for deep structural analysis.
- Applied dependency parsing using `udpipe` (`english-ewt` model).
- Quantified five key syntactic complexity metrics:
  - Mean Length of Sentence (MLS)
  - Clauses per Sentence (C/S)
  - Dependent Clauses per Sentence (DC/S)
  - Coordination per Sentence (Coord/S)
  - Complex Nominals per Sentence (CN/S)

## Repository Contents
- `Data_exp.Rmd`: Fully reproducible R Markdown analysis script.
- `*.txt`: Corpus of 23 Early Modern political economy texts.
- `README.md`: Project summary and pipeline documentation.

## Software Requirements
The analysis was performed in R using the following core packages:
- `tidyverse` (data manipulation and visualization)
- `quanteda` & `quanteda.textstats` (text preprocessing, DFM, TF–IDF, similarity metrics)
- `udpipe` (tokenization, POS tagging, dependency parsing)