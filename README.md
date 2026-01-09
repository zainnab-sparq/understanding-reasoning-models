# Understanding OpenAI Reasoning Models

A comprehensive guide to OpenAI's GPT-5.2 reasoning capabilities. This project demonstrates how to control reasoning effort, understand token costs, and implement production-ready workflow patterns.

## 📚 What's Included

### 1. [reasoning_model_cost.ipynb](reasoning_model_cost.ipynb)
**Token Cost Analysis** — Compare token usage across 5 reasoning effort levels.

- Tests `none`, `low`, `medium`, `high`, and `xhigh` reasoning efforts
- Visualizes token breakdown (input, reasoning, output)
- Calculates actual costs using OpenAI pricing
- Uses a spatial reasoning puzzle to demonstrate accuracy vs cost tradeoffs

### 2. [openai_reasoning_controls.ipynb](openai_reasoning_controls.ipynb)
**API Controls Deep Dive** — Learn the three main ways to control reasoning models.

- **Deliberation Control**: `reasoning={"effort": "low|medium|high"}`
- **Stopping Controls**: `max_output_tokens` to cap costs
- **Output Shaping**: Prompt engineering for structured JSON output

### 3. [reasoning_workflow_patterns.ipynb](reasoning_workflow_patterns.ipynb)
**Production Workflow Patterns** — Three battle-tested patterns for real applications.

- **Pattern 1: Fast Path, Then Escalate** — Try cheap first, escalate if uncertain
- **Pattern 2: Always Reason for High-Risk** — Financial/legal decisions always use high effort
- **Pattern 3: Draft, Then Verify** — Fast generation + thorough review

## 🚀 Quick Start

### 1. Clone the Repository
```bash
git clone https://github.com/suspicious-cow/understanding-reasoning-models.git
cd understanding-reasoning-models
```

### 2. Create Environment (Recommended)
```bash
conda create -n reasoning-models-demo python=3.11
conda activate reasoning-models-demo
```

### 3. Install Dependencies
```bash
pip install -r requirements.txt
```

### 4. Set Your OpenAI API Key
```bash
# Windows (Command Prompt)
set OPENAI_API_KEY=your-api-key-here

# Windows (PowerShell)
$env:OPENAI_API_KEY="your-api-key-here"

# macOS/Linux
export OPENAI_API_KEY=your-api-key-here
```

### 5. Run the Notebooks
Open in VS Code or Jupyter:
```bash
jupyter notebook
# or
code .
```

## 💰 Pricing Reference (as of January 2026)

| Token Type | Price per 1M Tokens |
|------------|---------------------|
| Input      | $1.75               |
| Output (includes reasoning) | $14.00 |

> **Note:** Reasoning tokens are billed as output tokens. Higher reasoning effort = more tokens = higher cost.

## 🔑 Key Concepts

### Reasoning Tokens
- **What they are**: Hidden "thinking" tokens the model uses internally before answering
- **You pay for them**: They're billed as output tokens even though you don't see them
- **Control them**: Use `reasoning={"effort": "low|medium|high"}` to control how much the model thinks

### The Responses API
```python
from openai import OpenAI
client = OpenAI()

response = client.responses.create(
    model="gpt-5.2",
    input=[{"role": "user", "content": "Your prompt here"}],
    reasoning={"effort": "medium"}  # low, medium, high
)

# Access the answer
print(response.output_text)

# Check token usage
print(f"Reasoning tokens: {response.usage.output_tokens_details.reasoning_tokens}")
print(f"Total output tokens: {response.usage.output_tokens}")
```

## 📊 Expected Results

### Token Usage by Effort Level (Example)
| Effort | Reasoning Tokens | Total Output | Use Case |
|--------|------------------|--------------|----------|
| none   | 0                | ~200         | Simple lookups |
| low    | 0-50             | ~250         | Classification |
| medium | 50-200           | ~400         | General tasks |
| high   | 200-500+         | ~600+        | Complex analysis |

### When to Use Each Pattern

| Pattern | Best For | Trade-off |
|---------|----------|-----------|
| **Escalate** | Mixed difficulty workloads | Lower avg cost, variable latency |
| **Always High** | Financial, legal, compliance | Higher cost, predictable quality |
| **Draft+Verify** | Code generation, content | Two calls, catches errors |

## 📁 Project Structure
```
understanding-reasoning-models/
├── README.md                           # This file
├── requirements.txt                    # Python dependencies
├── reasoning_model_cost.ipynb          # Token cost comparison
├── openai_reasoning_controls.ipynb     # API controls demo
├── reasoning_workflow_patterns.ipynb   # Production patterns
└── .github/
    └── copilot-instructions.md         # GitHub Copilot config
```

## ⚠️ Important Notes

1. **API Key Security**: Never commit your API key. Use environment variables.
2. **Cost Awareness**: High reasoning effort can be 2-3x more expensive than low effort.
3. **Not All Tasks Need Reasoning**: Simple questions (classifications, lookups) don't benefit from high effort.
4. **Model Availability**: These notebooks use `gpt-5.2`. Ensure your API has access to this model.

## 🤝 Contributing

Feel free to open issues or PRs for:
- Bug fixes
- Additional workflow patterns
- Documentation improvements
- New example use cases

## 📄 License

MIT License

## 🔗 Resources

- [OpenAI API Documentation](https://platform.openai.com/docs)
- [OpenAI Pricing](https://openai.com/pricing)
- [Responses API Reference](https://platform.openai.com/docs/api-reference/responses)
