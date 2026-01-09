# GitHub Copilot Instructions

## Project Overview

This project demonstrates OpenAI's GPT-5.2 reasoning capabilities using the Responses API. It compares token usage across different reasoning effort levels (minimal, low, medium, high).

## Environment

- **Conda Environment**: `reasoning-models-demo`
- **Python Version**: 3.11
- Activate with: `conda activate reasoning-models-demo`

## Tech Stack

- **Python 3.10+**
- **OpenAI API** - Using the Responses API (`client.responses.create()`)
- **Pandas** - Data manipulation and analysis
- **Matplotlib** - Visualization
- **Jupyter Notebooks** - Interactive development

## Code Style

- Use type hints where appropriate
- Follow PEP 8 conventions
- Use descriptive variable names
- Add docstrings to functions

## OpenAI API Patterns

When working with GPT-5.2 and reasoning models, use the Responses API:

```python
from openai import OpenAI
client = OpenAI()

response = client.responses.create(
    model="gpt-5.2",
    input=[{"role": "user", "content": prompt}],
    reasoning={"effort": "medium"}  # minimal, low, medium, high
)

# Access the response
answer = response.output_text

# Access token usage
input_tokens = response.usage.input_tokens
output_tokens = response.usage.output_tokens
reasoning_tokens = response.usage.output_tokens_details.reasoning_tokens
total_tokens = response.usage.total_tokens
```

## Key Files

- `reasoning_model_cost.ipynb` - Main demonstration notebook
- `requirements.txt` - Project dependencies
- `README.md` - Project documentation

## Common Tasks

### Adding a new reasoning test
1. Use the `query_model()` helper function
2. Pass the model name and reasoning effort level
3. Add results to the comparison dataframe

### Visualizing results
- Use matplotlib for charts
- Include both stacked bar charts (token breakdown) and comparison charts (total tokens)

## Notes

- Always handle API errors gracefully
- Remember that reasoning tokens are billed as output tokens
- Higher reasoning effort = more tokens = higher cost but potentially better answers
