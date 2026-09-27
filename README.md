# AI Resume Screening

A command-line AI tool that reads résumés, extracts structured candidate information, and ranks candidates against a job description.

It uses Groq's LLM API to turn unstructured PDF and DOCX résumés into a consistent schema, then produces a score and concise hiring-relevance summary for each candidate.

> This project is intended to support human review—not to make automated hiring decisions. Review all results for accuracy, fairness, and context before acting on them.

## Features

- Extracts text from PDF and DOCX résumés.
- Parses skills, work history, education, projects, and certifications into structured data.
- Extracts requirements from a job description.
- Scores and ranks candidates from 0–100 against the role.
- Returns matching skills, missing skills, experience fit, and a brief verdict.
- Keeps API keys and candidate documents out of version control.

## Tech stack

- Python 3.14+
- [Groq](https://console.groq.com/)
- Pydantic
- PyPDF
- python-docx
- uv (recommended dependency manager)

## Getting started

### 1. Clone the repository

```bash
git clone https://github.com/akshat-create/Resume-Screening-Using-LLA-AI-.git
cd Resume-Screening-Using-LLA-AI-
```

### 2. Install dependencies

Using [uv](https://docs.astral.sh/uv/):

```bash
uv sync
```

Or with pip:

```bash
python -m venv .venv
source .venv/bin/activate  # Windows: .venv\\Scripts\\activate
pip install groq pydantic pypdf python-docx python-dotenv
```

### 3. Configure your API key

Create a local `.env` file in the project root:

```env
GROQ_API_KEY=your_groq_api_key_here
```

Get an API key from the [Groq Console](https://console.groq.com/keys). Never commit `.env`; it is already ignored by Git.

### 4. Add résumés locally

Create a `resumes/` directory and place PDF or DOCX files inside it:

```bash
mkdir -p resumes
```

Candidate files are intentionally ignored by Git to avoid publishing personal information.

### 5. Run the screener

```bash
uv run python resume_parser.py
```

The script reads the job description defined in `resume_parser.py`, processes each supported file in `resumes/`, and prints the top two and lowest two candidates with their match details.

## How it works

```text
Job description ──> LLM extracts role requirements
                                      │
Local PDF/DOCX résumés ──> text extraction ──> LLM parses candidate data
                                      │
                         requirement comparison and score (0–100)
                                      │
                                ranked candidate output
```

## Project structure

```text
.
├── resume_parser.py   # Extraction, parsing, scoring, and ranking workflow
├── pyproject.toml     # Project metadata and dependencies
├── uv.lock            # Reproducible dependency lockfile
├── src/day5/          # Python package placeholder
└── resumes/           # Local candidate files (ignored by Git)
```

## Configuration notes

- Change `job_description` in `resume_parser.py` to screen for another role.
- The default model is `openai/gpt-oss-120b` through Groq. Ensure your Groq account can access it, or change the `model` value to an available model.
- The script pauses between requests to reduce the chance of rate-limit errors.

## Privacy and responsible use

Résumés can contain sensitive personal information. This repository does not include sample candidate files, API keys, or environment files. Use the tool only with appropriate authorization, protect any local input files, and keep a human in the decision loop.

## License

No license has been selected yet. Add one before reusing or distributing this project.
