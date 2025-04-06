# AI Scientific Query/Doubts Center 🧪🔬🔭

[![Python Version](https://img.shields.io/badge/Python-3.9+-blue.svg)](https://www.python.org/downloads/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

An AI-powered simulator mimicking a multi-disciplinary science department to answer your science questions. This project leverages multiple specialized AI agents, orchestrated by CrewAI, running within a Google Colab notebook.

## Overview

This project simulates a virtual "Science Department Doubt Center". When a user provides a science-related topic and a question/prompt, a team of AI agents collaborates to provide a comprehensive and well-formatted answer. The process involves:

1.  **Query Intake:** An AI agent clarifies and refines the user's prompt.
2.  **Specialized Analysis:** The task is routed to the most relevant science agent (e.g., Theoretical Physics, Quantum Mechanics, Astrophysics, Electrical Engineering, Mathematics).
3.  **Web Research (Optional):** Science agents can utilize the Serper API for real-time web searches to gather current information if needed.
4.  **Output Formatting:** A final agent polishes the scientific response for clarity and presentation using Markdown.

## Features ✨

*   **Multi-Agent System:** Utilizes distinct AI agents with specialized roles (Physics, Quantum, Astro, EE, Math, Intake, Output).
*   **CrewAI Orchestration:** Leverages the CrewAI framework to manage agent collaboration and task sequences.
*   **Google Gemini Integration:** Uses Google's Gemini models (specifically `gemini-1.5-flash` via LangChain) for AI reasoning and text generation.
*   **Web Search Capability:** Agents can perform real-time web searches using the Serper API for up-to-date information.
*   **Dynamic Task Handling:** Agents can potentially delegate tasks to other specialists within the crew.
*   **Formatted Output:** Delivers answers in a clean, Markdown-formatted style.
*   **Colab Environment:** Designed to run easily within a Google Colab notebook.

## Technology Stack 🛠️

*   **Framework:** CrewAI
*   **Language Model:** Google Gemini (`gemini-1.5-flash`)
*   **LLM Interface:** LangChain (`langchain-google-genai`)
*   **Web Search:** Serper API (`crewai[tools]`)
*   **Environment:** Google Colab / Jupyter Notebook
*   **Language:** Python

## Setup and Installation ⚙️

This project is designed to run in Google Colab.

**Prerequisites:**

1.  **Google Account:** To use Google Colab.
2.  **Google Gemini API Key:** Obtain from [Google AI Studio](https://aistudio.google.com/app/apikey) or your Google Cloud Console project. Ensure the API is enabled and billing is active if required.
3.  **Serper API Key:** Obtain from [Serper.dev](https://serper.dev/). A free plan is often sufficient for moderate use.

**Steps:**

1.  **Clone or Download:**
    *   Clone this repository: `git clone [Link to your repository]`
    *   OR Download the `.ipynb` notebook file directly.
2.  **Upload to Colab:** Open [Google Colab](https://colab.research.google.com/) and upload the `.ipynb` file (`File -> Upload notebook...`).
3.  **Configure API Keys (Cell 2):**
    *   Open the notebook in Colab.
    *   Navigate to the cell titled `# Cell 2: API Key Configuration...`.
    *   Follow the instructions within the cell's comments:
        *   Uncomment the lines under `# --- OPTION 2: Paste keys directly ---`.
        *   Replace `"YOUR_NEW_VALID_GEMINI_KEY"` with your actual Gemini API Key.
        *   Replace `"YOUR_VERIFIED_ACTIVE_SERPER_KEY"` with your actual Serper API Key.
    *   Run Cell 2 and verify the success message `✅ --- API Keys Seem Loaded...`.
4.  **Install Dependencies (Cell 1 & Runtime Restart):**
    *   Run the cell titled `# Cell 1: Install Necessary Packages...`.
    *   **CRITICAL:** After Cell 1 finishes, **restart the Colab Runtime** using the menu: `Runtime -> Restart Session`. This ensures the correct library versions are loaded. **Do not run Cell 1 again after restarting.**
5.  **Run Setup Cells:** After restarting the runtime, run the following cells sequentially, ensuring each completes successfully before proceeding to the next:
    *   Cell 2 (API Keys - already configured, just run it again)
    *   Cell 3 (Imports)
    *   Cell 4 (Configure LLM/Tools)
    *   Cell 5 (Define Agents)
    *   Cell 6 (Define Tasks)
    *   Cell 7 (Create Crew)

## Usage Instructions ▶️

1.  After successfully running Cells 1 through 7 (including the Runtime Restart after Cell 1):
2.  Navigate to the final cell, `# Cell 8: Kickoff the Simulation...`.
3.  Run Cell 8.
4.  The notebook will prompt you to:
    *   `Enter the topic:` (e.g., `Quantum Physics`)
    *   `Enter your question or prompt:` (e.g., `explain superposition in simple terms`)
5.  Press Enter after each input. The input will be normalized to lowercase.
6.  The CrewAI agents will start processing. Verbose output will show the agents thinking and acting. This may take some time depending on the complexity and required web searches.
7.  Wait for the execution to complete. The final, formatted answer will be printed under `--- Final Formatted Output ---`.

*   **Note on Errors:**
    *   If you encounter `503 Service Unavailable` errors, Google's Gemini servers may be temporarily overloaded. Wait a few minutes and try running Cell 8 again.
    *   Ensure your API keys entered in Cell 2 remain valid and active.

## How It Works 🧠

1.  **Input & Normalization:** User input (topic, prompt) is taken and converted to lowercase.
2.  **Kickoff:** The `inputs` dictionary is passed to the `Crew.kickoff()` method.
3.  **Task 1 (Intake):** The `query_intake_agent` receives the initial input, uses the LLM (Gemini) to refine the prompt for clarity and actionability, and outputs only the refined prompt string.
4.  **Task 2 (Science Analysis):**
    *   The `theoretical_physicist_agent` (or potentially another agent if delegation occurs) receives the refined prompt via context.
    *   It uses its defined role, goal, backstory, and the LLM to analyze the prompt.
    *   If it determines external information is needed, it can formulate a query and use the `web_scraper_tool` (Serper API).
    *   It generates a technical response.
5.  **Task 3 (Formatting):** The `output_formatting_agent` receives the technical response via context and uses the LLM to reformat it according to the specified style (Markdown, clarity, structure) without changing the scientific content.
6.  **Final Output:** The result from the formatting agent is returned as the final output of the `kickoff` call and printed to the user.

## Future Enhancements 🚀

*   Add more specialized science agents (e.g., Chemistry, Biology).
*   Implement conversational memory (`memory=True` in `Crew`) for follow-up questions.
*   Develop more sophisticated logic for agent selection/delegation.
*   Integrate other tools (e.g., code execution for calculations, database lookup).
*   Improve error handling for API issues or unexpected agent behavior.
*   Build a simple web interface (using Streamlit or Flask) instead of running in Colab.

## Contributing 🤝

Contributions, issues, and feature requests are welcome!

## License 📄

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details.

## Disclaimer ⚠️

This is an experimental project using generative AI. While it aims to provide helpful scientific explanations, the output should always be verified for accuracy and completeness, especially for critical applications. The AI may hallucinate or provide incorrect information. Use responsibly.
