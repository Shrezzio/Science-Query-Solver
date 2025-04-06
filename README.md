# AI Scientific Query/Doubts Center 🧪🔬🔭

[![Python Version](https://img.shields.io/badge/Python-3.9+-blue.svg)](https://www.python.org/downloads/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

An AI-powered simulator mimicking a multi-disciplinary science department to answer your science questions. This project leverages multiple specialized AI agents, orchestrated by CrewAI, using Google Gemini and Serper for web searches. It's designed primarily for Google Colab but can also be run locally.

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
*   **Flexible Environment:** Runs in Google Colab or locally with Python/Jupyter.

## Technology Stack 🛠️

*   **Framework:** CrewAI
*   **Language Model:** Google Gemini (`gemini-1.5-flash`)
*   **LLM Interface:** LangChain (`langchain-google-genai`)
*   **Web Search:** Serper API (`crewai[tools]`)
*   **Environment:** Google Colab / Local Python + Jupyter
*   **Language:** Python

## Getting Started: Setup Instructions

Choose **one** of the following setup methods:

### Method 1: Google Colab (Recommended - Easiest) ☁️

This project is designed to run easily within a Google Colab notebook.

**Prerequisites:**

*   A Google Account.
*   A **Google Gemini API Key:** Obtain from [Google AI Studio](https://aistudio.google.com/app/apikey) or Google Cloud Console. Ensure API is enabled and billing active if needed.
*   A **Serper API Key:** Obtain from [Serper.dev](https://serper.dev/).

**Steps:**

1.  **Open in Colab:** Click the "Open in Colab" badge (if available) or navigate to [Google Colab](https://colab.research.google.com/) and upload the `.ipynb` notebook file from this repository (`File -> Upload notebook...`).
2.  **Install Dependencies (Cell 1 & Runtime Restart):**
    *   Run the first cell (`# Cell 1: Install Necessary Packages...`).
    *   **CRITICAL:** After Cell 1 finishes, **restart the Colab Runtime** using the menu: `Runtime -> Restart Session`. This is crucial. **Do not run Cell 1 again after restarting.**
3.  **Configure API Keys (Cell 2):**
    *   Run Cell 2 (`# Cell 2: API Key Configuration...`).
    *   Follow the instructions in the cell's comments to uncomment the lines under `OPTION 2` and paste your **Gemini API Key** and **Serper API Key** into the respective strings.
    *   Ensure the cell runs successfully and prints the `✅ --- API Keys Seem Loaded...` message.
4.  **Run Setup Cells (Cells 3-7):** After restarting the runtime and running Cell 2, run Cells 3 through 7 sequentially, ensuring each completes successfully before proceeding. These cells import libraries, configure the LLM/tools, define agents/tasks, and create the Crew.

### Method 2: Local Setup (Running on Your PC) 💻

If you prefer to run this project locally:

**Prerequisites:**

*   **Git:** Installed on your system ([Download Git](https://git-scm.com/downloads)).
*   **Python:** Version 3.9 or higher installed ([Download Python](https://www.python.org/downloads/)).
*   **pip:** Python's package installer (usually included).
*   Your own valid **Gemini API Key** and **Serper API Key**.

**Steps:**

1.  **Clone the Repository:**
    Open your terminal or command prompt and navigate to where you want to store the project. Then run:
    ```bash
    git clone https://github.com/[Your-GitHub-Username]/[Your-Repository-Name].git
    cd [Your-Repository-Name]
    ```
    *(Replace `[Your-GitHub-Username]` and `[Your-Repository-Name]` with your actual details)*

2.  **Create and Activate Virtual Environment (Recommended):**
    ```bash
    # Create environment
    python -m venv venv
    # Activate (Windows)
    .\venv\Scripts\activate
    # Activate (macOS/Linux)
    source venv/bin/activate
    ```

3.  **Install Dependencies:**
    Install required packages using the `requirements.txt` file.
    ```bash
    pip install -r requirements.txt
    ```
    *(Make sure the `requirements.txt` file exists in the repository)*

4.  **Configure API Keys (Using `.env` file):**
    *   Create a file named `.env` in the project's root directory.
    *   Add your keys to the `.env` file:
        ```dotenv
        GEMINI_API_KEY="YOUR_ACTUAL_GEMINI_KEY_HERE"
        SERPER_API_KEY="YOUR_ACTUAL_SERPER_KEY_HERE"
        ```
    *   **Ensure `.env` is listed in `.gitignore`** to prevent committing secrets.

5.  **Run the Jupyter Notebook:**
    *   Ensure your virtual environment is active.
    *   Install Jupyter if needed: `pip install notebook`
    *   Start the server: `jupyter notebook`
    *   Open the `.ipynb` file in the browser interface.
    *   **Run the cells sequentially:**
        *   **SKIP Cell 1** (Installation).
        *   **Run Cell 2:** Verify it loads keys correctly from your `.env` file (leave Option 2 commented out in the code).
        *   Run Cells 3 through 7.

## Usage Instructions ▶️

**(Applicable after completing either Colab or Local Setup)**

1.  Ensure Cells 1-7 (or 2-7 for local setup) have run successfully.
2.  Navigate to the final cell, `# Cell 8: Kickoff the Simulation...`.
3.  Run Cell 8.
4.  When prompted in the output:
    *   `Enter the topic:` Type your topic (e.g., `black holes`) and press Enter.
    *   `Enter your question or prompt:` Type your question (e.g., `what is Hawking radiation?`) and press Enter.
5.  The CrewAI agents will begin processing. Verbose output logs their actions. This might take a minute or more.
6.  The final, Markdown-formatted answer will appear under `--- Final Formatted Output ---`.

*   **Note on Errors:** `503 Service Unavailable` indicates temporary Google server overload; wait and retry Cell 8. Ensure API keys remain valid.

## How It Works 🧠

1.  **Input & Normalization:** User input (topic, prompt) is taken and converted to lowercase.
2.  **Kickoff:** The `inputs` dictionary is passed to the `Crew.kickoff()` method.
3.  **Task 1 (Intake):** `query_intake_agent` refines the prompt using Gemini.
4.  **Task 2 (Analysis):** A relevant science agent (initially `theoretical_physicist_agent`, potentially delegated) analyzes the refined prompt using Gemini. It may use the `web_scraper_tool` (Serper) if external info is needed.
5.  **Task 3 (Formatting):** `output_formatting_agent` formats the technical response using Gemini and Markdown.
6.  **Final Output:** The formatted result is returned.

## Future Enhancements 🚀

*   Add more specialized science agents (e.g., Chemistry, Biology).
*   Implement conversational memory (`memory=True`).
*   Develop more sophisticated agent selection/delegation logic.
*   Integrate other tools (calculation, database lookup).
*   Improve error handling robustness.
*   Build a simple web interface (Streamlit/Flask).
*   Implementing a Chatbot if possible!

## Contributing 🤝

Contributions, issues, and feature requests are welcome!
## License 📄

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Disclaimer ⚠️

This is an experimental project using generative AI. Output should be verified for accuracy and completeness. The AI may hallucinate or provide incorrect information. Use responsibly.
