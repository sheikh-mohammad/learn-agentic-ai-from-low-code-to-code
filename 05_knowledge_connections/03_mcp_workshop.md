# Workshop 3: MCP Servers
## Connecting to Context7 for Real-Time Data

**Duration:** 20 minutes  
**Level:** Advanced  
**Prerequisites:** Completed Workshops 1 and 2, access to OpenAI platform

---

## Goal

Connect your agent to Context7 MCP server to access real-time market data, news, and research, then combine it with your company data for comprehensive answers.

## What You'll Learn

- What MCP (Model Context Protocol) is and why it matters
- How to set up MCP servers in Agent Builder
- How to configure Context7 for real-time data access
- How to combine multiple data sources in one agent
- How to manage costs and query limits

---

## What is Context7?

Context7 is an online service that provides real-time market data, news, and research. It uses MCP (Model Context Protocol) to connect with AI agents, giving them access to current information that isn't in your regular documents.

**Think of Context7 as:**
- A news service that updates constantly
- A market research database
- A source of current trends and information
- A way to get "live" data into your agent

**Why MCP matters:**
- It's the de facto standard for connecting agents with external context
- Like having a standard blueprint for building cars - everyone uses the same system
- Makes it easy to connect to any service that supports MCP
- Enables agents to access specialized data sources

---

## Setup

- Access to OpenAI Agent Builder
- Context7 demo API key (provided in class)
- Basic understanding of how agents work
- A working agent from previous workshops

---

## Step-by-Step Instructions

### Step 1: Access MCP Settings

1. In Agent Builder, go to Agent -> "Tools" -> "MCP" section
3. Click "Add MCP Server" or "Configure MCP"

### Step 2: Configure Context7 Connection

1. **Name:** "Context7"
2. **Server URL:** `https://context7-demo.mcp-server.com` (demo endpoint)
3. **Authentication:** Use the demo API key provided in class
4. **Description:** "Real-time market data and news"
5. Click "Save" and wait for verification

### Step 3: Enable Context7 Features

1. Select which Context7 services to use:
   - ✅ Market data: Current stock prices, market trends
   - ✅ News feeds: Latest industry news and updates
   - ✅ Industry research: Market analysis and reports
2. Set query limits: "Use Context7 no more than 50 times per day"
3. This prevents accidental high costs

### Step 4: Test the Connection

Ask your agent: "What's the latest AI industry news?"

**What to look for:**
- Did it get data from Context7?
- Is the data current (from today)?
- How fast was the response?
- Does the answer cite Context7 as a source?

### Step 5: Test Different Types of Questions

**Test 1: Current News**
- Question: "What's happening in AI today?"
- Expected: Recent news from Context7
- Check: Is the information from today or yesterday?

**Test 2: Market Data**
- Question: "What's the current market size for AI companies?"
- Expected: Live market data from Context7
- Check: Does it include recent numbers and trends?

**Test 3: Industry Trends**
- Question: "What are the latest trends in customer service AI?"
- Expected: Current research and trends
- Check: Is the information up-to-date and relevant?

### Step 6: Combine Multiple Sources

**The powerful part:** Your agent can now use both your company documents AND live data from Context7.

**Example question:** "How do our employee benefits compare to industry standards?"

**What happens:**
1. Agent searches SharePoint for your company benefits
2. Agent asks Context7 for current industry benefit data
3. Agent combines both sources to give a comprehensive answer

**Test this:**
1. Ask the combined question above
2. Check if the answer mentions:
   - Your company's specific benefits
   - Current industry standards
   - A comparison between them

**Expected result:** "Our company offers 15 vacation days, but the industry standard is 20 days. We might want to consider increasing our vacation policy to stay competitive."

---

## Advanced Configuration

### Setting Up Multiple MCP Servers

You can connect multiple MCP servers to one agent:

1. **Context7:** For market data and news
2. **Weather API:** For location-based information
3. **Custom Database:** For specialized company data
4. **Social Media API:** For brand monitoring

### Cost Management

1. **Set daily limits:** Prevent runaway costs
2. **Monitor usage:** Check how many queries you're making
3. **Use caching:** Avoid repeated queries for the same data
4. **Optimize queries:** Ask specific questions to get better results

### Error Handling

1. **Fallback responses:** What to do if Context7 is unavailable
2. **Retry logic:** How many times to try before giving up
3. **User notifications:** Let users know when external data isn't available

---

## Real-World Use Cases

### HR Benefits Comparison
- **Company data:** Your benefits from SharePoint
- **Context7 data:** Industry standards and trends
- **Result:** Comprehensive benefits analysis

### Market Research
- **Company data:** Your product information
- **Context7 data:** Market trends and competitor analysis
- **Result:** Strategic market insights

### News Monitoring
- **Company data:** Your brand mentions
- **Context7 data:** Industry news and developments
- **Result:** Complete brand and industry monitoring

---

## Troubleshooting

| Problem | Why it happens | How to fix |
|---|---|---|
| Can't connect to Context7 | Wrong URL or API key | Check the server URL and authentication |
| No data returned | Query limits exceeded | Check your daily usage limits |
| Slow responses | Network issues or server load | Try again later or check connection |
| Wrong data returned | Query not specific enough | Make your questions more specific |

---

## Security Considerations

### API Key Management
- Keep your API keys secure
- Don't share them in public repositories
- Rotate keys regularly
- Use different keys for different environments

### Data Privacy
- Be aware of what data you're sending to external services
- Check Context7's privacy policy
- Consider data residency requirements
- Monitor what information is being shared

### Access Controls
- Limit who can use MCP servers
- Set up proper permissions
- Monitor usage and access
- Log all external data requests

---

## Testing Your Setup

### Basic Functionality Test
1. Ask simple questions that require Context7 data
2. Verify that data is current and relevant
3. Check that responses are complete and accurate

### Integration Test
1. Ask questions that combine company data and Context7 data
2. Verify that both sources are used properly
3. Check that the combined response makes sense

### Performance Test
1. Time how long responses take
2. Test with different types of questions
3. Monitor for any error messages or timeouts

---

## Best Practices

### Query Optimization
- Ask specific questions to get better results
- Use filters and parameters when available
- Avoid asking the same question multiple times
- Cache frequently requested data

### Cost Management
- Set reasonable daily limits
- Monitor your usage regularly
- Use free tiers when possible
- Optimize queries to reduce costs

### Error Handling
- Always have fallback responses
- Log errors for debugging
- Notify users when external services are unavailable
- Implement retry logic for temporary failures

---

## Next Steps

Once you've completed this workshop:

1. **Try other MCP servers:** Explore different data sources
2. **Build custom integrations:** Create your own MCP servers
3. **Optimize performance:** Fine-tune your queries and responses
4. **Monitor usage:** Track costs and performance

---

## Key Takeaways

- MCP is the standard way to connect agents to external data
- Context7 provides real-time market data and news
- Multiple data sources can be combined for comprehensive answers
- Cost management is important when using external services
- Security and privacy must be considered for all external connections

---

*Congratulations! You've completed all three workshops. You now know how to use File Search, Connectors, and MCP servers to build powerful, data-driven agents.*
