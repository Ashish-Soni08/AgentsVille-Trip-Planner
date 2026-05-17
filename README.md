# AgentsVille Trip Planner

Build a multi-stage AI travel assistant for the fictional city of AgentsVille.

The project has two main parts:

1. **Expert Planner**: generates a structured, day-by-day itinerary from traveler preferences.
2. **Resourceful Assistant**: uses a ReAct-style loop with simulated tools to answer follow-up requests and refine the itinerary.

## Local Setup With uv

This project uses `uv` only. Do not use `pip` directly for setup.

### 1. Install Python With uv

If you do not already have a compatible Python, install one with:

```powershell
uv python install 3.12
```

Python 3.10 or newer is required by the pinned dependencies. Python 3.12 is recommended for this project.

### 2. Create the Virtual Environment

From the project directory:

```powershell
uv venv --python 3.12
```

Activate it on Windows:

```powershell
.venv\Scripts\activate
```

Activation is optional for most commands because `uv run ...` will use the project environment automatically.

### 3. Install Dependencies

```powershell
uv sync
```

If your global uv cache has local permission issues, keep the cache inside the project:

```powershell
$env:UV_CACHE_DIR=".uv-cache"
uv sync
```

The pinned project dependencies are:

- `json-repair==0.47.1`
- `numexpr==2.11.0`
- `openai==1.74.0`
- `pandas==2.3.0`
- `pydantic==2.11.7`
- `python-dotenv==1.1.0`
- `jupyterlab`
- `ipykernel`

### 4. Configure Your Vocareum OpenAI API Key

Create a `.env` file in the project root:

```text
VOC_OPENAI_API_KEY=voc-your-key-here
```

This project is configured for Vocareum OpenAI keys. All OpenAI SDK v1 requests are routed to:

```text
https://openai.vocareum.com/v1
```

The code also falls back to `OPENAI_API_KEY` if `VOC_OPENAI_API_KEY` is not set, but Vocareum keys are the expected default for this course project.

### 5. Start JupyterLab

```powershell
uv run jupyter lab
```

Open `project_starter.ipynb` and run the cells from top to bottom.

## Files

- `project_starter.ipynb`: notebook application starter.
- `project_lib.py`: Pydantic models, sample AgentsVille data, simulated tools, and helper functions.
- `pyproject.toml`: uv-managed project dependencies.
- `.env.example`: example environment file.

## Expected Workflow

1. Define traveler preferences.
2. Ask the LLM to produce a JSON itinerary.
3. Validate the result with Pydantic.
4. Ask follow-up questions.
5. Let the ReAct assistant decide when to call simulated tools.
6. Use tool observations to improve the final answer or itinerary.
