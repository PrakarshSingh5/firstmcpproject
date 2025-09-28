🌦️ Weather MCP Server

This project implements a Model Context Protocol (MCP) server that provides weather data from the National Weather Service (NWS) API
. It exposes tools that allow Claude (or any MCP-compatible client) to fetch weather alerts and forecasts for US locations.

🚀 Features

get_alerts → Get active weather alerts for a given US state (e.g., CA, NY).

get_forecast → Get weather forecast for a given latitude and longitude (US only).

Communicates with MCP clients over stdio transport.

Built with:

TypeScript

@modelcontextprotocol/sdk

Zod
 for input validation

📦 Setup
1. Clone and install
git clone https://github.com/your-username/mcpproject.git
cd mcpproject
npm install

2. Build

Since the project is written in TypeScript, you must compile it before running:

npm run start


👉 This will:

Compile TypeScript from src/ into build/

Run the compiled build/index.js file

🔧 Tools
get_alerts

Get weather alerts for a US state.
Input schema:

{
  "state": "CA"
}


Output example:

Active alerts for CA:

Event: Fire Weather Warning
Area: Southern California
Severity: Severe
Status: Actual
Headline: Red Flag Warning issued...
---

get_forecast

Get a weather forecast for a US latitude/longitude.
Input schema:

{
  "latitude": 34.0522,
  "longitude": -118.2437
}


Output example:

Forecast for 34.0522, -118.2437:

Today:
Temperature: 75°F
Wind: 10 mph SW
Sunny
---
Tonight:
Temperature: 58°F
Wind: 5 mph W
Clear
---

🔌 Running with Claude Desktop (or another MCP client)

Add this server to your MCP config file (e.g. claude_desktop_config.json):

{
  "mcpServers": {
    "weather": {
      "command": "node",
      "args": [
        "/Users/<your-username>/Desktop/Coding/mcpproject/build/index.js"
      ]
    }
  }
}


Replace <your-username> with your system username (check by running whoami in your terminal).

After restarting Claude, it will discover the new weather server and its tools.

🧪 Development

Run in watch mode (recompile on save):

npx tsc --watch


Run directly with ts-node (without compiling):

npx ts-node src/index.ts
