# ✍️ Prompt Engineering

[← Back to Home](../index.md)

Techniques, tools, and best practices for crafting effective prompts and optimizing LLM interactions.

---

## 📋 Table of Contents
- [Overview](#overview)
- [Tools List](#tools-list)
- [Core Techniques](#core-techniques)
- [Best Practices](#best-practices)

---

## Overview

Prompt engineering is the art and science of:
- **Instruction Design**: Clear, specific task descriptions
- **Context Management**: Providing relevant information
- **Output Formatting**: Structuring responses
- **Optimization**: Iterative improvement

---

## Tools List

| Repo | Description | Stars |
|------|-------------|-------|
| [dair-ai/Prompt-Engineering-Guide](https://github.com/dair-ai/Prompt-Engineering-Guide) | Comprehensive guide to prompt engineering | ![GitHub stars](https://img.shields.io/github/stars/dair-ai/Prompt-Engineering-Guide?style=social) |
| [microsoft/promptbase](https://github.com/microsoft/promptbase) | Manage and version prompts | ![GitHub stars](https://img.shields.io/github/stars/microsoft/promptbase?style=social) |
| [brexhq/prompt-engineering](https://github.com/brexhq/prompt-engineering) | Practical tips from Brex | ![GitHub stars](https://img.shields.io/github/stars/brexhq/prompt-engineering?style=social) |
| [f/awesome-chatgpt-prompts](https://github.com/f/awesome-chatgpt-prompts) | Curated ChatGPT prompts | ![GitHub stars](https://img.shields.io/github/stars/f/awesome-chatgpt-prompts?style=social) |

**Note**: Prompt engineering is primarily technique-based rather than tool-based.

---

## Core Techniques

### 1. **Zero-Shot Prompting**

Simple, direct instructions without examples.

```python
prompt = """Classify the sentiment of this text as positive, negative, or neutral.

Text: "I absolutely loved the new restaurant downtown!"

Sentiment:"""

# Response: "Positive"
```

**Best for:**
- Simple tasks
- Well-defined problems
- Modern models (GPT-4, Claude Opus)

### 2. **Few-Shot Prompting**

Provide examples to guide the model.

```python
prompt = """Classify sentiment as positive, negative, or neutral.

Text: "The movie was amazing!"
Sentiment: Positive

Text: "I hated the long wait times."
Sentiment: Negative

Text: "The weather is cloudy today."
Sentiment: Neutral

Text: "This product exceeded my expectations!"
Sentiment:"""

# Response: "Positive"
```

**Best for:**
- Complex tasks
- Specific output formats
- Consistency across examples

**Guidelines:**
- 3-5 examples optimal
- Diverse, representative examples
- Consistent formatting

### 3. **Chain-of-Thought (CoT)**

Encourage step-by-step reasoning.

```python
prompt = """Question: Roger has 5 tennis balls. He buys 2 more cans of tennis balls.
Each can has 3 tennis balls. How many tennis balls does he have now?

Let's solve this step by step:
1. Roger starts with 5 tennis balls
2. He buys 2 cans, each with 3 balls
3. 2 cans × 3 balls = 6 balls
4. 5 + 6 = 11 balls

Answer: 11 tennis balls

Question: Sarah has $23. She buys 3 books at $5 each. How much money does she have left?

Let's solve this step by step:"""

# Response:
# 1. Sarah starts with $23
# 2. She buys 3 books at $5 each
# 3. 3 × $5 = $15
# 4. $23 - $15 = $8
# Answer: $8
```

**Best for:**
- Math and reasoning
- Complex multi-step problems
- Debugging LLM logic

**Variants:**
- **Zero-Shot CoT**: "Let's think step by step"
- **Few-Shot CoT**: Show reasoning examples
- **Self-Consistency**: Generate multiple reasoning paths

### 4. **Instruction Following**

Clear, structured task descriptions.

```python
prompt = """You are a professional editor. Your task is to:
1. Fix all grammar and spelling errors
2. Improve clarity and conciseness
3. Maintain the original meaning
4. Use active voice where possible

Text to edit:
"The report was wrote by me and it had been reviewed by the manager yesterday. There was several errors which was corrected."

Edited text:"""

# Response:
# "I wrote the report, and the manager reviewed it yesterday. We corrected several errors."
```

**Best for:**
- Specific output requirements
- Multi-step tasks
- Quality control

### 5. **Role Prompting**

Assign a specific persona or expertise.

```python
prompt = """You are a senior Python developer with 10 years of experience.
Review this code and suggest improvements:

def calc(x, y):
    return x + y

Your feedback:"""

# Response provides expert-level code review
```

**Best for:**
- Domain-specific tasks
- Consistent tone/style
- Creative writing

**Examples:**
- "You are a helpful customer support agent..."
- "You are a technical writer for developers..."
- "You are a data scientist analyzing..."

### 6. **Structured Output**

Request specific formats (JSON, XML, tables).

```python
prompt = """Extract company information from this text and return as JSON.

Text: "Tesla, Inc. was founded in 2003 by Martin Eberhard and Marc Tarpenning.
The company is headquartered in Austin, Texas."

Return JSON with fields: name, founded_year, founders (array), headquarters"""

# Response:
# {
#   "name": "Tesla, Inc.",
#   "founded_year": 2003,
#   "founders": ["Martin Eberhard", "Marc Tarpenning"],
#   "headquarters": "Austin, Texas"
# }
```

**Formats:**
- JSON: Best for APIs
- Markdown: Documentation
- XML: Data interchange
- CSV: Tabular data

### 7. **Retrieval-Augmented Generation (RAG)**

Provide context from external sources.

```python
context = """
# Documentation
Our API uses API keys for authentication.
Include the key in the Authorization header: Authorization: Bearer YOUR_KEY
"""

prompt = f"""Context:
{context}

Question: How do I authenticate with your API?

Answer based only on the context above:"""

# Response: "To authenticate with our API, include your API key in the Authorization header..."
```

**Best for:**
- Knowledge-intensive tasks
- Reducing hallucinations
- Up-to-date information

### 8. **Self-Consistency**

Generate multiple responses and choose the most common.

```python
# Generate 5 reasoning paths
responses = []
for i in range(5):
    response = llm.generate(prompt, temperature=0.7)
    responses.append(response)

# Extract final answers
answers = [extract_answer(r) for r in responses]

# Majority vote
from collections import Counter
final_answer = Counter(answers).most_common(1)[0][0]
```

**Best for:**
- High-stakes decisions
- Math and reasoning
- Reducing errors

### 9. **ReAct (Reasoning + Acting)**

Combine reasoning with tool use.

```python
prompt = """Question: What is the weather in San Francisco and Paris today?

Thought: I need to check the weather for both cities.
Action: weather_api("San Francisco")
Observation: San Francisco: 65°F, Sunny

Thought: Now I need to check Paris.
Action: weather_api("Paris")
Observation: Paris: 18°C, Cloudy

Thought: I have both temperatures. I should present them clearly.
Answer: San Francisco is 65°F and sunny. Paris is 18°C (64°F) and cloudy.

Question: What is the current stock price of Apple and Microsoft?

Thought:"""
```

**Best for:**
- Agent systems
- Multi-step tasks requiring tools
- Complex workflows

---

## Advanced Techniques

### 1. **Constitutional AI / Self-Critique**

Have the model critique and improve its own output.

```python
# Initial generation
prompt_v1 = "Write a product description for noise-canceling headphones."
response_v1 = llm.generate(prompt_v1)

# Self-critique
prompt_v2 = f"""Here is a product description:

{response_v1}

Critique this description for:
1. Clarity
2. Persuasiveness
3. Completeness

Then rewrite it to address the issues."""

response_v2 = llm.generate(prompt_v2)
```

### 2. **Tree of Thoughts (ToT)**

Explore multiple reasoning paths systematically.

```python
def tree_of_thoughts(problem, branching_factor=3, depth=3):
    """
    1. Generate multiple initial thoughts
    2. Evaluate each thought
    3. Expand promising thoughts
    4. Repeat until solution found
    """
    thoughts = generate_initial_thoughts(problem, n=branching_factor)

    for level in range(depth):
        evaluated = [(t, evaluate_thought(t)) for t in thoughts]
        top_thoughts = sorted(evaluated, key=lambda x: x[1], reverse=True)[:branching_factor]

        if any(is_solution(t) for t, _ in top_thoughts):
            return best_solution(top_thoughts)

        thoughts = []
        for thought, _ in top_thoughts:
            thoughts.extend(expand_thought(thought, n=branching_factor))

    return best_candidate(thoughts)
```

### 3. **Prompt Chaining**

Break complex tasks into sequential steps.

```python
# Step 1: Summarize
summary_prompt = f"Summarize this article in 3 sentences:\n\n{article}"
summary = llm.generate(summary_prompt)

# Step 2: Extract key points
extract_prompt = f"From this summary, extract 5 key points:\n\n{summary}"
key_points = llm.generate(extract_prompt)

# Step 3: Generate questions
questions_prompt = f"Based on these key points, generate 3 discussion questions:\n\n{key_points}"
questions = llm.generate(questions_prompt)
```

### 4. **Meta-Prompting**

Use the LLM to generate prompts.

```python
meta_prompt = """I need to create a prompt for classifying customer support tickets.
The categories are: Billing, Technical, Feature Request, Other.

Generate an effective prompt for this task that includes:
1. Clear instructions
2. Few-shot examples
3. Output format specification"""

generated_prompt = llm.generate(meta_prompt)
# Use generated_prompt for actual classification
```

---

## Model-Specific Techniques

### GPT-4 / GPT-4 Turbo

```python
# System message for consistent behavior
messages = [
    {"role": "system", "content": "You are a helpful assistant that always responds in JSON."},
    {"role": "user", "content": "Extract entities from: 'Apple Inc. was founded by Steve Jobs.'"}
]

# Use lower temperature for deterministic tasks
response = client.chat.completions.create(
    model="gpt-4-turbo",
    messages=messages,
    temperature=0,
    response_format={"type": "json_object"}  # Force JSON
)
```

### Claude (Anthropic)

```python
# Use XML tags for structure
prompt = """<task>
Extract product features from this review.
</task>

<review>
The laptop has a great battery life and the screen is crystal clear.
However, it's quite heavy and expensive.
</review>

<format>
Provide your response in this format:
<features>
<positive>...</positive>
<negative>...</negative>
</features>
</format>"""

# Claude responds well to:
# - Clear XML structure
# - Explicit formatting
# - Long, detailed contexts (200k tokens)
```

### Open-Source Models (Llama, Mistral)

```python
# Use explicit formatting
prompt = """### Instruction:
Translate the following English text to French.

### Input:
Hello, how are you today?

### Response:"""

# Many open models trained on specific templates
# Check model card for recommended format
```

---

## Prompt Optimization

### Iterative Refinement

```python
# Version 1
prompt_v1 = "Summarize this article."
# Issue: Too vague, inconsistent length

# Version 2
prompt_v2 = "Summarize this article in 3 sentences."
# Issue: Sometimes misses key points

# Version 3
prompt_v3 = """Summarize this article in exactly 3 sentences.
Include:
1. Main topic
2. Key findings
3. Conclusion/implications"""
# Better: Specific structure

# Version 4 (Final)
prompt_v4 = """Summarize this article in exactly 3 sentences.

Sentence 1: State the main topic and context
Sentence 2: Describe the key findings or arguments
Sentence 3: Explain the conclusion or implications

Article:
{article}

Summary:"""
# Best: Clear template with examples
```

### A/B Testing

```python
def compare_prompts(prompt_a, prompt_b, test_cases, metric):
    """Compare two prompts across multiple test cases."""
    scores_a = []
    scores_b = []

    for test in test_cases:
        response_a = llm.generate(prompt_a.format(**test))
        response_b = llm.generate(prompt_b.format(**test))

        scores_a.append(metric(response_a, test['expected']))
        scores_b.append(metric(response_b, test['expected']))

    avg_a = sum(scores_a) / len(scores_a)
    avg_b = sum(scores_b) / len(scores_b)

    print(f"Prompt A: {avg_a:.2f}")
    print(f"Prompt B: {avg_b:.2f}")
    print(f"Winner: {'A' if avg_a > avg_b else 'B'}")

    return avg_a, avg_b
```

---

## Common Mistakes

### ❌ 1. Ambiguous Instructions

```python
# Bad
prompt = "Write something about AI."

# Good
prompt = "Write a 200-word introduction to AI for a general audience, explaining what it is and its current applications."
```

### ❌ 2. Lacking Context

```python
# Bad
prompt = "Is this good?"

# Good
prompt = """Evaluate this customer review for helpfulness.
Criteria: Specificity, balanced perspective, actionable information.

Review: "The product works great and shipping was fast."

Evaluation:"""
```

### ❌ 3. Overloading

```python
# Bad (too many tasks)
prompt = "Translate this to French, summarize it, extract entities, check for errors, and rate the sentiment."

# Good (one task)
prompt = "Translate this text to French, preserving the original tone and style."
```

### ❌ 4. Ignoring Model Limits

```python
# Bad (exceeds context window)
prompt = f"Summarize this book: {entire_book_text}"

# Good (chunk and map-reduce)
summaries = [summarize_chunk(chunk) for chunk in book_chunks]
final_summary = summarize_summaries(summaries)
```

### ❌ 5. No Output Validation

```python
# Bad
response = llm.generate(prompt)
return response

# Good
response = llm.generate(prompt)

# Validate format
if not is_valid_json(response):
    response = fix_json(response)

# Validate content
if contains_hallucination(response, context):
    response = regenerate_with_stricter_prompt()

return response
```

---

## Prompt Templates

### Classification

```python
template = """Classify the following {item} into one of these categories: {categories}.

{item_name}: {item_value}

Category:"""

# Usage
prompt = template.format(
    item="email",
    categories="Spam, Important, Newsletter, Personal",
    item_name="Subject",
    item_value="Congratulations! You've won $1,000,000!"
)
```

### Information Extraction

```python
template = """Extract {fields} from the following {source_type}.
Return the result as JSON.

{source_type}:
{source_content}

JSON:"""

# Usage
prompt = template.format(
    fields="name, date, location",
    source_type="news article",
    source_content=article_text
)
```

### Creative Writing

```python
template = """Write a {length} {genre} story about {topic}.

Style: {style}
Tone: {tone}
Target audience: {audience}

Story:"""

# Usage
prompt = template.format(
    length="500-word",
    genre="science fiction",
    topic="first contact with aliens",
    style="descriptive and immersive",
    tone="optimistic",
    audience="young adults"
)
```

### Code Generation

```python
template = """Generate {language} code to {task}.

Requirements:
{requirements}

Include:
- Clear variable names
- Comments explaining logic
- Error handling
- Example usage

Code:"""

# Usage
prompt = template.format(
    language="Python",
    task="read a CSV file and calculate statistics",
    requirements="- Use pandas\n- Handle missing values\n- Calculate mean, median, std dev"
)
```

---

## Prompt Management

### Version Control

```yaml
# prompts.yaml
summarization:
  version: 2.1
  template: |
    Summarize this {doc_type} in {length}.

    {doc_type}:
    {content}

    Summary:
  changelog:
    - v2.1: Added doc_type parameter
    - v2.0: Changed to structured format
    - v1.0: Initial version
```

### Programmatic Generation

```python
class PromptBuilder:
    def __init__(self):
        self.system = ""
        self.context = ""
        self.examples = []
        self.instruction = ""

    def set_system(self, message):
        self.system = message
        return self

    def add_context(self, text):
        self.context += f"\n{text}"
        return self

    def add_example(self, input, output):
        self.examples.append({"input": input, "output": output})
        return self

    def set_instruction(self, text):
        self.instruction = text
        return self

    def build(self):
        prompt = ""
        if self.system:
            prompt += f"System: {self.system}\n\n"
        if self.context:
            prompt += f"Context:{self.context}\n\n"
        if self.examples:
            prompt += "Examples:\n"
            for ex in self.examples:
                prompt += f"Input: {ex['input']}\nOutput: {ex['output']}\n\n"
        prompt += f"Instruction: {self.instruction}"
        return prompt

# Usage
prompt = (PromptBuilder()
    .set_system("You are a helpful assistant.")
    .add_context("We are building a customer support bot.")
    .add_example("How do I reset my password?", "Click 'Forgot Password' on the login page.")
    .set_instruction("Answer this: How do I change my email?")
    .build())
```

---

## Evaluation Metrics

### Accuracy

```python
def evaluate_accuracy(predictions, ground_truth):
    correct = sum(p == gt for p, gt in zip(predictions, ground_truth))
    return correct / len(predictions)
```

### Semantic Similarity

```python
from sentence_transformers import SentenceTransformer, util

model = SentenceTransformer('all-MiniLM-L6-v2')

def semantic_score(response, reference):
    emb1 = model.encode(response)
    emb2 = model.encode(reference)
    return util.cos_sim(emb1, emb2).item()
```

### LLM-as-Judge

```python
def llm_judge(response, criteria):
    judge_prompt = f"""Evaluate this response on {criteria}.
Score from 1-10.

Response: {response}

Score (1-10):"""

    score = llm.generate(judge_prompt)
    return int(score.strip())
```

---

## Related Resources

- [Agents & Orchestration](agents-orchestration.md) - Prompt-based agents
- [RAG & Knowledge](rag-knowledge.md) - RAG prompting
- [Evaluation & Testing](evaluation-testing.md) - Test prompts
- [Foundation Models](foundation-models.md) - Model-specific prompting

---

## Further Reading

- [OpenAI Prompt Engineering Guide](https://platform.openai.com/docs/guides/prompt-engineering)
- [Anthropic Prompt Engineering](https://docs.anthropic.com/claude/docs/prompt-engineering)
- [Prompt Engineering Guide (DAIR.AI)](https://www.promptingguide.ai/)
- [Learn Prompting](https://learnprompting.org/)

---

[← Back to Home](../index.md) | [Next: AI Safety & Alignment →](ai-safety-alignment.md)
