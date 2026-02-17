# ai-code-review-assignment-3-answer

## Python version

Tested with Python 3.13.2.

## Install dependencies

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

## Run tests locally

```bash
pytest -v
```

## Build Docker image

```bash
docker build -t ai-code-review-assignment-3-answer .
```

## Run tests in Docker

```bash
docker run --rm ai-code-review-assignment-3-answer
```
