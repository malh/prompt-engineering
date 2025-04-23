# LLM Parameters

## LLM Parameters: Controlling Output

Large language models (LLMs) like GPT-4, Claude, and LLaMA can generate very different responses depending on how you configure them. A handful of settings — known as **LLM parameters** — shape the tone, creativity, length, and repetition of their output. Think of these parameters as knobs you can adjust to tune the model’s behaviour.

This page explains the key **decoding parameters** (used during text generation) and **context settings** (which define how much information the model can handle at once). It's intended for developers and technical users working with LLMs via APIs, CLIs, or embedded tools.

---

## Core Decoding Parameters

| **Parameter**        | **Range / Unit** | **Effect**                                                    | **Typical Use**                                |
|----------------------|------------------|----------------------------------------------------------------|------------------------------------------------|
| `temperature`        | 0 to 2           | Controls randomness. Higher = more creative                   | Use low for accuracy (0.1–0.3), high for ideation (0.8–1.2) |
| `top_p`              | 0 to 1           | Limits token selection to a cumulative probability threshold  | Combine with or use instead of temperature for tighter control |
| `max_tokens`         | Integer          | Sets a hard limit on response length                          | Prevents long or runaway outputs, helps control cost         |
| `presence_penalty`   | 0 to 2           | Penalises token reuse after first occurrence                  | Encourages new ideas, reduces redundancy                    |
| `frequency_penalty`  | 0 to 2           | Penalises repeated tokens based on frequency                  | Helps reduce repetition in longer outputs                   |

These are commonly referred to as **decoding parameters** or **sampling strategies** in documentation and APIs.

### Decoding Parameters in Detail

1. **Temperature (0–2)**
   - At 0: Deterministic, always chooses the most probable next token
   - At 0.7: Balanced creativity (common default)
   - At 1.5+: Highly unpredictable, potentially incoherent

2. **Top-p / Nucleus Sampling**
   - Considers only tokens whose cumulative probability exceeds the threshold
   - Example: `top_p = 0.9` means the model only considers tokens in the top 90% of probability mass
   - Often more stable than temperature for controlling randomness

3. **Max Tokens**
   - Directly impacts API costs and response time
   - Too low can result in truncated responses
   - Can be dynamically adjusted based on the complexity of the request

4. **Presence & Frequency Penalties**
   - `presence_penalty`: Applies once a token has appeared
   - `frequency_penalty`: Increases with each repetition of the same token
   - Higher values can increase diversity but may reduce coherence

---

## Context Window Considerations

The context window defines the model’s short-term memory — the maximum amount of text it can consider at once. This includes your prompt, prior conversation, and the model’s own output. A token is roughly 3/4 of a word in English.

| **Model Type**   | **Typical Context Limit** |
|------------------|----------------------------|
| Smaller LLMs     | 2K–4K tokens               |
| Mid-size LLMs    | 8K–16K tokens              |
| Larger LLMs      | 32K–128K+ tokens           |

If your input and output exceed the context window, the model will truncate from the beginning.

---

## Examples of Parameter Combinations

**Factual Q&A**
```
temperature: 0.1–0.3
top_p: 0.9
presence_penalty: 0
frequency_penalty: 0.1
```

**Creative Writing**
```
temperature: 0.7–1.0
top_p: 1.0
presence_penalty: 0.5
frequency_penalty: 0.5
```

**Code Generation**
```
temperature: 0.2–0.4
top_p: 0.95
presence_penalty: 0
frequency_penalty: 0.2
```

**Summarisation**
```
temperature: 0.3–0.5
top_p: 0.9
presence_penalty: 0.2
frequency_penalty: 0.3
```

**Brainstorming / Ideation**
```
temperature: 0.8–1.2
top_p: 1.0
presence_penalty: 0.6
frequency_penalty: 0.6
```

---

## Getting Started

1. Start with defaults (`temperature: 0.7`, `top_p: 1.0`)
2. Adjust one parameter at a time
3. Use consistent prompts for testing
4. Document what works for your use case

---

