# Workshop 2: Connectors
## Building an HR Benefits Assistant

**Duration:** 30 minutes  
**Level:** Intermediate  
**Prerequisites:** Access to Microsoft 365 and OpenAI platform

---

## Goal

Connect your agent to a SharePoint library so it can search employee policies and answer benefits questions.

## What You'll Learn

- How to set up SharePoint connector
- How to configure permissions and access controls
- How to enable semantic search through connected data
- How to test connector functionality
- How to troubleshoot connection issues

---

## Setup

- Access to Microsoft 365
- Permission to create agents in your platform
- A SharePoint site with employee policy documents
- Admin access to configure connectors

---

## Step-by-Step Instructions

### Step 1: Create a New Agent

1. Log into [OpenAI Agent Builder](https://platform.openai.com/playground/agent-builder)
2. Click "Create New Agent"
3. Name it "HR Benefits Assistant"
4. Add a system prompt: "You are an HR assistant. Help employees find information about benefits, policies, and procedures."

### Step 2: Add SharePoint Connector

1. In your agent, go to the "Connectors" or "Knowledge" section
2. Click "Add Connector" or "Add Data Source"
3. Select "SharePoint" from the list of available connectors
4. Click "Connect Microsoft 365"
5. Sign in with your Microsoft account
6. Grant permissions when prompted
7. Select your SharePoint site

### Step 3: Choose Which Library to Connect

1. You might see options like:
   - "Policies"
   - "Employee Handbook"
   - "Shared Documents"
   - "HR Resources"
2. Select "Employee Policies" or the library containing your HR documents
3. This is where the agent will search for information

### Step 4: Configure Search Settings

1. Look for "Enable semantic search" or "Enable smart search"
2. Check this box to turn on intelligent searching
3. Wait for the system to index your documents (this may take a few minutes)
4. You'll see a progress indicator during indexing

### Step 5: Set Permissions

1. Decide who can use this connector:
   - All employees: Can see general policies
   - HR staff only: Can see all documents
   - Specific groups: Custom access levels
2. For HR benefits, usually all employees can see general policies
3. Save your permission settings

### Step 6: Test the Connection

Ask your agent these questions:

**Basic Policy Questions:**
- "What's our vacation policy?"
- "How many sick days do I get?"
- "What are our health insurance benefits?"

**Specific Scenarios:**
- "Can I work from home on Fridays?"
- "What's the process for requesting time off?"
- "How do I change my health insurance?"

**Complex Questions:**
- "What happens to my benefits if I go on maternity leave?"
- "Can I carry over unused vacation days?"

### Step 7: Verify Results

Check that your agent:
- Finds the correct documents
- Cites which document the answer came from
- Provides complete and accurate information
- Responds within 3 seconds

---

## Expected Results

- Agent finds correct documents from SharePoint
- Agent cites sources in responses
- Search completes in under 3 seconds
- Answers are accurate and helpful
- Agent can handle different ways of asking the same question

---

## Advanced Configuration

### Setting Up Multiple Libraries

If you have different types of HR documents in separate libraries:

1. Add multiple SharePoint connectors
2. Connect to different libraries (e.g., "Policies", "Forms", "Procedures")
3. Configure the agent to search all connected libraries
4. Set different permissions for each library

### Custom Search Scopes

1. **Department-specific access:** Only show relevant policies to each department
2. **Role-based filtering:** Different access levels for managers vs. employees
3. **Document type filtering:** Separate access for public vs. confidential documents

### Integration with Other Connectors

1. **Teams integration:** Search Teams messages for policy discussions
2. **OneDrive integration:** Access personal HR documents
3. **Outlook integration:** Search HR emails for policy updates

---

## Troubleshooting

| Problem | Why it happens | How to fix |
|---|---|---|
| Can't connect to SharePoint | Wrong permissions or site access | Check Microsoft 365 permissions |
| Agent ignores instructions | Instructions too vague | Add specific examples and context |
| Wrong documents retrieved | Document metadata unclear | Improve document titles and descriptions |
| Slow search | Too many documents or large files | Reduce document scope or optimize files |
| Permission errors | Access controls too restrictive | Review and adjust permission settings |

---

## Security Best Practices

### Access Control
- Use least-privilege access (only give access that's needed)
- Regularly review who has access to what
- Set up different access levels for different user groups

### Data Protection
- Ensure sensitive documents are properly protected
- Use document-level permissions when possible
- Monitor access logs regularly

### Compliance
- Follow your organization's data handling policies
- Ensure connector usage complies with regulations
- Document your connector configurations

---

## Testing Your Setup

### Basic Functionality Test
1. Ask simple policy questions
2. Verify correct documents are found
3. Check that answers are complete and accurate

### Security Test
1. Try accessing documents you shouldn't see
2. Verify that access controls work properly
3. Test with different user accounts if possible

### Performance Test
1. Time how long searches take
2. Test with different types of questions
3. Monitor for any error messages

---

## Next Steps

Once you've completed this workshop:

1. **Try other connectors:** Experiment with Google Drive, Teams, or OneDrive
2. **Add more libraries:** Connect to additional SharePoint libraries
3. **Customize permissions:** Set up role-based access controls
4. **Monitor usage:** Track how the connector is being used

---

## Key Takeaways

- Connectors bridge your agent with external data sources
- SharePoint integration enables search through company documents
- Proper permissions are essential for security
- Testing with real questions improves results
- Multiple connectors can work together

---

*Ready for the next workshop? Try [Workshop 3: MCP Servers](../03_mcp_workshop.md) to learn about connecting to custom data sources.*
