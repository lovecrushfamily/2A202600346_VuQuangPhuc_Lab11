# `src/` Run Guide

This folder contains the local Python implementation of the Lab 11 project using:

- Google ADK for the agent and plugin guardrails
- Google Gemini for generation and LLM-as-Judge
- NVIDIA NeMo Guardrails for Colang-based safety rules

## Structure

- `main.py` — run the full lab flow or individual parts
- `core/` — API key setup and shared helpers
- `agents/` — unsafe and protected agent creation
- `attacks/` — manual adversarial prompts and AI-generated red teaming
- `guardrails/` — input guardrails, output guardrails, and NeMo config
- `testing/` — before/after comparison and automated test pipeline
- `hitl/` — confidence routing and human-in-the-loop design

## Setup

From the project root:

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
export GOOGLE_API_KEY="your-api-key-here"
```

## Run Everything

From the project root:

```bash
python src/main.py
```

Or from inside `src/`:

```bash
python main.py
```

## Run By Part

```bash
python src/main.py --part 1
python src/main.py --part 2
python src/main.py --part 3
python src/main.py --part 4
```

## Run Individual Modules

From inside `src/`:

```bash
python guardrails/input_guardrails.py
python guardrails/output_guardrails.py
python guardrails/nemo_guardrails.py
python testing/testing.py
python hitl/hitl.py
```

## What Each Part Does

### Part 1

- Creates an unsafe VinBank assistant
- Runs 5 manual adversarial prompts
- Uses Gemini to generate extra red-team prompts

### Part 2

- Tests input guardrails:
  - prompt-injection regex detection
  - topic filtering
  - ADK input plugin
- Tests output guardrails:
  - PII and secret redaction
  - LLM-as-Judge safety review
  - ADK output plugin
- Initializes and tests NeMo Guardrails

### Part 3

- Compares unsafe vs protected agent behavior
- Runs an automated security testing pipeline
- Prints block-rate and leak-rate metrics

### Part 4

- Demonstrates confidence-based routing
- Prints 3 HITL decision points for the banking assistant

## Notes

- `GOOGLE_API_KEY` is required for Gemini and ADK model calls.
- NeMo Guardrails is optional at runtime, but recommended. If it is not installed, the project will skip that part gracefully.
- If package installation fails because of network restrictions, activate the environment later and rerun:

```bash
source .venv/bin/activate
pip install -r requirements.txt
```
