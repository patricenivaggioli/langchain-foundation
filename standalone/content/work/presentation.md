---
marp: true
theme: default
paginate: true
backgroundColor: #fff
style: |
  section {
    font-size: 24px;
    padding: 50px;
  }
  h1 {
    color: #0078D4;
  }
  h2 {
    color: #004E8C;
  }
---

# Building AI Agents with LangChain

## A Comprehensive Guide

---

# Agenda

1. Foundational Models
2. Prompt Engineering
3. Tools & Actions
4. Web Search Integration
5. Memory & State
6. Multimodality
7. Project: Personal Chef

---

# 1. Foundational Models

## The "Brain" of the Agent

- **Chat Models**: Serve as the reasoning engine.
- **Model Agnostic**: LangChain allows switching providers (OpenAI, Claude, Gemini) with minimal code changes.
- **Interaction**: 
  - Input: Prompts/Messages.
  - Output: AI Messages.

---

# Configuring Models

Models can be fine-tuned via parameters:

- **Temperature**: Controls randomness (0 = deterministic, 1 = creative).
- **Max Tokens**: Limits output length.
- **Timeout & Retries**: Manages latency and reliability.

```python
model = ChatOpenAI(
    temperature=0, 
    model="gpt-4o"
)
```

---

# Agents vs. Models

- **Models**: Passive "thinkers".
- **Agents**: Active systems that use "tools" to interact with the world.
- **Workflow**:
  1. Initialize Model.
  2. Create Agent (`create_agent`).
  3. Invoke with user input.

---

# 2. Prompt Engineering

## Shaping Behavior

System prompts are the easiest way to modify performance and persona.

- **Role Setting**: "You are a science fiction writer..."
- **Few-Shot Prompting**: Providing examples (Input -> Output) to guide style.
- **Structural Constraints**: Defining specific formats for the answer.

---

# Structured Output

Forcing the model to return data in a specific schema (e.g., JSON, Pydantic objects).

- Vital for programmatic usage of the agent's response.
- Ensures consistency in data extraction.

---

# 3. Tools & Actions

## The ReAct Pattern

Agents use the **ReAct** (Reason + Act) pattern.

- **Definition**: Use the `@tool` decorator on Python functions.
- **Discovery**: Agents use function names and docstrings to understand *when* and *how* to use a tool.

```python
@tool
def square_root(x: float) -> float:
    """Calculate the square root of a number"""
    return x ** 0.5
```

---

# Tool Execution Flow

1. **Human Message**: User asks a question.
2. **AI Message (Tool Call)**: Agent decides to call a tool.
3. **Tool Message**: The output of the function execution.
4. **Final AI Message**: Agent formulates the answer based on tool output.

---

# 4. Web Search Integration

## Real-Time Knowledge

- LLMs have a knowledge cutoff (static training data).
- **Web Search** connects agents to the live internet.
- **Usage**:
  - Integrate tools like `TavilyClient`.
  - Agent queries the web when internal knowledge is insufficient.

---

# 5. Memory & State

## From Stateless to Stateful

- **Default**: LLMs are stateless (each call is independent).
- **Memory**: Allows the agent to remember context across turns.
- **Implementation**:
  - Use `checkpointer` (e.g., `InMemorySaver`).
  - Pass a `thread_id` config to maintain conversation history.

---

# 6. Multimodality

## Beyond Text

Modern agents can process multiple types of input:

- **Text**: Standard interaction.
- **Images**: Sending base64 encoded images for analysis.
- **Audio**: Recording and processing audio data.

Allows for more natural and versatile user interfaces.

---

# 7. Project: Personal Chef

## Putting It All Together

We will build a **Personal Chef Agent** that:

1. Takes a **list of ingredients**.
2. Uses **Web Search** to find recipes.
3. Provides **instructions**.
4. Remembers context for **follow-up questions**.

---

# Ready to Start?

Let's dive into the notebooks!
