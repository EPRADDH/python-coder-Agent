# Coder Crew: Multi-Agent Python Coding with crewAI

Welcome to **Coder Crew**, a template for building collaborative, multi-agent AI systems using [crewAI](https://crewai.com). This project enables you to automate Python coding tasks by orchestrating AI agents that plan, write, execute, and validate code together.

---

## 🚀 Features
- **Multi-agent orchestration**: Define agents with unique roles and goals.
- **Task automation**: Assign complex coding tasks to your AI crew.
- **Custom tools**: Extend agent capabilities with your own Python tools.
- **Safe code execution**: Uses Docker for secure code runs.
- **Easy configuration**: YAML-based agent and task setup.

---

## 🛠️ Prerequisites
- **Python**: >=3.10, <3.14
- **[UV](https://docs.astral.sh/uv/)**: For fast dependency management
- **OpenAI API Key**: For LLM-powered agents (add to `.env`)

---

## 📦 Installation
1. **Install UV** (if not already):
   ```bash
   pip install uv
   ```
2. **Clone this repository** and navigate to the project directory.
3. **Install dependencies**:
   ```bash
   uv pip install -r pyproject.toml
   ```
   Or, if using crewAI CLI:
   ```bash
   crewai install
   ```
4. **Set your OpenAI API key** in a `.env` file:
   ```env
   OPENAI_API_KEY=your-key-here
   ```

---

## ⚙️ Configuration

### Agents
- Define agent roles, goals, and LLMs in `src/coder/config/agents.yaml`.
- Example:
  ```yaml
  coder:
    role: Python Developer
    goal: You write python code to achieve this assignment: {assignment}
    backstory: You're a seasoned python developer with a knack for writing clean, efficient code.
    llm: openai/gpt-4o-mini
  ```

### Tasks
- Define tasks and expected outputs in `src/coder/config/tasks.yaml`.
- Example:
  ```yaml
  coding_task:
    description: Write python code to achieve this: {assignment}
    expected_output: A text file that includes the code itself, along with the output of the code.
    agent: coder
    output_file: output/code_and_output4.txt
  ```

---

## ▶️ Running the Project
From the root folder, run:
```bash
crewai run
```
Or, if you have a script entry point:
```bash
python -m coder.src.coder.main
```
This will:
- Assemble your agents and tasks
- Execute the workflow
- Output results and code to the `output/` directory

---

## 🧩 Customization
- **Add/modify agents**: Edit `agents.yaml` for new skills or personalities.
- **Add/modify tasks**: Edit `tasks.yaml` for new objectives.
- **Custom tools**: Add Python files in `src/coder/tools/` and register them with your agents.
- **Logic and workflow**: Edit `src/coder/crew.py` to change agent orchestration, add hooks, or customize execution.
- **Assignment input**: Change the `assignment` variable in `src/coder/main.py` to set the coding challenge.

---

## 📤 Output
- Results (code and output) are saved in the `output/` directory, e.g., `output/code_and_output4.txt`.
- You can change the output file in your task configuration.

---

## 🏆 Best Practices for Good Python Code
- **Plan before coding**: Agents are encouraged to outline their approach before writing code.
- **Write modular, readable code**: Use functions, docstrings, and clear variable names.
- **Handle errors gracefully**: Use try/except blocks where appropriate.
- **Validate output**: Agents should run and check code output, reporting errors or unexpected results.
- **Document assumptions**: If the code makes assumptions (e.g., about input data), document them in comments.
- **Use type hints**: For better clarity and static analysis.
- **Keep dependencies minimal**: Only import what you need.

---

## 🧰 Example: Adding a Custom Tool
To extend agent capabilities, add a tool in `src/coder/tools/custom_tool.py`:
```python
from crewai.tools import BaseTool
from typing import Type
from pydantic import BaseModel, Field

class MyCustomToolInput(BaseModel):
    argument: str = Field(..., description="Description of the argument.")

class MyCustomTool(BaseTool):
    name = "Name of my tool"
    description = "Clear description for what this tool is useful for."
    args_schema: Type[BaseModel] = MyCustomToolInput
    def _run(self, argument: str) -> str:
        # Implementation goes here
        return "tool output"
```
Register your tool with an agent in `crew.py`.

---

## 🐞 Troubleshooting
- **Python version errors**: Ensure you are using Python >=3.10 and <3.14.
- **API key issues**: Make sure your `.env` file is present and correct.
- **Docker errors**: Docker is required for safe code execution. Install [Docker Desktop](https://docs.docker.com/desktop/).
- **Dependency issues**: Reinstall with `uv pip install -r pyproject.toml` or `crewai install`.

---

## 📚 Resources & Support
- [crewAI Documentation](https://docs.crewai.com)
- [GitHub Issues](https://github.com/joaomdmoura/crewai)
- [Discord Community](https://discord.com/invite/X4JWnZnxPb)
- [Chat with crewAI Docs](https://chatg.pt/DWjSBZn)

---

Let's build powerful, collaborative Python solutions with Coder Crew and crewAI!
