# L4: MCP Nodes
## Using MCP Nodes in Your Agent Workflows

**Duration:** 10 minutes  
**Level:** Intermediate  
**Prerequisites:** Completed L2 (Connectors) and L3 (MCP Servers)

---

## Goal

Learn how to add MCP Nodes to your agent workflows and connect them to MCP servers for real-time data access.

## What You'll Learn

- How to add MCP Nodes to your agent workflow
- How to configure MCP Nodes to connect to MCP servers
- How to use MCP Nodes for different types of data access
- How to test MCP Node functionality
- Best practices for MCP Node usage

---

## Setup

- A working agent from previous labs
- MCP server configured (from L3)
- Access to Agent Builder
- Basic understanding of workflow nodes

---

## Step-by-Step Instructions

### Step 1: Add MCP Node to Your Workflow

1. Open your agent in [Agent Builder](https://platform.openai.com/playground/agent-builder)
2. In your workflow, look for the "Nodes" or "Tools" section
3. Find "MCP Node" in the available nodes
4. Drag the MCP Node onto your workflow canvas
5. Position it where you want it in your workflow

### Step 2: Configure the MCP Node

1. Click on the MCP Node to open its settings
2. **Name:** Give it a descriptive name like "Context7 Data"
3. **MCP Server:** Select the MCP server you configured in L3
4. **Function:** Choose what you want to do:
   - Get market data
   - Search news
   - Get industry research
   - Custom function

### Step 3: Connect MCP Node to Your Agent

1. **Option A: Direct Connection**
   - Connect MCP Node directly to your Agent Node
   - Agent will use MCP data when needed

2. **Option B: Conditional Connection**
   - Add an If/Else node before the MCP Node
   - Set condition: "If user asks about market data or news"
   - Connect MCP Node to the "Yes" branch

### Step 4: Configure Agent to Use MCP Data

1. In your Agent Node settings, add instructions:
   ```
   When you need current market data or news, use the MCP Node to get real-time information.
   Always cite your sources when using MCP data.
   ```

2. **Tool Selection:** Make sure your agent knows when to use the MCP Node
   - Add examples in your agent's instructions
   - Show when to use MCP vs. other data sources

### Step 5: Test Your MCP Node

**Test 1: Basic Functionality**
- Question: "What's the latest AI industry news?"
- Expected: Agent uses MCP Node to get current news
- Check: Does the response include current data?

**Test 2: Conditional Usage**
- Question: "What's our company vacation policy?"
- Expected: Agent uses SharePoint connector (not MCP)
- Check: Does it use the right data source?

**Test 3: Combined Data**
- Question: "How do our benefits compare to industry standards?"
- Expected: Agent uses both SharePoint (company data) and MCP (industry data)
- Check: Does it combine both sources effectively?

### Step 6: Advanced Configuration

**Multiple MCP Nodes:**
1. Add another MCP Node for different data types
2. Configure each for specific purposes:
   - MCP Node 1: Market data
   - MCP Node 2: News feeds
   - MCP Node 3: Weather data

**Error Handling:**
1. Add a fallback path if MCP Node fails
2. Configure timeout settings
3. Set up retry logic

---

## Expected Results

- Agent automatically uses MCP Node when appropriate
- Real-time data is integrated into responses
- Agent cites MCP data sources properly
- Workflow handles MCP failures gracefully
- Response time remains under 5 seconds

---

## Common MCP Node Patterns

### Pattern 1: Always Use MCP
```
Start → Agent → MCP Node → Response
```
**Use when:** You always want real-time data

### Pattern 2: Conditional MCP
```
Start → If/Else → MCP Node (if needed) → Agent → Response
```
**Use when:** MCP data is only needed sometimes

### Pattern 3: Multiple Data Sources
```
Start → Agent → [SharePoint + MCP Node] → Response
```
**Use when:** You need both company data and real-time data

---

## Troubleshooting

| Problem | Why it happens | How to fix |
|---|---|---|
| MCP Node not working | Server not connected | Check MCP server configuration |
| No data returned | Wrong function selected | Verify function settings in MCP Node |
| Agent ignores MCP Node | Instructions unclear | Add specific examples to agent instructions |
| Slow responses | MCP server overloaded | Add timeout settings or retry logic |

---

## Best Practices

### Configuration
- Give MCP Nodes descriptive names
- Use specific functions rather than generic ones
- Set appropriate timeout values
- Test each MCP Node individually

### Workflow Design
- Place MCP Nodes where they make sense in your workflow
- Use conditional logic to avoid unnecessary MCP calls
- Always have fallback options
- Monitor MCP usage and costs

### Error Handling
- Set up proper error handling for MCP failures
- Provide meaningful error messages to users
- Log MCP usage for debugging
- Have backup data sources when possible

---

## Testing Your Setup

### Basic Test
1. Ask a question that requires MCP data
2. Verify the MCP Node is triggered
3. Check that current data is returned
4. Confirm sources are cited

### Integration Test
1. Ask questions that need both company data and MCP data
2. Verify both sources are used appropriately
3. Check that the combined response makes sense
4. Test error scenarios

### Performance Test
1. Time how long MCP responses take
2. Test with different types of questions
3. Monitor for any timeout issues
4. Check error rates

---

## Next Steps

Once you've completed this lab:

1. **Try different MCP functions:** Experiment with various data types
2. **Add more MCP Nodes:** Connect to additional MCP servers
3. **Optimize workflows:** Fine-tune when and how MCP Nodes are used
4. **Monitor performance:** Track MCP usage and response times

---

## Key Takeaways

- MCP Nodes connect your workflows to external data sources
- Use conditional logic to control when MCP Nodes are triggered
- Always test MCP Node functionality before going live
- Monitor costs and performance when using MCP services
- Combine MCP data with company data for comprehensive answers

---

*Congratulations! You've completed all four labs. You now know how to use File Search, Connectors, MCP Servers, and MCP Nodes to build powerful, data-driven agents.*
