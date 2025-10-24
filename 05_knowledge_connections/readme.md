# Session 5: Connecting Knowledge Safely

## A Guide to Making Smart Decisions About Information in AI Agents

**Duration:** 2 hours  
**Level:** Intermediate  
**Background Needed:** Basic understanding of AI agents (from Session 4)

---

## What You Will Learn

By the end of this session, you will understand:
- How to decide what information to keep inside an agent versus link to external sources
- How file search and vector stores work
- How to use built-in connectors (Google Drive, SharePoint, Teams, etc.)
- How to set up and use MCP servers for custom connections
- How to protect sensitive data while sharing information
- How to track who accessed what and when

---

## Part 1: Introduction and Theory (15 minutes)

### Understanding Knowledge Connectivity

Think of an AI agent like a smart assistant in an office. This assistant needs access to information to do its job well. But here's the challenge: should you give the assistant copies of everything they might need, or should you let them ask for information when they need it?

**Knowledge connectivity** is about deciding how your agent gets access to information. It involves three main ideas:

**1. What to Store vs. What to Link**

Some information should live inside the agent (like instructions and settings). Other information should stay in its original place and the agent should access it when needed (like company documents in Google Drive).

**2. Finding the Right Information Quickly**

When an agent needs information, it has to search through available documents. This is like a librarian finding the right book from thousands on the shelf. We need smart search tools so the agent finds the correct information fast.

**3. Keeping Information Safe**

When multiple people and agents share information, we need rules about who can see what. This is called "least-privilege access" — everyone gets only the access they absolutely need, nothing more.

### Key Terms

- **File Search:** A tool that lets agents search through uploaded documents using smart search technology
- **Connector:** A bridge that lets your agent talk to other systems (like Google Drive, SharePoint, or Teams)
- **MCP Servers:** Special tools that help agents connect to different services. It's the defactor Standard to connect Agents with Context like we have standard blueprint for building cars.
- **Vector Store:** A smart filing system that helps agents find documents by meaning, not just keywords
- **Redaction:** Hiding or removing sensitive information before sharing
- **Auditability:** The ability to see a clear record of what happened and who did it

### Understanding File Search and Vector Stores

**What is File Search?**

Instead of asking an agent to answer from memory alone, File Search means:
1. Agent receives a question
2. Agent searches through uploaded documents using smart search
3. Agent finds the most relevant information
4. Agent uses that information to create a better answer

Example: "What's our return policy?"
- Without File Search: Agent guesses based on general knowledge (might be wrong)
- With File Search: Agent searches your uploaded documents, finds the return policy document, reads it, then answers accurately

**What are Vector Stores?**

Vector Stores are smart filing systems that help agents find documents by meaning, not just keywords. They understand what your documents are about and can find relevant information even if you ask using different words.

**Why File Search matters:**
- More accurate answers (based on real documents, not guesses)
- Current information (if documents are updated, answers are automatically current)
- Traceable answers (you can see which document the agent used)
- Reduced hallucination (agent makes up less false information)

---

## Part 2: Understanding OpenAI's Knowledge Tools (15 minutes)

### The Connectors

The Connectors are how you manage all the places your agents can get information from. Think of it as a phone book for your agent's data sources.

**How it works:**
- You set up connections to different services (Google Drive, SharePoint, etc.)
- You decide who can use each connection
- You can turn connections on or off as needed

### Built-in Connectors

OpenAI provides ready-made connections to popular services. You don't have to build them from scratch.

**Microsoft 365 Suite:**
- **SharePoint Connector:** Access documents in SharePoint libraries
- **Teams Connector:** Read messages and files from Teams
- **OneDrive Connector:** Access personal cloud storage
- **Outlook Connector:** Search emails and calendar

**Google Workspace Suite:**
- **Google Drive Connector:** Search Docs, Sheets, PDFs in Drive
- **Gmail Connector:** Search email messages
- **Google Calendar Connector:** Access calendar events

**Others:**
- **Slack Connector:** Search Slack messages and files
- **Notion Connector:** Access Notion databases and pages
- **Jira Connector:** Search issues and documentation

### File Search and Vector Stores

**File Search** lets your agent look through documents you've uploaded. It's like having a smart search engine for your files.

**Vector Stores** are special databases that understand the meaning of your documents. Instead of just looking for exact words, they can find documents that are about the same topic, even if they use different words.

**How it works:**
1. You upload documents to a vector store
2. The system reads each document and creates a "fingerprint" of what it's about
3. When someone asks a question, the system finds documents with similar fingerprints
4. The agent uses those documents to answer the question

### MCP Servers (Model Context Protocol)

MCP servers are like special bridges that connect your agent to services that aren't built into OpenAI's platform. They let you connect to custom databases, APIs, or specialized services.

**Think of it like this:**
- Built-in connectors: Direct connections to Google Drive, SharePoint (pre-built)
- MCP servers: Custom connections to specialized services
- MCP servers act as translators between your agent and specialized data sources

---

## Part 3: Deciding What to Connect (20 minutes)

### Decision Framework

When deciding what to connect to your agent, ask these three questions:

**1. How big is the information?**
- Small (a few pages): Consider storing inside the agent
- Large (hundreds of documents): Link to external source

**2. How often does it change?**
- Rarely changes: Store inside the agent
- Changes frequently: Link to external source

**3. How will the agent use it?**
- Same information every time: Store inside
- Needs to search and find different parts: Link to external source

### Solved Problem 1: Marketing Company Example

**Scenario:** You work at a marketing company. You're building an AI agent to help customers find information about your services. You have three types of information:

1. Brand guidelines (40 PDF pages)
2. Current product prices (changes weekly)
3. Customer support policies (200 documents)

The agent needs all three. What should you store inside the agent and what should you link to?

**Solution - Step by Step:**

**Step 1: Consider the size**
- Brand guidelines: Large but stable (40 pages)
- Product prices: Small but changes often
- Support policies: Very large (200 documents)

**Step 2: Consider how often it changes**
- Brand guidelines: Almost never changes
- Product prices: Changes every week
- Support policies: Changes sometimes

**Step 3: Consider how the agent will use it**
- Brand guidelines: Needs to reference the same information every time
- Product prices: Must show current information
- Support policies: Needs to search through many documents

**Step 4: Make your decision**

| Information | Store Inside | Link To | Reason |
|---|---|---|---|
| Brand guidelines | ✓ | | Stable, frequently needed, creates consistent brand voice |
| Product prices | | ✓ | Changes weekly; must always be current |
| Support policies | | ✓ | Too large; agent can search and retrieve what's needed |

**Best Practice:** Store only the information that rarely changes and is essential for every conversation. Link to everything else.

---

## Hands-On Live Class Labs (70 Minutes)

Now that you understand the concepts, it's time to build! We have three focused workshops that will teach you how to use each type of knowledge connection:

### 🔍 [L1: File Search with Vector Stores](01_file_search_workshop.md)
**Duration:** 20 minutes | **Level:** Intermediate

Learn how to create vector stores and connect them to your agents for intelligent document search.

**What you'll build:** A customer support agent that can search through FAQ documents and answer questions while protecting customer privacy.

**Key skills:**
- Creating vector stores in the OpenAI dashboard
- Uploading and indexing documents
- Connecting File Search tool to vector stores
- Implementing PII protection
- Testing semantic search capabilities

---

### 🔗 [L2: Connectors](02_connectors_workshop.md)
**Duration:** 20 minutes | **Level:** Intermediate

Learn how to connect your agents to external data sources like SharePoint, Google Drive, and Teams.

**What you'll build:** An HR Benefits Assistant that can search employee policies and answer benefits questions.

**Key skills:**
- Setting up SharePoint connector
- Configuring permissions and access controls
- Enabling semantic search through connected data
- Testing connector functionality
- Troubleshooting connection issues

---

### 🌐 [L3: MCP Servers](03_mcp_workshop.md)
**Duration:** 20 minutes | **Level:** Advanced

Learn how to connect your agents to custom data sources using MCP (Model Context Protocol).

**What you'll build:** An agent that combines company data with real-time market data from Context7.

**Key skills:**
- Understanding MCP and why it matters
- Setting up MCP servers in Agent Builder
- Configuring Context7 for real-time data access
- Managing costs and query limits

---

### ⚙️ [L4: MCP Nodes](04_mcp_nodes_workshop.md)
**Duration:** 10 minutes | **Level:** Intermediate

Learn how to add MCP Nodes to your agent workflows and connect them to MCP servers.

**What you'll build:** A workflow that uses MCP Nodes to access real-time data when needed.

**Key skills:**
- Adding MCP Nodes to workflows
- Configuring MCP Nodes to connect to MCP servers
- Using MCP Nodes for different types of data access
- Testing MCP Node functionality
- Best practices for MCP Node usage

---

## Part 7: Security and Data Handling (20 minutes)

### Least-Privilege Access

**What it means:** Everyone gets only the access they absolutely need, nothing more.

**Example:**
- HR staff: Can see all employee policies
- Regular employees: Can see general policies only
- External users: Cannot access anything

### Redaction Strategies

**Option A: Redact before indexing (safest)**
- Remove personal information from documents before uploading
- Agent searches clean documents
- No sensitive data to accidentally expose

**Option B: Redact during retrieval**
- Store full documents
- When agent retrieves a document, automatically hide sensitive data
- Agent sees clean version

**Option C: Use access controls**
- Different users see different documents
- Customer service reps see all documents
- Customers see only public FAQs

### Setting Up Audit Trails

**What to log:**
- Who asked what question
- Which documents were searched
- What information was retrieved
- When it happened
- Who had access

**Example audit log:**
```
Question: "What's the return policy?"
User: customer@email.com
Documents searched: returns-faq.pdf, policy-handbook.pdf
Data retrieved: Section 3.2 on 30-day returns
Answer generated: "You have 30 days to return items"
Timestamp: Oct 24, 2025, 2:45 PM
```

### Testing Security

**Test 1: Try unauthorized access**
- Ask questions you shouldn't be able to answer
- Verify that access is properly restricted

**Test 2: Check PII masking**
- Upload documents with fake personal information
- Ask questions that would retrieve those documents
- Verify that personal information is hidden

**Test 3: Review audit logs**
- Check that all queries are being logged
- Verify that logs contain the right information

---

## Part 8: Troubleshooting and Optimization (15 minutes)

### Common Problems and Solutions

| Problem | Why it happens | How to fix |
|---|---|---|
| Agent ignores instructions | Instructions too vague | Add specific examples |
| Wrong documents retrieved | Document metadata unclear | Improve document titles and descriptions |
| Slow search | Too many documents | Reduce document scope or upgrade plan |
| RAG returns too much info | Chunk size too large | Adjust chunk size or add length limits |
| Approval always needed | No clear decision rules | Add if/else logic for common cases |

### Performance Monitoring

**Check these regularly:**

**Search speed:**
- Most searches should complete in under 3 seconds
- If slower, consider reducing document count

**Accuracy:**
- Are the right documents being found?
- Are answers helpful and relevant?

**Connector health:**
- Are all connectors working?
- Are there any error messages?

**Cost monitoring:**
- How much are you spending on API calls?
- Are there any unexpected charges?

### Optimization Tips

**For better search results:**
1. Use clear, descriptive document titles
2. Add summaries to documents
3. Tag documents with relevant keywords
4. Remove old or irrelevant documents

**For faster performance:**
1. Use smaller document files
2. Split large PDFs into sections
3. Archive old documents
4. Use fewer connectors if possible

**For better security:**
1. Review access permissions regularly
2. Check audit logs weekly
3. Test PII masking monthly
4. Update security settings as needed

---

## Part 9: Real-World Examples (10 minutes)

### Success Stories

**Klarna: Customer Support Agent**
- Built an agent that handles 2/3 of customer service tickets
- Uses RAG to search through support documents
- Saves time and improves customer satisfaction

**Ramp: Buyer Agent**
- Built a procurement agent in just a few hours
- Connects to multiple data sources
- Automates purchase decisions and approvals

**HubSpot: Sales Assistant**
- Created an agent that helps sales teams
- Connects to CRM data and product information
- Provides personalized recommendations

### Key Lessons

1. **Start simple:** Begin with one data source, then add more
2. **Test thoroughly:** Always test with real questions before going live
3. **Monitor performance:** Keep track of how well your agent is working
4. **Iterate quickly:** Make small improvements based on user feedback

---

## Practice Exercises

**Beginner Level:**
- Complete [L1: File Search](01_file_search_workshop.md) with your own documents
- Add Google Drive connector to your HR agent (see [L2: Connectors](02_connectors_workshop.md))
- Upload some policy documents to Drive and test that your agent can find them

**Intermediate Level:**
- Complete [L2: Connectors](02_connectors_workshop.md) with multiple data sources
- Add [L4: MCP Nodes](04_mcp_nodes_workshop.md) to your workflow
- Combine SharePoint + Google Drive with priority routing
- Test with questions that might be in either location

**Advanced Level:**
- Complete all four labs: [L1: File Search](01_file_search_workshop.md), [L2: Connectors](02_connectors_workshop.md), [L3: MCP Servers](03_mcp_workshop.md), and [L4: MCP Nodes](04_mcp_nodes_workshop.md)
- Build an agent with 3 data sources:
  - SharePoint (company policies)
  - Google Drive (project documents)
  - Context7 (market data via MCP Nodes)
- Create a question that uses all three sources

---

### Preparation for Session 6

**Think about these scenarios:**
1. When would you need multiple agents working together?
2. What processes in your business need human approval?
3. How could you break complex workflows into smaller steps?

**Make a list:**
- 3 business processes that could use multiple agents
- 2 decisions that always need human approval
- 1 complex workflow you'd like to automate

### Resources

**Official Documentation:**
- [OpenAI Agent Builder Guide](https://platform.openai.com/docs/guides/agent-builder)
- [Connector Registry Documentation](https://platform.openai.com/docs/guides/connector-registry)
- [MCP Server Guide](https://platform.openai.com/docs/guides/mcp-servers)

**Community Examples:**
- Browse the OpenAI community forum for agent examples
- Check out the Agent Builder templates
- Look for case studies in your industry

---

## Key Takeaways

1. **Choose the right connection method:** Store small, stable data inside; link to large, changing data
2. **Use RAG for better answers:** Let your agent search documents instead of guessing
3. **Protect sensitive information:** Always use redaction and access controls
4. **Test everything:** Make sure your agent works before going live
5. **Monitor performance:** Keep track of speed, accuracy, and costs
6. **Start simple:** Begin with one data source and add more over time

Remember: The goal is to make your agent helpful, accurate, and safe. Take your time to set things up correctly, and don't be afraid to ask for help when you need it!

---

## Glossary

**Agent:** A system that works toward goals through multiple steps, using tools and decision-making

**Connector:** A bridge that lets your agent talk to other systems (like Google Drive, SharePoint, or Teams)

**File Search:** The ability to look through documents and find specific information

**Guardrails:** Automatic safety checks that protect against data leaks and misuse

**MCP (Model Context Protocol):** A standard way to connect agents to external tools and services

**PII (Personally Identifiable Information):** Private data like social security numbers, addresses, or phone numbers

**File Search:** A tool that lets agents search through uploaded documents using smart search technology

**Vector Store:** A smart filing system that helps agents find documents by meaning, not just keywords

**Workflow:** The complete sequence of steps (nodes) your agent follows

---

*Use this guide during the session, for self-study, or as a reference when building your own agents.*
