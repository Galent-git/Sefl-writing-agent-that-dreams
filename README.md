# Eon Agent: A Conceptual Exploration of Self-Reflective AI

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

**Status: Experimental / Conceptual**

Eon Agent is a Python prototype exploring ideas around AI agent metacognition, dynamic functionality, and simulated internal states ("dreaming"). It simulates an agent that processes tasks, reflects on them through generated "dreams," maintains a simple memory, and **conceptually explores the idea of self-modification**.

**Crucially, by default, this agent operates safely.** It checks if necessary Python functions exist locally. If not, it *simulates* the idea of generating them via a Large Language Model (LLM) by logging a message, but **does not actually generate or execute new code, nor modify its own script file.**

This project is primarily an **exploration and thought experiment**, not a production-ready system. Its value lies in demonstrating concepts related to potentially more sophisticated future AI agents and prompting discussion about their possibilities and inherent challenges.

## Core Concepts Explored

1.  **Task Processing:** Accepts natural language queries and processes them using either pre-defined local Python functions or a general-purpose LLM call.
2.  **SAFE Conceptual Self-Writing Simulation (Default Behavior):**
    *   The agent checks if specific Python functions (e.g., `generate_report`) required for certain tasks exist within its codebase (`eon_agent.py`).
    *   It uses Python's `importlib` for this check – **no code is generated or executed if the function is missing.**
    *   If a required function is **not found**, the agent logs a message stating it *would conceptually* use an LLM to generate it, simulating the *idea* of dynamic functionality without the associated risks.
3.  **Simulated Metacognition ("Dreaming"):** After processing a task, the agent uses an LLM (often with higher 'temperature' settings for creativity) to generate a short, surreal, symbolic "dream" reflecting on the task, exploring non-utilitarian internal states.
4.  **Memory:** Logs interactions (queries, results) to a persistent JSON file (`memory.json`) and dreams to a Markdown file (`dreams.md`).
5.  **Multi-LLM Integration:** Designed to flexibly work with different LLM backends:
    *   OpenAI (GPT-3.5, GPT-4, etc.) via `openai` library.
    *   Google Gemini (Gemini Pro, Flash, etc.) via `google-generativeai` SDK.
    *   Local models via Ollama (Llama3, Mistral, etc.) using `requests`.

## WARNING: Includes Unsafe Demonstrative Code

For purely illustrative and conceptual purposes, the source code (`eon_agent.py`) **also contains a separate function (`_unsafe_generate_and_append_function`)** that demonstrates the original technical *idea* of calling an LLM to generate Python code and append it to the script file.

*   **This function is NOT called by the agent during its normal operation.**
*   It is **explicitly marked as UNSAFE** and accompanied by strong warnings in the code and comments.
*   **EXECUTING CODE GENERATED BY AN LLM WITHOUT RIGOROUS SANDBOXING, VALIDATION, AND SECURITY REVIEW IS EXTREMELY DANGEROUS.** It can lead to arbitrary code execution, security vulnerabilities, data loss, and system instability.
*   An option to run this unsafe function (requiring explicit confirmation) is included in the `if __name__ == "__main__"` block for **demonstration only**. **Do not enable or run this unless you fully understand and accept the significant risks.**

## Technology

*   **Language:** Python 3.8+
*   **Core Libraries:** `requests`, `python-dotenv`
*   **Optional LLM Libraries:** `openai`, `google-generativeai` (install based on chosen provider)
*   **LLM Backend:** Access to OpenAI API, Google AI Studio API, or a running local Ollama instance.

## Setup and Usage

1.  **Clone Repository:**
    ```bash
    git clone https://github.com/your-username/eon-agent.git # Replace with your repo URL
    cd eon-agent
    ```

2.  **Create Virtual Environment (Recommended):**
    ```bash
    python -m venv venv
    source venv/bin/activate  # On Windows: venv\Scripts\activate
    ```

3.  **Install Dependencies:**
    *   Install base requirements:
        ```bash
        pip install -r requirements.txt
        ```
    *   Install the library for your chosen LLM provider(s) if not already covered (see `requirements.txt` for package names):
        ```bash
        # Example for OpenAI:
        # pip install openai
        # Example for Google Gemini:
        # pip install google-generativeai
        ```

4.  **Configure Environment Variables:**
    *   Copy the example file:
        ```bash
        cp .env.example .env
        ```
    *   **Edit the `.env` file:**
        *   Set `LLM_PROVIDER` to `openai`, `google`, or `ollama` (defaults to `ollama`).
        *   Fill in the required API key (`OPENAI_API_KEY` or `GOOGLE_API_KEY`) for your chosen cloud provider. Keys for unused providers can be left as placeholders.
        *   Optionally, set `MODEL_NAME` to specify a particular model (e.g., `gpt-4`, `gemini-1.5-pro-latest`, `llama3`). Defaults are provided in the script.
        *   Ensure `OLLAMA_URL` and `OLLAMA_CHECK_URL` are correct if using Ollama and it's not on the default `http://localhost:11434`.
    *   **Security:** The `.env` file contains secrets. **Do not commit `.env` to Git.** The provided `.gitignore` should prevent this.

5.  **Run Ollama (if using):**
    If `LLM_PROVIDER` is `ollama`, ensure the Ollama server is running in a separate terminal:
    ```bash
    ollama serve
    ```
    Also ensure you have pulled the model specified in `.env` or the script default (e.g., `ollama pull mistral`).

6.  **Run the Agent:**
    ```bash
    python eon_agent.py
    ```
    The script will run a few predefined demonstration cycles and then enter an interactive loop where you can type queries. Type `quit` to exit. Check `memory.json` and `dreams.md` for output.

## Ethical Considerations and Limitations

*   **Self-Modification Risks (Handled via Simulation):** The **default safe mode** only simulates the *idea* of self-modification. The **included unsafe demo function** highlights the extreme risks of executing LLM-generated code without safeguards. Use with extreme caution if you choose to explore it.
*   **"Dreaming" is Generative:** Dreams are creative LLM outputs, not genuine consciousness or subjective experience. It's a simulation exploring such concepts.
*   **LLM Reliability & Bias:** Output quality depends entirely on the chosen LLM. Biases or inaccuracies in the LLM will be reflected.
*   **Basic Memory:** Memory is a simple chronological log, not a deep semantic understanding of the past.
*   **Error Handling:** Basic error handling is included, but complex failures in LLM communication or file access might occur.

## Future Ideas

*   Implement safer dynamic functionality (e.g., sandboxed code execution, plugin system).
*   Explore vector databases for semantic memory retrieval.
*   Allow "dreams" to subtly influence agent state or responses (conceptual "mood").
*   Integrate external tools/APIs via function calling (if supported by the LLM).
*   Develop more sophisticated pre-defined functions for the agent to utilize.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
