# Model Context Protocol

MCP enables AI models to connect with external data sources, tools, and environments, allowing for the seamless transfer of information and capabilities between AI systems and the broader digital world. 

This interoperability is crucial for the growth and adoption of truly useful AI applications.

MCP offers a consistent protocol for linking AI models to external capabilities. This standardization benefits the entire ecosystem:

- users enjoy simpler and more consistent experiences across AI applications
- AI application developers gain easy integration with a growing ecosystem of tools and data sources
- tool and data providers need only create a single implementation that works with multiple AI applications
- the broader ecosystem benefits from increased interoperability, innovation, and reduced fragmentation

# The Integration Problem
The **M×N Integration Problem** refers to the challenge of connecting M different AI applications to N different external tools or data sources without a standardized approach.

### Without MCP (M×N Problem)
Without a protocol like MCP, developers would need to create M×N custom integrations—one for each possible pairing of an AI application with an external capability.

<img width="882" alt="Screenshot 2025-06-25 at 07 22 33" src="https://github.com/user-attachments/assets/80236237-b502-46ae-997d-df3be9c48671" />

Each AI application would need to integrate with each tool/data source individually. This is a very complex and expensive process which introduces a lot of friction for developers, and high maintenance costs.

Once we have multiple models and multiple tools, the number of integrations becomes too large to manage, each with its own unique interface.

<img width="882" alt="Screenshot 2025-06-25 at 07 23 24" src="https://github.com/user-attachments/assets/6db028ff-d945-4eab-ae23-481f810c68c2" />

### With MCP (M+N Solution)
MCP transforms this into an M+N problem by providing a standard interface: each AI application implements the client side of MCP once, and each tool/data source implements the server side once. 

This dramatically reduces integration complexity and maintenance burden.

<img width="877" alt="Screenshot 2025-06-25 at 07 22 51" src="https://github.com/user-attachments/assets/d6acad67-6642-47d0-9662-b4d1bcea286e" />

Each AI application implements the client side of MCP once, and each tool/data source implements the server side once.

## Components

<img width="860" alt="Screenshot 2025-06-25 at 07 23 55" src="https://github.com/user-attachments/assets/e7aa2377-2e69-483b-b502-4615e18020fe" />

- **Host:** The user-facing AI application that end-users interact with directly. Examples include Anthropic’s Claude Desktop, AI-enhanced IDEs like Cursor, inference libraries like Hugging Face Python SDK, or custom applications built in libraries like LangChain or smolagents. Hosts initiate connections to MCP Servers and orchestrate the overall flow between user requests, LLM processing, and external tools.

- **Client:** A component within the host application that manages communication with a specific MCP Server. Each Client maintains a 1:1 connection with a single Server, handling the protocol-level details of MCP communication and acting as an intermediary between the Host’s logic and the external Server.

- **Server:** An external program or service that exposes capabilities (Tools, Resources, Prompts) via the MCP protocol.

Capabilities
Of course, your application’s value is the sum of the capabilities it offers. So the capabilities are the most important part of your application. MCP’s can connect with any software service, but there are some common capabilities that are used for many AI applications.

| Capability | Description | Example |
|------------|-------------|---------|
| Tools | Executable functions that the AI model can invoke to perform actions or retrieve computed data. Typically relating to the use case of the application. | A tool for a weather application might be a function that returns the weather in a specific location. |
| Resources | Read-only data sources that provide context without significant computation. | A researcher assistant might have a resource for scientific papers. |
| Prompts | Pre-defined templates or workflows that guide interactions between users, AI models, and the available capabilities. | A summarization prompt. |
| Sampling | Server-initiated requests for the Client/Host to perform LLM interactions, enabling recursive actions where the LLM can review generated content and make further decisions. | A writing application reviewing its own output and decides to refine it further. |


In the following diagram, we can see the collective capabilities applied to a use case for a code agent.

<img width="769" alt="Screenshot 2025-06-25 at 07 27 13" src="https://github.com/user-attachments/assets/ad8672d4-4a6e-4a16-b241-6aee2a710e17" />

This application might use their MCP entities in the following way:

| Entity | Name | Description |
|--------|------|-------------|
| Tool | Code Interpreter | A tool that can execute code that the LLM writes. |
| Resource | Documentation | A resource that contains the documentation of the application. |
| Prompt | Code Style | A prompt that guides the LLM to generate code. |
| Sampling | Code Review | A sampling that allows the LLM to review the code and make further decisions. |



