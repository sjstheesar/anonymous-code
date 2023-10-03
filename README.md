
# BrainCode

Project investigating human and artificial neural representations of python program comprehension and execution.

This pipeline supports several major functions.

-   **MVPA** (multivariate pattern analysis) evaluates decoding of **code properties** or **code model** representations from their respective **brain representations** within a collection of canonical **brain regions**.
-   **PRDA** (program representation decoding analysis) evaluates decoding of **code properties** from **code model** representations.

To run all core experiments from the paper, the following command will suffice after setup:

```bash
python braincode mvpa # runs all core MVPA analyses in parallel
python braincoda prda # runs all supplemental PRDA analyses in parallel
```

To regenerate tables and figures from the paper, run the following after completing the analyses:

```bash
cd paper/scripts
source run.sh # pulls scores, runs stats, generates plots and tables
```

### Supported Brain Regions

-   `brain-MD` (Multiple Demand)
-   `brain-lang` (Language)
-   `brain-vis` (Visual)
-   `brain-aud` (Auditory)

### Supported Code Features

**Code Properties**

-   `test-code` (code vs. sentences)
-   `test-lang` (english vs. japanese)
-   `task-content` (math vs. str) <sup>\*datatype</sup>
-   `task-structure` (seq vs. for vs. if) <sup>\*control flow</sup>
-   `task-tokens` (# of tokens in program) <sup>\*static analysis</sup>
-   `task-lines` (# of runtime steps during execution) <sup>\*dynamic analysis</sup>
-   `task-bytes` (# of bytecode ops executed)
-   `task-nodes` (# of nodes in AST)
-   `task-halstead` (function of tokens, operations, vocabulary)
-   `task-cyclomatic` (function of program control flow graph)

**Code Models**

-   `code-projection` (presence of tokens)
-   `code-bow` (token frequency)
-   `code-tfidf` (token and document frequency)
-   `code-seq2seq`<sup> [1](https://github.com/IBM/pytorch-seq2seq)</sup> (sequence modeling)
-   `code-xlnet`<sup> [2](https://arxiv.org/pdf/1906.08237.pdf)</sup> (autoregressive LM)
-   `code-gpt2`<sup> [4](https://huggingface.co/microsoft/CodeGPT-small-py)</sup> (autoregressive LM)
-   `code-bert`<sup> [5](https://arxiv.org/pdf/2002.08155.pdf)</sup> (masked LM)
-   `code-roberta`<sup> [6](https://huggingface.co/huggingface/CodeBERTa-small-v1)</sup> (masked LM)
-   `code-transformer`<sup> [3](https://arxiv.org/pdf/2103.11318.pdf)</sup> (LM + structure learning)

## Installation

Requirements: [Anaconda](https://conda.io/projects/conda/en/latest/user-guide/install/index.html)

```bash
conda create -n braincode python=3.7
source activate braincode
git clone --branch ICML2022 --depth 1 https://github.com/anonmyous-author/anonymous-code
cd braincode
pip install . # -e for development mode
cd setup
source setup.sh # downloads 'large' files, e.g. datasets, models
```

## Run

```bash
usage: braincode [-h] [-f FEATURE] [-t TARGET] [-m METRIC] [-d CODE_MODEL_DIM]
                 [-p BASE_PATH] [-s] [-b]
                 {mvpa,prda}

run specified analysis type

positional arguments:
  {mvpa,prda}

optional arguments:
  -h, --help            show this help message and exit
  -f FEATURE, --feature FEATURE
  -t TARGET, --target TARGET
  -m METRIC, --metric METRIC
  -d CODE_MODEL_DIM, --code_model_dim CODE_MODEL_DIM
  -p BASE_PATH, --base_path BASE_PATH
  -s, --score_only
  -b, --debug
```

note: BASE_PATH must be specified to match setup.sh if changed from default.

**Sample calls**

```bash
# basic examples
python braincode mvpa -f brain-MD -t task-structure # brain -> {task, model}
python braincode prda -f code-bert -t task-tokens # model -> task

# more complex example
python braincode mvpa -f brain-lang+brain-MD -t code-projection -d 64 -m SpearmanRho -p $BASE_PATH --score_only
# note how `+` operator can be used to join multiple representations via concatenation
# additional metrics are available in the `metrics.py` module
```

## Automation

### Make

This package also provides an automated build using [GNU Make](https://www.gnu.org/software/make/manual/make.html). A single pipeline is provided, which starts from an empty environment, and proceeds through to the creation of paper tables and figures.

```bash
make paper # see 'make help' for more info
```

### Docker

Build automation can also be containerized in [Docker](https://hub.docker.com/)

```bash
make docker
```

## Citation

If you use this work, please cite XXX (under review)

## License

[![License: MIT](https://img.shields.io/badge/License-MIT-brightgreen.svg)](https://opensource.org/licenses/MIT)

Updated on 2022-05-14T20:53:34+06:55
Updated on 2022-12-03T14:30:30+06:55
Updated on 2023-12-14T11:47:01+06:55
Updated on 2022-12-24T17:52:40+06:55
Updated on 2023-01-30T19:37:35+06:55
Updated on 2023-01-17T06:19:00+06:55
Updated on 2023-06-10T19:12:18+06:55
Updated on 2022-09-03T23:00:03+06:55
Updated on 2023-10-26T23:38:39+06:55
Updated on 2022-12-17T19:21:21+06:55
Updated on 2023-05-27T11:19:12+06:55
Updated on 2022-07-16T21:23:53+06:55
Updated on 2022-06-13T18:50:06+06:55
Updated on 2022-11-14T15:04:35+06:55
Updated on 2023-04-12T16:43:34+06:55
Updated on 2023-07-15T09:55:01+06:55
Updated on 2023-05-04T02:45:46+06:55
Updated on 2023-07-22T13:51:11+06:55
Updated on 2022-08-11T03:11:58+06:55
Updated on 2023-01-16T05:03:15+06:55
Updated on 2023-06-17T15:07:06+06:55
Updated on 2022-12-11T11:05:48+06:55
Updated on 2023-12-31T11:29:44+06:55
Updated on 2024-01-03T12:48:09+06:55
Updated on 2022-08-22T19:05:47+06:55
Updated on 2023-10-01T17:48:48+06:55
Updated on 2023-12-24T10:43:32+06:55
Updated on 2023-10-03T10:39:05+06:55