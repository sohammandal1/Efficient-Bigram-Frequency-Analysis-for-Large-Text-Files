
# \# Bigram Frequency Counter with Map-Reduce (Shuffle \& Sort)

This project implements a **Map function from scratch** with shuffle and sort functionality to find the most frequent **bi-grams** (pairs of consecutive words) in a given text file.
The implementation is inspired by the **MapReduce paradigm**, as taught in Lecture 8.

---

## 📌 Problem Statement

You are given a large text file containing real-world textual data. Your task is to implement a **map function** that:

- Reads the file in **partitions** using a user-specified buffer size (RAM in MB).
- Extracts **key bi-grams** from the text:
    - A **bi-gram** is an ordered sequence of two words where the second word appears immediately after the first.
    - Both words must contain at least **three English letters**.
    - Bi-grams must **exclude articles, prepositions, and conjunctions**.
- Ensures all words are **lowercased** before counting.
- Performs **shuffle and sort** on the intermediate results.
- Produces the **top K most frequent bi-grams** from the input file.

The program must handle:

- **Corrupt bytes, unknown characters, and non-English content** gracefully.
- Tokenization of words using **non-English characters and digits as boundaries**.

---

## ⚙️ Example

Input text:
IIT Kharagpur is the oldest IIT.

vbnet
Copy code

Key bi-grams:
(iit kharagpur)
(oldest iit)

yaml
Copy code

---

## 🚀 Features

- **Partitioning**: Reads input file in chunks based on user-defined buffer size (MB).
- **Tokenizer**: Extracts only alphabetic words (`[a-zA-Z]+`).
- **Filtering**: Removes articles, prepositions, conjunctions, and stopwords.
- **Lowercasing**: Ensures case-insensitive processing.
- **Bigram Detection**: Creates pairs of consecutive words that meet constraints.
- **Shuffle \& Sort**: Aggregates, shuffles, and sorts bigram counts.
- **Top-K Extraction**: Outputs the most frequent K bi-grams.

---
yaml
Copy code

---

## 🖥️ Requirements

- **Python 3.10+**
- [NLTK](https://www.nltk.org/) library

Install dependencies:

```bash
pip install nltk
First-time NLTK setup:

python
Copy code
import nltk
nltk.download('stopwords')
▶️ Usage
Run from the Linux command line:

bash
Copy code
python code.py <input_file> <buffer_size_MB> <k>
<input_file>: Path to the text file (e.g., data.txt)

<buffer_size_MB>: Amount of RAM (in MB) used for partitioning the file

<k>: Number of most frequent bi-grams to output

Example:
bash
Copy code
python code.py data.txt 1024 20
This will:

Partition data.txt into chunks of 1024 MB each.

Process each chunk to extract and count valid bi-grams.

Shuffle & sort across partitions.

Print the top 20 most frequent bi-grams.

📊 Output
Example final output (shuffled_sorted_bigrams.txt):

bash
Copy code
('iit', 'kharagpur'): 15
('machine', 'learning'): 12
('deep', 'learning'): 9
...
Console output for top_k_occurrences:

bash
Copy code
('iit', 'kharagpur'): 15
('machine', 'learning'): 12
...
🛠️ Notes
The implementation is robust against:

Non-English characters

Corrupt or malformed bytes

Bi-grams are only considered if both words:

Are alphabetic with length ≥ 3

Are not in the excluded stopword list

