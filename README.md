# Understanding Reasoning Models

A demonstration of OpenAI's GPT-5.2 reasoning capabilities, showing how different reasoning effort levels affect token usage and response quality.

## Overview

This project explores how reasoning models "think" before answering by comparing token usage (input, reasoning, and output tokens) across different reasoning effort levels:

- **Minimal** - Fastest, cheapest, minimal internal reasoning
- **Low** - Light reasoning overhead
- **Medium** - Balanced (default)
- **High** - Maximum reasoning depth, highest token usage

## The Test Prompt

We use a spatial reasoning puzzle to test the model's ability to catch subtle details:

> "I live in Houston, Texas and I have a box with a big hole in it and I need to ship a baseball. I put the ball into the box. Tape it up. Put a label on it. Then send it to my friend in New York City, New York. He picks up the box on Union Street. Takes a cab to his out on Wilson Blvd and goes into his kitchen. He then opens the box and pours out the contents. Where is the baseball?"

The correct answer requires recognizing that the baseball likely fell out through the hole during shipping.

## Setup

### 1. Install Dependencies

```bash
pip install -r requirements.txt
```

### 2. Set Your OpenAI API Key

```bash
# Windows
set OPENAI_API_KEY=your-api-key-here

# macOS/Linux
export OPENAI_API_KEY=your-api-key-here
```

Or add it directly in the notebook (not recommended for production).

### 3. Run the Notebook

Open `reasoning_models_demo.ipynb` in Jupyter or VS Code and run all cells.

## Key Findings

- **Reasoning tokens** increase significantly with higher effort levels
- Higher reasoning effort generally produces more accurate answers for complex problems
- The trade-off is cost and latency vs. accuracy
- Simple questions don't benefit much from high reasoning effort

## API Reference

This project uses the OpenAI **Responses API**:

```python
from openai import OpenAI
client = OpenAI()

response = client.responses.create(
    model="gpt-5.2",
    input=[{"role": "user", "content": "Your prompt here"}],
    reasoning={"effort": "medium"}  # minimal, low, medium, or high
)

print(response.output_text)
print(response.usage.output_tokens_details.reasoning_tokens)
```

## License

MIT
