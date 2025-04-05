# Project_Idea_2: Job Candidate "Due Diligence" Agent - Outline & WBS

This document outlines the structure and work plan for a Capstone Project focused on creating an AI agent to assist job candidates with company due diligence.

---

## Project Outline (Kaggle Notebook Structure)

1.  **Introduction & Use Case:**
    *   **Problem:** Job seekers lack deep, actionable insights into company health, culture shifts (due to deals, etc.), and ESOP potential from standard job platforms. Standard metrics like salary and job description are insufficient for assessing long-term fit and potential equity value.
    *   **Proposed Solution:** Develop an AI Agent within a Kaggle Notebook that simulates fetching diverse data (news, financials, reviews, funding) from various simulated sources. The agent will then synthesize this information into a structured report focusing specifically on potential employee impact and considerations relevant to Employee Stock Option Plans (ESOPs).
    *   **Value Proposition:** Empowering candidates to make more informed career decisions by providing context beyond the surface level, especially regarding growth trajectory, potential risks, and the realistic value of equity.
    *   **GenAI Capabilities to be Demonstrated:** (Explicitly list 5+ intended capabilities from the course list, e.g., Function Calling, Agents, Document Understanding, Long Context Window, Structured Output/JSON Mode, RAG, Few-Shot Prompting).

2.  **Setup & Environment:**
    *   Import necessary Python libraries (e.g., `google-generativeai`, `json`, potentially `langchain` if using its Agent framework).
    *   Configure API key access securely using Kaggle Secrets.
    *   Briefly explain the chosen libraries and model (e.g., Google Gemini via Vertex AI API).

3.  **Simulated Data Sources & Function Definitions:**
    *   **Explain Simulation:** Clearly state that for this Proof of Concept (PoC) within Kaggle, calls to external data sources (News APIs, Financial DBs, Review sites) are *simulated* using predefined functions returning sample data. This avoids the need for real API keys and focuses on the GenAI workflow.
    *   **Define Simulated Functions:** Present the Python function definitions used as "tools" for the agent. Example functions:
        *   `search_financial_news(company_name)`
        *   `search_press_releases(company_name)`
        *   `search_market_analysis(company_name, sector)`
        *   `search_employee_reviews(company_name)`
        *   `get_funding_history(company_name)`
        *(Show the actual Python code for these functions in the notebook, emphasizing they return hardcoded sample text).*
    *   **Show Sample Data:** Include examples of the text snippets these functions will return (representing news headlines/summaries, PR excerpts, review themes, funding round details).
    *   **(Demonstrates GenAI Capability: Function Calling - Defining the tools)**

4.  **The Agent's Core Logic:**
    *   **Explain Agent Approach:** Describe the chosen method for implementing the agent (e.g., using LangChain's ReAct framework, a custom Python loop managing state and function calls, etc.). Explain *why* an agent is suitable for orchestrating multiple data gathering steps.
    *   **Show Agent Initialization/Prompting (if applicable):** Display the code or prompt used to initialize the agent, defining its goal, personality (e.g., "You are a helpful financial analyst assistant"), and the list of available tools (the simulated functions).
    *   **Trace Agent Execution (Conceptual):** Use Markdown or comments to illustrate the agent's expected decision-making process:
        *   Input: `company_name = "Innovatech Inc."`
        *   Agent decides: Need financial news -> Calls `search_financial_news("Innovatech Inc.")`.
        *   Agent receives: [Simulated news text].
        *   Agent decides: Need funding info -> Calls `get_funding_history("Innovatech Inc.")`.
        *   Agent receives: [Simulated funding text].
        *   ...and so on.
    *   **(Demonstrates GenAI Capability: Agents)**

5.  **Information Processing & Context Preparation:**
    *   **Gathering Results:** Show the code that collects the string outputs from all the simulated function calls made by the agent.
    *   **Preparing Context for LLM:** Explain how this aggregated text (potentially long) is formatted or prepared to be fed into the final LLM call for synthesis. Discuss any simple preprocessing if done (e.g., adding headers before each source's text).
    *   **(Demonstrates GenAI Capabilities: Document Understanding, Long Context Window)**

6.  **Synthesizing Insights & Structured Output Generation:**
    *   **Final Analysis Prompt:** Display the complete, detailed prompt given to the LLM for the final analysis. This prompt must:
        *   Clearly state the input is a collection of information about a company.
        *   Explicitly instruct the LLM to analyze specific aspects: `financial_health_summary`, `recent_deals_partnerships` (and their `potential_employee_impact`), `funding_status`, `employee_sentiment_themes`, and especially `esop_considerations`.
        *   Strictly instruct the LLM to format its entire response as a single **JSON object** matching a predefined schema. Include the schema definition in the prompt or description.
        *   (Optional but recommended) Include one or two examples (few-shot) within the prompt showing how to analyze "employee impact" or frame "ESOP considerations" based on sample inputs, guiding the AI's reasoning style.
    *   **Executing the Final LLM Call:** Show the Python code making the API call to the LLM (e.g., Gemini) with this carefully crafted prompt and the collected context.
    *   **Displaying the Result:** Print the raw response from the LLM, and then parse and pretty-print the resulting JSON object.
    *   **(Demonstrates GenAI Capabilities: Structured Output/JSON Mode, RAG (implicitly, by instructing analysis based *only* on provided context), Few-Shot Prompting (optional))**

7.  **Example Run & Analysis:**
    *   Execute the entire workflow within the notebook for at least one sample company name (e.g., "Innovatech Inc.").
    *   Present the final structured JSON report generated by the agent for that company.
    *   **Discuss Results:** Provide a brief analysis of the generated JSON. Does it successfully address the required sections (employee impact, ESOPs)? Is the information synthesized coherently based on the simulated input data?
    *   **Limitations:** This section is critical for a good score. Discuss the limitations honestly:
        *   Reliance on *simulated* data; real-world data is messier.
        *   Potential for LLM to hallucinate details not present in the provided context, despite instructions.
        *   Sensitivity to prompt phrasing.
        *   Bias in simulated data or the LLM itself.
        *   Analysis is high-level; not financial advice.
    *   **Capability Mapping:** Add a small section explicitly linking specific code cells or steps back to the GenAI capabilities listed in the introduction.

8.  **Conclusion & Future Work:**
    *   Summarize the project's achievement: Successfully demonstrated an AI agent concept capable of gathering simulated diverse data and synthesizing specific, deep insights for job candidate due diligence.
    *   Suggest potential future enhancements: Integrating real APIs, adding more sophisticated analysis modules (e.g., trend analysis), incorporating user feedback, comparing insights across multiple companies, using RAG against a larger internal knowledge base of analysis patterns.

---

## Work Breakdown Structure (WBS) - 10-Day AI-Assisted PoC

*   **Phase 1: Setup, Scope & Simulation Design (Days 1-2)**
    *   1.1 Define precise PoC scope: Finalize the exact simulated functions (3-5 functions are likely sufficient), the specific fields required in the output JSON schema, choose 1-2 sample "companies" for testing.
    *   1.2 Design core prompts: Draft the agent's initialization prompt (defining goal, tools) and the detailed final analysis/JSON generation prompt. Include the JSON schema definition.
    *   1.3 Kaggle Env Setup: Create notebook, install necessary libraries (`google-generativeai`, `json`, potentially `langchain`), configure API key using Kaggle Secrets.
    *   1.4 **(AI-Assisted)** Generate basic Python code structure: imports, API client initialization (e.g., `genai.configure`, `genai.GenerativeModel`).
    *   1.5 Prepare Sample Data: Write realistic (but concise) text snippets representing news articles, press releases, review themes, funding details for your chosen sample companies. Store these as Python strings or in simple text files accessible by the notebook.
    *   *Deliverable: Scoped plan document, Draft prompts (including JSON schema), Setup notebook with boilerplate code, Sample data snippets ready.*

*   **Phase 2: Implement Simulated Functions & Agent Logic (Days 3-5)**
    *   2.1 **(AI-Assisted)** Generate Python code for *each* defined simulated function (e.g., `search_financial_news`). These functions should accept `company_name` as input and return the corresponding pre-defined sample text snippet from step 1.5. Test each function individually to ensure they return the correct data. *(Demonstrates Function Calling Setup)*.
    *   2.2 **(AI-Assisted)** Implement the agent's core orchestration logic. Choose one path:
        *   *Option A (Simpler - Manual Orchestration):* Write Python code that explicitly calls each simulated function in sequence for the input company name. Store the returned text snippets in a list or dictionary.
        *   *Option B (Advanced - Using Agent Framework):* If comfortable, use a library like LangChain to define the functions as "tools" and set up an agent (e.g., ReAct agent) that decides which tools to call. Generate the code to run the agent executor. (Requires understanding agent concepts).
    *   2.3 **(AI-Assisted)** Generate code to aggregate all the text results collected (either from the manual calls or the agent execution) into a single large string or list of strings, ready to be used as context. *(Demonstrates Document Understanding, prepares for Long Context)*.
    *   *Deliverable: Working Python code for all simulated functions, Implemented agent/orchestration logic (Option A or B), Code to collect and aggregate context.*

*   **Phase 3: Implement Final Analysis & Structured Output (Days 6-7)**
    *   3.1 Refine Final Prompt: Based on initial thoughts and maybe quick tests, refine the final analysis prompt. Ensure it's very specific about the required JSON structure and the focus areas (employee impact, ESOPs). Add few-shot examples directly into the prompt string if desired. *(Demonstrates Prompt Engineering, Few-Shot Prompting)*.
    *   3.2 **(AI-Assisted)** Generate the Python code block for the final step:
        *   Takes the aggregated context string/list (from 2.3) as input.
        *   Constructs the final API call to the chosen LLM (e.g., Gemini) using the refined prompt and the aggregated context. Ensure model parameters (like temperature) are set appropriately.
        *   Retrieves the LLM's response (expected to be a JSON string).
        *   Includes error handling (e.g., a `try-except` block) to gracefully manage cases where the LLM response isn't valid JSON. Use the `json` library to parse the string.
    *   3.3 Test & Debug: Focus testing on this specific step. Does the LLM consistently return valid JSON matching the schema? Are the insights relevant to the input context? Use AI assistance to debug JSON parsing errors or refine the prompt if the output structure or content is incorrect. *(Demonstrates Structured Output/JSON Mode)*.
    *   *Deliverable: Robust code for the final analysis LLM call, including JSON parsing and basic error handling.*

*   **Phase 4: Documentation, End-to-End Testing & Demo Prep (Days 8-10)**
    *   4.1 Integrate & Test: Assemble all code blocks into the final Kaggle notebook structure outlined previously. Run the notebook from top to bottom for your 1-2 sample companies. Debug any issues encountered during the full run, using AI assistance as needed.
    *   4.2 Write Documentation: Fill in all the Markdown cells defined in the Project Outline. Provide clear explanations for each step, the code, the prompts, and the simulation approach. **Crucially, add the Limitations section and the Capability Mapping section.**
    *   4.3 Refine & Polish: Review the notebook for clarity, correctness, and readability. Ensure code cells are commented where necessary. Check that the notebook runs without errors.
    *   4.4 Prepare Demo: Plan a concise walkthrough of the notebook, highlighting the key steps: defining simulated functions, the agent's role (or manual orchestration), the final analysis prompt, and the structured JSON output. Be ready to explain the limitations and the demonstrated GenAI capabilities.
    *   *Deliverable: Completed, well-documented, and runnable Kaggle Notebook ready for submission.*
