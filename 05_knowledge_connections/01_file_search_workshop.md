# Workshop 1: File Search with Vector Stores
## Building a Customer Support Agent

**Duration:** 30 minutes  
**Level:** Intermediate  
**Prerequisites:** Access to OpenAI platform and Agent Builder

---

## Goal

Create a customer support agent that can search through FAQ documents and answer questions while protecting customer privacy.

## What You'll Learn

- How to create vector stores in the OpenAI dashboard
- How to upload and index documents
- How to connect File Search tool to vector stores
- How to implement PII protection
- How to test semantic search capabilities

---

## Setup

- Create a vector store in the OpenAI dashboard
- Upload FAQ documents to the vector store
- Connect File Search tool to the vector store
- Add PII masking guardrail

---

## Step-by-Step Instructions

### Step 1: Create a Vector Store in the Dashboard

1. Go to [platform.openai.com](https://platform.openai.com) and sign in
2. Open the "Data" section and choose "Vector stores"
3. Click "Create vector store"
4. Give it a friendly name like "customer-support-faqs"
5. Click "Create"
6. **Important:** Copy the Vector store ID (it starts with vs_...) - you'll need this later

### Step 2: Upload Documents

1. In your vector store, click "Upload files"
2. Upload your FAQ documents (PDFs work best)
3. Common documents to include:
   - Return policy
   - Shipping information
   - Product manuals
   - Troubleshooting guides
4. Wait for indexing to complete (you'll see a progress bar)
5. The system will show "Indexing complete" when ready

### Step 3: Create Your Agent

1. Go to [Agent Builder](https://platform.openai.com/playground/agent-builder)
2. Click "Create New Agent"
3. Name it "Customer Support Assistant"
4. Add a basic system prompt like: "You are a helpful customer support agent. Answer questions using the provided documents."

### Step 4: Connect File Search Tool

1. In your agent workflow, add a "File Search" node
2. In the File Search node settings, paste your Vector store ID
3. The agent will now be able to search through your uploaded documents
4. Save your agent

### Step 5: Add PII Protection

1. Add a "Guardrails" node before the File Search
2. Enable "PII Masking" to hide personal information
3. This will automatically hide names, phone numbers, and email addresses
4. Configure the guardrail to block or mask sensitive data

### Step 6: Test Your Agent

Try these different ways of asking the same question:

**Test 1 - Exact match:**
- Question: "What is the return policy?"
- Expected: Find document about returns
- Check: Did it find the right document?

**Test 2 - Different words:**
- Question: "Can I send things back?"
- Expected: Same return policy document (even though you didn't say "return")
- Check: Did it understand the meaning?

**Test 3 - Combined concepts:**
- Question: "How long do I have to exchange a broken item?"
- Expected: Find both return policy AND warranty information
- Check: Did it find both documents?

### Step 7: Test Security

1. Upload a test document with fake personal information
2. Ask a question that would retrieve that document
3. Verify that personal information is hidden in the response
4. Check that the agent cites sources properly

---

## Expected Results

- Agent finds relevant documents quickly using vector search
- Agent combines information from multiple documents when needed
- Personal information is automatically hidden by PII masking
- Agent cites sources in responses
- Search completes in under 3 seconds

---

## Troubleshooting

| Problem | Why it happens | How to fix |
|---|---|---|
| Agent can't find documents | Vector store not connected properly | Check the Vector store ID is correct |
| Search is slow | Too many documents or large files | Reduce document count or file sizes |
| Wrong documents found | Document titles unclear | Improve document metadata and descriptions |
| PII not masked | Guardrail not configured | Check guardrail settings and test with sample data |

---

## Next Steps

Once you've completed this workshop:

1. **Try different document types:** Test with Word docs, text files, and web pages
2. **Experiment with chunk sizes:** See how different chunk sizes affect search results
3. **Add more guardrails:** Try content filtering and custom safety rules
4. **Test with real data:** Use actual company documents (with permission)

---

## Key Takeaways

- Vector stores make document search fast and accurate
- File Search tool connects agents to your knowledge base
- PII protection is essential for customer data
- Testing with different question phrasings improves results
- Always verify security settings before going live

---

*Ready for the next workshop? Try [Workshop 2: Connectors](../02_connectors_workshop.md) to learn about connecting to external data sources.*
