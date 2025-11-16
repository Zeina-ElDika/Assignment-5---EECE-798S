# MCP Map Servers – Agents Course Assignment

This repository contains my solution to the **C5 – MCP Map Servers** assignment in the Agents course.

The goals are:

- To understand the **Model Context Protocol (MCP)** as a standard way for models to access external tools and data.
- To design and implement at least **two map servers** exposing operations for geocoding, POI search, routing, and tiles.
- To integrate these servers into a small project using the **OpenAI Agents SDK**, so an agent can call the tools from natural-language queries.

The main deliverable is the notebook:

- `map_servers_agent.ipynb` – contains the MCP/map-server summary, the tool implementations, the MapAssistant agent, and demonstration cells.

---

## 1. Requirements

- Python 3.10+ (tested in Google Colab)
- OpenAI API key with access to the Agents SDK (stored as a secret called `KEY` in Colab)
- Internet access (for Nominatim and OSRM demo endpoints)

Python packages:

- `openai-agents`
- `openai`
- `httpx`

---

## 2. Installation & Setup (Colab)

1. **Upload the notebook** `map_servers_agent.ipynb` to Google Colab.

2. **Add your OpenAI API key as a secret**:
   - In Colab, go to **Settings → Secrets**.
   - Add a new secret with:
     - **Name:** `KEY`
     - **Value:** your OpenAI API key.

3. **Install the correct packages in the first code cell:**

```python
!pip uninstall -y agents
!pip install -U openai-agents openai httpx
```

4. **Configure your API key:**

```python
import os, openai

if "KEY" not in os.environ:
    raise RuntimeError("Please add your OpenAI key as a secret named KEY in Colab.")

os.environ["OPENAI_API_KEY"] = os.environ["KEY"]
openai.api_key = os.environ["OPENAI_API_KEY"]

print("API key configured.")
```

5. **Run all remaining notebook cells** to initialize tools and the agent.

---

## 3. Demo Instructions

To run the demo, execute:

```python
await ask_map_agent_with_details(
    "Search for at least three coffee shops in Hamra, Beirut and plan a driving route between the first two."
)
```

The output includes:
- A natural-language summary of the POI results and driving route.
- A trace of tool calls showing calls to Nominatim and OSRM.

---

## 4. Repository Structure

```
├── README.md
├── map_servers_agent.ipynb
├── part1_summary.md
├── video_script.md
```

---

## 5. Notes

- Nominatim and OSRM demo services are rate-limited.
- Production systems require hosted services and caching.
- The focus of this assignment is tool schema design, MCP concepts, and agent reasoning using the OpenAI Agents SDK.

---

## 6. Reflection

This project demonstrated how MCP principles translate to practical tool integration. By structuring each geospatial operation as a tool with a clear JSON schema, the agent could automatically chain POI search, geocoding, and routing based on natural-language instructions. The OpenAI Agents SDK handled tool selection and execution.

A notable challenge was uninstalling the unrelated reinforcement-learning `agents` package in Colab and installing the correct `openai-agents` package. Another challenge was handling asynchronous execution in Colab, which required using top-level `await` instead of `asyncio.run`. Future improvements include deploying each map server as a standalone MCP server and adding an interactive map visualization using Leaflet or MapLibre.

---

## 7. Video Recording

The full video demonstrating the agent and map servers is available here:

https://drive.google.com/file/d/1DswQQOs5yfFARiI2yomH0NpWo73gMh9e/view?usp=drive_link

