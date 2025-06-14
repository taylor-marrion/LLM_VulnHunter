[![License: CC BY-NC-ND 4.0](https://img.shields.io/badge/License-CC%20BY--NC--ND%204.0-lightgrey.svg)](http://creativecommons.org/licenses/by-nc-nd/4.0/)

# LLM-Based Vulnerability Detection in Tokenized Assembly: 
A Case Study on CWE-457 (Use of Uninitialized Variable).
<br>
Presentation discussing approach, methodology, and results can be found [here](https://youtu.be/N6KSaptGfOk).

> ⚠️*Note:*⚠️ <br>
> This repository documents Phase 2 of an ongoing multi-stage research effort, which is expected to form the foundation of my future dissertation work. 
> Due to the academic and proprietary nature of this research, the full source code and model training implementation are not publicly available at this time. 
> However, the repository includes the associated research paper to outline the methodology, experimental design, and key findings. 
> The primary purpose of this repository is to share the scope of work, technical direction, and contributions to the field of binary vulnerability detection. 
> Additional materials (e.g., visualizations, presentation slides, and selected data samples) may be added in the future, depending on publication timelines and review clearance. 

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


## 📄 License

This project is licensed under the [Creative Commons BY-NC-ND 4.0 License](https://creativecommons.org/licenses/by-nc-nd/4.0/).  
You may view, share, or cite this work with attribution. Commercial use, redistribution, or modification is not permitted.
