# LLM-Based Vulnerability Detection in Tokenized Assembly: 
A Case Study on CWE-457 (Use of Uninitialized Variable).

## Project Overview
This project explores the feasibility of using pre-trained large language models (LLMs) to detect vulnerabilities directly from disassembled binary code, focusing on detecting instances of CWE-457.

The workflow includes:
- Disassembly normalization
- Tokenization of assembly code
- Model fine-tuning and evaluation
- Hyperparameter optimization

## Dataset Preparation

> **Note:** The processed dataset (`llm_cwe457.jsonl`) is included with this project for immediate use.  
> This section documents the original preparation process for reproducibility.

1. Clone the Juliet Test Suite Linux port by Alexander Richardson:

```bash
git clone https://github.com/arichardson/juliet-test-suite-c.git
cd juliet-test-suite-c
```

2. Build the test cases into ELF binaries:

```bash
python3 juliet.py --all --generate --make -k --run | tee full_build.log
```

- This compiles all available Juliet C/C++ test cases (excluding Windows-specific ones).

3. Run the provided `generate_dataset.py` script:

```bash
python3 generate_dataset.py
```
This script:
   - Normalizes disassembly into abstract tokens (`READ`, `WRITE`, `END`, etc.)
   - Filters to CWE-457 samples only
   - Exports the dataset to `llm_cwe457.jsonl`

## Project Setup

1. Create and activate a Python virtual environment:

```bash
python3 -m venv my_venv
source my_venv/bin/activate
```

2. Install project dependencies:

```bash
pip install --upgrade pip
pip install -r "requirements.txt"
```

The `setup_env.sh` script will:
- Create a virtual environment (if not already created)
- Install all required Python libraries listed in `requirements.txt`

## Requirements
Python 3.9 or newer is recommended.

Key libraries:
- PyTorch
- Hugging Face Transformers
- Datasets
- scikit-learn
- Evaluate
- Accelerate
- Jupyter

Full list is available in `requirements.txt`.

## Running the Project
Once dependencies are installed:
- Open and run the provided `LLM_VulnHunter.ipynb` notebook for training and evaluation.
- Saved models and results will be written to the `results/` directory.

## Notes
- Training was performed using CPU-only PyTorch builds for compatibility.
- The project uses a lightweight dataset derived from the Juliet Test Suite.

## Acknowledgments
- [Juliet Test Suite (NIST)](https://samate.nist.gov/SARD/test-suites/112)
- [arichardson's Juliet Test Suite C Port](https://github.com/arichardson/juliet-test-suite-c)
- [Hugging Face Transformers](https://huggingface.co/models)