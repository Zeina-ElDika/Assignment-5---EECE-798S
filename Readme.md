MCP Map Servers – Agents Course Assignment

This repository contains my solution to the C5 – MCP Map Servers assignment in the Agents course.

The goals are:

To understand the Model Context Protocol (MCP) as a standard way for models to access external tools and data.

To design and implement at least two map servers exposing operations for geocoding, POI search, routing, and tiles.

To integrate these servers into a small project using the OpenAI Agents SDK, so an agent can call the tools from natural-language queries.

The main deliverable is the notebook:

map_servers_agent.ipynb – contains the MCP/map-server summary, the tool implementations, the MapAssistant agent, and demonstration cells.

1. Requirements

Python 3.10+ (tested in Google Colab)

OpenAI API key with access to the Agents SDK (stored as a secret called KEY in Colab)

Internet access (for Nominatim and OSRM demo endpoints)

Python packages:

openai-agents

openai

httpx

2. Installation & Setup (Colab)

Upload the notebook map_servers_agent.ipynb to Google Colab.

Add your OpenAI API key as a secret:

In Colab, go to Settings → Secrets.

Add a new secret with:

Name: KEY

Value: your OpenAI API key.

Install the correct packages in the first code cell:

!pip uninstall -y agents
!pip install -U openai-agents openai httpx


Configure your API key:

import os, openai

if "KEY" not in os.environ:
    raise RuntimeError("Please add your OpenAI key as a secret named KEY in Colab.")

os.environ["OPENAI_API_KEY"] = os.environ["KEY"]
openai.api_key = os.environ["OPENAI_API_KEY"]

print("API key configured.")


Run all remaining notebook cells to initialize tools and the agent.
