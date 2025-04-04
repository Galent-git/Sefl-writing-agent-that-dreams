# Eon Agent: A Conceptual Exploration of Self-Reflective AI

## Overview

Eon Agent is a Python-based conceptual prototype exploring ideas around AI agent metacognition, dynamic functionality, and simulated internal states ("dreaming"). It simulates an agent that processes tasks, reflects on them through generated "dreams," maintains a simple memory, and conceptually explores the idea of self-modification by checking for required functions and *simulating* their generation via Large Language Models (LLMs).

**This project is primarily an exploration and thought experiment, not a production-ready or robustly autonomous system.** Its value lies in demonstrating concepts and prompting discussion about the future possibilities and inherent challenges of more sophisticated AI agents.

## Core Concepts Explored

1.  **Task Processing:** The agent accepts natural language queries and attempts to process them, either through pre-defined functions or by leveraging an LLM.
2.  **Conceptual Self-Writing/Dynamic Functionality:** The agent explores the *idea* of modifying its own capabilities. It includes a mechanism (`check_or_simulate_function`) that checks if specific functions needed for a task (e.g., `generate_report`) exist locally. If not, it logs a message indicating it *would conceptually* use an LLM to generate the required code. **For safety and stability, this prototype does *not* execute dynamically generated code or modify its own script file during runtime by default.** It relies on pre-defined functions if available.

    *   **Experimental (Unsafe) Code Included:** For purely illustrative and conceptual purposes, the source code (`eon_agent.py`) also contains a separate, **unused by default**, function (`_unsafe_generate_and_append_function`) that demonstrates the *original technical approach* of calling an LLM and appending the generated code to the script file. **This function is accompanied by strong warnings in its docstring and is inherently unsafe.** See the "Ethical Considerations and Limitations" section for more details on the risks.
3.  **Simulated Metacognition ("Dreaming"):** After processing a task, the agent uses a high-temperature LLM call to generate a surreal, symbolic "dream" reflecting on the task. This explores the idea of non-utilitarian, internal states in AI.
4.  **Memory:** The agent logs its interactions (queries, results) to a persistent JSON file, providing a basic history.
5.  **LLM Integration:** Designed to work with multiple LLM backends (OpenAI, Google Gemini, local Ollama models) for flexibility.

## Features

*   Modular Python class structure.
*   Simple JSON-based memory persistence.
*   Markdown file logging for "dreams."
*   Conceptual simulation of self-writing/dynamic function checking.
*   Surreal "dream" generation based on task context.
*   Support for multiple LLM providers:
    *   OpenAI (via `openai` library)
    *   Google Gemini (via `google-generativeai` library)
    *   Ollama (via local API endpoint and `requests`)
*   Basic logging for monitoring agent activity.

## Tech Stack

*   Python 3.8+
*   Required Libraries: `openai`, `google-generativeai`, `requests` (install based on chosen LLM provider)
*   LLM Backend: Access to OpenAI API, Google AI Studio API, or a running local Ollama instance.

## Setup and Usage

1.  **Clone the Repository:**
    ```bash
    git clone <your-repo-link>
    cd <your-repo-directory>
    ```

2.  **Install Dependencies:**
    ```bash
    # Install libraries based on the LLM(s) you plan to use
    pip install requests # For Ollama
    pip install google-generativeai # For Google Gemini
    pip install openai # For OpenAI
    ```

3.  **Configure Environment Variables:**
    *   **For OpenAI:** Set `OPENAI_API_KEY` to your API key.
    *   **For Google:** Set `GOOGLE_API_KEY` to your API key.
    *   **For Ollama:** Ensure Ollama is running (e.g., `ollama serve`). You can optionally set `OLLAMA_URL` if it's not running on the default `http://localhost:11434`.
    *   Set `LLM_PROVIDER` to `openai`, `google`, or `ollama` (defaults to `ollama`).
    *   Optionally set `MODEL_NAME` to specify a model (e.g., `gpt-4`, `gemini-1.5-pro-latest`, `llama3`); defaults are provided in the script.

    *(Example for Bash/Zsh)*
    ```bash
    export OPENAI_API_KEY='your_openai_key'
    export GOOGLE_API_KEY='your_google_key'
    export LLM_PROVIDER='google' # Or 'openai' or 'ollama'
    # export MODEL_NAME='gemini-1.5-pro-latest' # Optional
    ```

4.  **Run the Agent:**
    ```bash
    python eon_agent.py
    ```
    The script will run a few predefined cycles. You can uncomment the interactive loop at the bottom of the script for manual querying.

## Ethical Considerations and Limitations

*   **Self-Modification Risks (Conceptual vs. Unsafe Demo):**
    *   The agent's default behavior **simulates** self-writing conceptually without executing generated code or modifying files, ensuring basic safety for experimentation.
    *   The codebase includes an **experimental, unsafe function (`_unsafe_generate_and_append_function`)** that demonstrates the *technical* possibility of LLM-driven code generation and file appending. **This function is NOT called by default and is extremely risky.** Executing LLM-generated code without strict sandboxing, validation, and security reviews can lead to critical vulnerabilities, instability, or unintended behavior. It is included for academic/conceptual demonstration only and should not be enabled or used without fully understanding and mitigating the associated dangers.
*   **"Dreaming" is Generative:** # ... (Keep existing text) ...
*   **LLM Reliability:** # ... (Keep existing text) ...
*   **Basic Memory:** # ... (Keep existing text) ...

# ... (Keep Future Ideas, Contributing) ...
*   **"Dreaming" is Generative:** The dreams are creative text outputs generated by an LLM based on a prompt. They do not represent genuine consciousness, understanding, or internal subjective experience. It's an exploration of simulating such states.
*   **LLM Reliability:** The quality of responses, generated code (in simulation), and dreams depends entirely on the capabilities and potential biases of the underlying LLM.
*   **Basic Memory:** The memory system is simple and non-semantic. The agent doesn't deeply learn from or reason about its past experiences.

## Future Ideas

*   Implement safer mechanisms for dynamic functionality (e.g., plugin system, sandboxed execution).
*   Develop a more sophisticated memory system (e.g., vector database for semantic recall).
*   Allow dreams to subtly influence future task processing or agent "mood."
*   Explore different "dreaming" techniques beyond simple LLM prompts.
*   Integrate external tools or APIs for the agent to use.

## Contributing

This is a personal exploration project. Feel free to fork, experiment, and share your findings. Discussions about the concepts are welcome.

---
*Conceptualized and built as an exploration into the potential and pitfalls of autonomous, self-reflective AI systems.*
