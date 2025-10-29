# Tool Use Pattern: Personal Assistant

## Overview

This tutorial demonstrates the **Tool Use Pattern** in agentic AI, where an agent leverages external tools to perform tasks beyond simple text generation. In this example, we'll build a Personal Assistant that can search the web for current information.

## What You'll Build

A personal assistant agent that can:
- Search the web for current information
- Provide intelligent responses based on web search results

## Workflow Diagram

```
Start Node ──▶ Personal Assistant Agent ──▶ End Node
                         │
                         └── Tool: Web Search
```

## Prerequisites

Before starting this tutorial, ensure you have:
1. Access to OpenAI Agent Builder
2. Basic understanding of the OpenAI Agent Builder interface

---

## Step 1: Create the Start Node

The Start Node initializes the workflow and can accept user input.

1. In OpenAI Agent Builder, create a new workflow
2. Name your workflow: `Personal Assistant`
3. The **Start Node** is already present by default
4. Configure the Start Node:
   - **Input Type**: `Text`
   - **Description**: `User's request or query`
5. Optionally, add any state variables you might need (we'll keep it simple for now)

---

## Step 2: Create the Personal Assistant Agent

This is the main agent that will handle user requests using web search.

1. Click **Add Agent**
2. Name it: `Personal Assistant Agent`
3. Add the following System Instructions:

```
You are a helpful personal assistant with access to web search.

When the user makes a request:
- Use web search for current information, news, weather, or facts
- Provide concise, friendly, and helpful answers
```

---

## Step 3: Enable Web Search Tool

1. With the **Personal Assistant Agent** selected, look for the **Tools** section in the right panel.
2. Click **+**, and select **Web Search** in the available tools list
3. Configure search settings (optional)

---

## Step 4: Connect the Workflow Nodes

Now connect the nodes to create the workflow flow:

1. Connect **Start Node** to **Personal Assistant Agent**
   - Drag from the output port of Start Node to the input port of Personal Assistant Agent
2. Connect **Personal Assistant Agent** to **End Node**
   - Drag from the output port of Personal Assistant Agent to End Node

Your workflow should now look like:
```
Start Node ──▶ Personal Assistant Agent ──▶ End Node
```

---

## Key Concepts Explained

### Tool Use Pattern

The **Tool Use Pattern** enables agents to:
- **Extend capabilities** beyond text generation
- **Access external data** in real-time
- **Perform actions** in connected systems
- **Combine multiple tools** for complex tasks

### When to Use This Pattern

Use the Tool Use Pattern when your agent needs to:
- Access current information (web search, APIs)
- Interact with external systems (calendar, databases, etc.)
- Perform calculations or data processing
- Execute actions on behalf of the user

---

## Troubleshooting

### Agent Not Using Tools

**Issue**: Agent responds without using available tools

**Solutions**:
- Make tool usage more explicit in system instructions
- Provide examples of when to use each tool
- Test with clearer, more specific user queries
- Check that tools are properly enabled

---

## Summary

In this tutorial, you learned:
- ✅ How to create an agent with web search tool
- ✅ How to configure tool permissions and capabilities
- ✅ Best practices for the Tool Use Pattern
- ✅ How to troubleshoot common issues

The Tool Use Pattern is one of the most powerful agentic AI patterns, enabling your agents to interact with the real world and provide truly useful assistance.

---

## Additional Resources

- [OpenAI Agent Builder Documentation](https://platform.openai.com/docs/agents)
- [Agentic Design Patterns Overview](../readme.md)

---
