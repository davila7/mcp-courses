# Architectural Components of MCP
The MCP architecture consists of three primary components, each with well-defined roles and responsibilities: Host, Client, and Server. We touched on these in the previous section, but let’s dive deeper into each component and their responsibilities.

## Host
The Host is the user-facing AI application that end-users interact with directly.

Examples include:

- AI Chat apps like OpenAI ChatGPT or Anthropic’s Claude Desktop
- AI-enhanced IDEs like Cursor, or integrations to tools like Continue.dev
- Custom AI agents and applications built in libraries like LangChain or smolagents

The Host’s responsibilities include:

- Managing user interactions and permissions
- Initiating connections to MCP Servers via MCP Clients
- Orchestrating the overall flow between user requests, LLM processing, and external tools
- Rendering results back to users in a coherent format

In most cases, users will select their host application based on their needs and preferences. For example, a developer may choose Cursor for its powerful code editing capabilities, while domain experts may use custom applications built in smolagents.

## Client
The Client is a component within the Host application that manages communication with a specific MCP Server. Key characteristics include:

- Each Client maintains a 1:1 connection with a single Server
- Handles the protocol-level details of MCP communication
- Acts as the intermediary between the Host’s logic and the external Server

## Server
The Server is an external program or service that exposes capabilities to AI models via the MCP protocol. Servers:

- Provide access to specific external tools, data sources, or services
- Act as lightweight wrappers around existing functionality
- Can run locally (on the same machine as the Host) or remotely (over a network)
- Expose their capabilities in a standardized format that Clients can discover and use
