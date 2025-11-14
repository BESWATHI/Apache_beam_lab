# Apache-beam-lab


This repository contains a simple Apache Beam **WordCount** example implemented in Python using the **DirectRunner**.  
The notebook demonstrates how to prepare input data, construct a Beam pipeline, execute it locally, and inspect the processed results.

---

## 1. Overview

This lab provides an introductory walkthrough of Apache Beam's programming model.  
You will learn how a pipeline reads input data, transforms it using Beam primitives, and produces output in a structured form.

The example uses a local text file (`prejudice.txt`) and performs the following:

- Normalizes and tokenizes the text  
- Counts the frequency of each word  
- Writes results in Python tuple-style format  
- Displays the top 20 most common words

This serves as a foundational exercise for understanding Beam pipelines before moving on to distributed runners such as Dataflow, Flink, or Spark.

---

## 2. Directory Structure

```

├── data/
│   └── prejudice.txt               # Input dataset for the WordCount pipeline
│
├── outputs/
│   └── output_words                # Beam-generated word count results (Python tuple format)
│
└── Try_Apache_Beam_Python.ipynb    # Notebook implementing the full pipeline

```

---

## 3. Input Data

The input file **prejudice.txt** must be placed inside the `data/` directory.  
The notebook verifies that this file exists before the pipeline is executed.  
No file contents are printed during setup to keep the environment clean and simple.

---

## 4. Pipeline Summary

The WordCount pipeline consists of the following steps:

1. **ReadFromText**  
   Reads the input file line by line into a Beam `PCollection`.

2. **FlatMap (normalize + tokenize)**  
   Uses regular expressions to extract words from each line while preserving their original capitalization.

3. **Map (word → (word, 1))**  
   Converts each word into a key-value pair where the value is `1`.

4. **CombinePerKey**  
   Aggregates the counts for each unique word across the dataset.

5. **Format**  
   Formats each `(word, count)` pair as a Python tuple string, for example:  
```

('SYNTHETIC', 1)

````

6. **WriteToText**  
Writes the formatted output to the `outputs/` directory.

---

## 5. Result Exploration

After the pipeline completes, the notebook reads the generated output file(s) and loads the results into a Python `Counter`.  
It then prints the **top 20 most frequent words**, allowing you to verify the correctness of your WordCount pipeline and understand the distribution of words in the input text.

---

## 6. Learning Objectives

By completing this lab, you will:

- Understand how Apache Beam pipelines are structured  
- Learn how `PCollection`s flow through a sequence of transformations  
- Use Beam’s core transforms: `FlatMap`, `Map`, `CombinePerKey`  
- Run pipelines locally using the **DirectRunner**  
- Interpret and validate Beam output using native Python tools

---

## 7. Requirements

You will need:

- **Python 3.x**
- **Apache Beam (Python SDK)**  
Install using:
```bash
pip install apache-beam
````

Additional Python libraries used:

* `os`
* `pathlib`
* `collections`
* `re`

---

## 8. Running the Notebook

1. Place the input file in:

   ```
   data/prejudice.txt
   ```
2. Open the notebook:

   ```
   Try_Apache_Beam_Python.ipynb
   ```
3. Run the cells in order to:

   * Set up the environment
   * Execute the Apache Beam WordCount pipeline
   * Display and analyze the results

---

## 9. Sample Output

Example output produced by the pipeline:

```
('SYNTHETIC', 1)
('FICTION', 1)
('DATASET', 1)
('WORDS', 1)
('Inspired', 1)
('by', 311)
('themes', 1)
('from', 1)
('Pride', 1)
('and', 968)
...
```

---

```
This completes the Apache Beam WordCount Lab.
```


