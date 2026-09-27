# AI Resume Screening

An AI-powered command-line tool that reads PDF and DOCX resumes, compares them with a job description, and ranks candidates by match score.

It is built to help a recruiter review candidates faster. It does **not** make hiring decisions automatically.

## What it does

For every resume in the `resumes/` folder, the project:

1. Reads the PDF or DOCX file.
2. Extracts the candidate's skills, education, projects, and experience.
3. Compares that information with the job description in `resume_parser.py`.
4. Gives a match score from 0 to 100.
5. Prints the strongest and weakest matches with an easy-to-read explanation.

Example output:

```text
Processing: candidate_resume.pdf
Score: 85.0

TOP 2 CANDIDATES
Candidate Name - 85.0%
```

## Requirements

- Python 3.14 or newer
- A free or paid [Groq API key](https://console.groq.com/keys)
- [uv](https://docs.astral.sh/uv/) (recommended)

## Quick start

### 1. Clone the project

```bash
git clone https://github.com/akshat-create/Resume-Screening-Using-LLM-AI-.git
cd Resume-Screening-Using-LLM-AI-
```

### 2. Install dependencies

```bash
uv sync
```

This creates a local `.venv` environment and installs everything the project needs.

### 3. Add your Groq API key

Create a file named `.env` in the project folder:

```env
GROQ_API_KEY=your_groq_api_key_here
```

Get your key from the [Groq Console](https://console.groq.com/keys).

### 4. Add resumes

Put the PDF or DOCX files you want to screen inside the `resumes/` folder:

```text
resumes/
├── candidate_one.pdf
└── candidate_two.docx
```

### 5. Run the project

```bash
.venv/bin/python resume_parser.py
```

On Windows, use:

```powershell
.venv\Scripts\python.exe resume_parser.py
```

The project sends the job description and resume text to Groq for analysis. It pauses briefly between requests, so allow it to finish before closing the terminal.

## Change the job description

Open `resume_parser.py` and edit the text assigned to `job_description` near the top of the file. For example, replace the current Software Development Engineer description with the role you want to screen for.

You can also change the Groq model by editing this line:

```python
model = "openai/gpt-oss-120b"
```

## Project structure

```text
.
├── resume_parser.py              # Main program
├── resumes/                      # Add local PDF and DOCX files here
├── src/resume_screening_llm/     # Python package
├── pyproject.toml                # Dependencies and project settings
├── uv.lock                       # Locked dependency versions
└── README.md                     # Project guide
```

## Common problems

### `zsh: command not found: python`

Use the project environment directly:

```bash
.venv/bin/python resume_parser.py
```

### `ModuleNotFoundError: No module named 'dotenv'`

Dependencies have not been installed in this project yet. Run:

```bash
uv sync
```

Then run the project again with:

```bash
.venv/bin/python resume_parser.py
```

### The program stops with `KeyboardInterrupt`

The program was stopped manually with `Ctrl+C`. Run it again and wait; it intentionally pauses for a few seconds between API requests.

### Groq connection or API-key error

Check that:

- `.env` exists in the project folder.
- The key is written as `GROQ_API_KEY=...`.
- Your internet connection is working.
- Your Groq account can access the selected model.

## Privacy and responsible use

Resumes may contain personal information. `.env`, virtual environments, and the contents of `resumes/` are ignored by Git, so they are not uploaded to this repository. Only screen resumes you are authorized to use, and always have a person review the final results.

## Tech used

- Python
- Groq API
- Pydantic
- PyPDF
- python-docx
- python-dotenv
