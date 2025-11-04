# Session 7: Deploy with ChatKit

## From Agent Builder to Production Chat Interface

**Duration:** 2 hours
**Level:** Intermediate
**Prerequisites:** Sessions 4-6 (Agent Builder, Knowledge Connections, Visual Patterns)

---

## 📋 Prerequisites Checklist

Before we start, make sure you have:

- [ ] **Node.js** installed (version 20 or higher)
  - Check: Open terminal and type `node --version`
  - If not installed: Download from [nodejs.org](https://nodejs.org)

- [ ] **npm** installed (comes with Node.js)
  - Check: Type `npm --version`

- [ ] **Git** installed
  - Check: Type `git --version`
  - If not installed: Download from [git-scm.com](https://git-scm.com)

- [ ] **Code editor** installed (VS Code recommended)
  - Download from [code.visualstudio.com](https://code.visualstudio.com)

- [ ] **OpenAI account** with API access
  - Sign up at [platform.openai.com](https://platform.openai.com)

- [ ] **Agent created** in Agent Builder
  - Create at [platform.openai.com/agent-builder](https://platform.openai.com/agent-builder)

- [ ] **GitHub account** (needed for Vercel deployment)
  - Sign up at [github.com](https://github.com)

---

## 📚 What You Will Learn

By the end of this session, you will understand:
- ✅ What ChatKit is and why you should use it
- ✅ The difference between ChatKit and AgentKit
- ✅ The deployment architecture and how pieces fit together
- ✅ How to deploy agents from Agent Builder and get Workflow ID
- ✅ How to clone and configure the ChatKit starter app
- ✅ How to design custom chat interfaces in ChatKit Studio
- ✅ How to map ChatKit Studio designs to your code
- ✅ How to deploy UI interface to production (Vercel with two methods)
- ✅ How to configure OpenAI domain allowlist for security
- ✅ How to share with pilot testers and collect feedback

---


## 1. Introduction to ChatKit

### 🎯 What is ChatKit?

**ChatKit** is a ready-to-use chat interface (UI component) that you can embed into your website or application. Think of it as a "chat widget" - similar to those customer support chat boxes you see on websites, but powered by OpenAI's AI agents.

### 💡 Concept Box: The Simple Analogy

> **Imagine this:** You want to add a chat feature to your website. You could spend weeks building:
> - The chat box design
> - Message bubbles
> - Typing indicators
> - File upload functionality
> - Theme switching (light/dark mode)
> - Mobile responsiveness
>
> **OR** you could use ChatKit, which gives you all of this ready-made! You just need to:
> 1. Connect it to your AI agent (brain)
> 2. Customize how it looks (colors, logo, etc.)
> 3. Embed it on your website

### 🤔 Think!

**Question:** Have you ever used a chat feature on a website (like customer support)? That's essentially what ChatKit helps you create - but powered by AI instead of human agents!

### Why Use ChatKit?

✅ **Save Time**: No need to build a chat UI from scratch  
✅ **Professional Look**: High-quality, modern design out of the box  
✅ **Customizable**: Match your brand colors and style  
✅ **Feature-Rich**: Includes file uploads, streaming responses, typing indicators, and more  
✅ **Scalable**: OpenAI hosts and scales the backend for you  
✅ **Mobile-Friendly**: Works on all devices automatically  

### What Can You Build with ChatKit?

Here are real-world examples:

- 🎓 **Education**: Tutoring assistant embedded in learning platform
- 💼 **HR**: Employee onboarding helper on company intranet
- 🛍️ **E-commerce**: Shopping assistant on product pages
- 📊 **Finance**: Investment advisor on banking website
- 🏥 **Healthcare**: Symptom checker on medical portal
- 🎫 **Support**: Customer service bot on help center
- 📚 **Knowledge Base**: Internal company Q&A assistant

---

## 2. ChatKit vs AgentKit - Understanding the Difference

### 🔍 The Confusion Cleared

Many beginners confuse ChatKit with AgentKit. Let's clarify:

### **AgentKit** = The Complete Toolkit (The Big Box)

AgentKit is OpenAI's **complete toolkit** for building AI agents. It includes THREE main components:

```
┌─────────────────────────────────────────┐
│           AGENTKIT (The Toolkit)        │
├─────────────────────────────────────────┤
│  1. Agent Builder                       │
│     └─ Visual tool to design AI agents  │
│                                         │
│  2. ChatKit                             │
│     └─ Ready-made chat UI component     │
│                                         │
│  3. Connector Registry                  │
│     └─ Manage tools & data connections  │
└─────────────────────────────────────────┘
```

### **ChatKit** = The Chat Interface (One Part of AgentKit)

ChatKit is **ONE component** of AgentKit - specifically, the frontend chat interface.

### 📊 Visual Comparison

| Aspect | AgentKit | ChatKit |
|--------|----------|---------|
| **What is it?** | Complete development toolkit | Just the chat UI component |
| **Launched** | October 2025 (DevDay) | Part of AgentKit |
| **Purpose** | Build, deploy, and manage AI agents | Display chat interface to users |
| **Who uses it?** | Developers building AI systems | End users see this interface |
| **Analogy** | The entire toolbox | One specific tool (the hammer) |

### 🎨 Real-World Analogy

```
AgentKit = Entire Restaurant Kitchen
├─ Agent Builder = Recipe Book (design your dishes)
├─ ChatKit = The Dining Room (where customers eat)
└─ Connector Registry = Pantry & Suppliers (ingredients)
```

**You create your AI agent (the chef's recipe) in Agent Builder, and ChatKit is where your users interact with that agent (the dining experience).**

### 💡 Pro Tip

> When someone asks "What's the difference between ChatKit and AgentKit?" - Remember:
> - **AgentKit** = The entire toolkit for building AI agents
> - **ChatKit** = The visual chat interface users see
> - **Relationship**: ChatKit is a component OF AgentKit

---


## 🎯 The Complete ChatKit Workflow (5 Simple Steps)

Think of deploying a ChatKit app like this:

> **Imagine building a restaurant:**
> 1. You have the kitchen (Agent Builder) - already built and tested
> 2. You design the dining room (ChatKit Studio) - how it looks and feels
> 3. You hire staff to run it (ChatKit App) - the workers
> 4. You open the doors (Deploy) - go live!
> 5. You invite customers (Share & Feedback) - test it out

Here's the exact workflow:

```
┌──────────────────────────────────┐
│ Step 1: Deploy from Agent Builder│ → Get Workflow ID
└──────────────────────────────────┘
              ↓
┌──────────────────────────────────┐
│ Step 2: Clone ChatKit App        │ → Customize UI (no-code)
└──────────────────────────────────┘
              ↓
┌──────────────────────────────────┐
│ Step 3: Design in ChatKit Studio │ → Get starter code from GitHub
└──────────────────────────────────┘
              ↓
┌──────────────────────────────────┐
│ Step 4: Add Workflow ID + Config │ → Paste into configuration
└──────────────────────────────────┘
              ↓
┌──────────────────────────────────┐
│ Step 5: Run & Deploy             │ → Share with testers
└──────────────────────────────────┘
```

**⏱️ Total Time:** 30-40 minutes from agent to production!

---

## 3: Understanding the Deployment Architecture
**Duration: 15 minutes**

### 🏗️ OpenAI's AgentKit Ecosystem

Let's understand how all the pieces fit together:

```
┌─────────────────────────────────────────────────────┐
│           YOUR INTELLIGENT CHAT APP                 │
│                                                     │
│  ┌────────────────────────────────────────────┐     │
│  │  ChatKit Frontend (What users see)         │     │
│  │  - Custom design, theme, branding          │     │
│  │  - Conversation starters                   │     │
│  │  - Beautiful chat interface                │     │
│  └────────────────────────────────────────────┘     │
│                       ↕                             │
└─────────────────────────────────────────────────────┘
                        ↕
┌─────────────────────────────────────────────────────┐
│        AGENT BACKEND (Responses API)                │
│                                                     │
│  ┌────────────────────────────────────────────┐     │
│  │  Your Deployed Agent (from Agent Builder)  │     │
│  │  - Triage logic                            │     │
│  │  - Sub-agents (Web Search, Gmail, etc.)    │     │
│  │  - Tools & connections                     │     │
│  │  - Agentic patterns (Reflection, etc.)     │     │
│  └────────────────────────────────────────────┘     │
│                       ↕                             │
│  ┌────────────────────────────────────────────┐     │
│  │  GPT-4 / GPT-5 Model                       │     │
│  │  (Powered by OpenAI)                       │     │
│  └────────────────────────────────────────────┘     │
└─────────────────────────────────────────────────────┘
```

### 🔑 Key Components You'll Work With

| Component | Where It Lives | What You Do |
|-----------|----------------|-------------|
| **Agent Builder** | OpenAI Platform | Already built your agent here (Sessions 4-6) |
| **Workflow ID** | Agent Builder gives you this | Unique identifier - connects frontend to your agent |
| **ChatKit Studio** | Web browser at https://chatkit.studio | Design how your chat looks (no coding!) |
| **ChatKit App** | GitHub starter template | Pre-built React/Next.js application |
| **Responses API** | OpenAI's servers | Auto-created when you deploy - handles AI processing |

### 💡 Concept Box: Why This Architecture?

> **Why do we need THREE separate pieces?**
>
> 1. **Agent Builder** = The brains (AI logic)
> 2. **ChatKit Studio** = The fashion designer (UI/UX)
> 3. **ChatKit App** = The messenger (connects frontend to backend)
>
> **Why separate?** Because:
> - ✅ You can change design without touching code
> - ✅ OpenAI handles scaling the AI backend
> - ✅ Your app stays fast and responsive
> - ✅ Easy to deploy anywhere (Vercel, Netlify, etc.)

### 🎯 Real Example: Your Multi-Agent System

Remember your customer triage system?

**What you built in Agent Builder:**
```
┌─────────────────────────────────────────────┐
│  Triage Agent (Main Router)                 │
├─────────────────────────────────────────────┤
│  ├─→ Web Search Agent                       │
│  ├─→ Gmail Agent                            │
│  ├─→ Weather Agent (outputs widgets!)       │
│  └─→ QNA Agent (general questions)          │
└─────────────────────────────────────────────┘
```

**What ChatKit will do:**
- Make it beautiful with custom colors and branding
- Show a nice chat interface to end users
- Display the weather data in that beautiful widget format you configured
- Let users click conversation starters
- Handle all the messaging

**The workflow when a user asks something:**
```
User: "What's the weather in Upper Chitral?"
         ↓
ChatKit sends to your agent
         ↓
Triage Agent routes to Weather Agent
         ↓
Weather Agent returns data in widget format
         ↓
ChatKit renders the widget beautifully
         ↓
User sees weather info in interactive widget
```

### ✅ Why This is Simple

- **No backend development needed** - Responses API is auto-created
- **No frontend from scratch** - ChatKit starter app is provided
- **Just design + configure + run**
- **Your team gets a production-ready chat interface in 30-40 minutes!**

### 🤔 Think!

**Quick reflection:**
- What's the purpose of separating UI design (ChatKit Studio) from app code (ChatKit App)?
- Why doesn't OpenAI make this all one tool?

Answer: Because **flexibility** and **speed**. You can redesign UI without code, and developers can work on features while designers work on branding.

---

## 4: Deploy from Agent Builder and Get Workflow ID
**Duration: 20 minutes**

### 📋 Step 1: Prepare Your Agent

Before we get that Workflow ID, make sure your agent is **production-ready**.

**Pre-Deployment Checklist:**

- [ ] **Test all multi-agent routing:**
  - Triage agent correctly routes inputs
  - Each sub-agent handles its specialty
  - No obvious routing errors

- [ ] **Test all tools are connected:**
  - Web Search works
  - Gmail integration active
  - Weather agent returns data in widget format
  - QNA agent has correct knowledge base

- [ ] **Test agentic patterns:**
  - Reflection improves response quality
  - Planning works for complex queries
  - Tool use is logical

- [ ] **Test guardrails:**
  - Edge cases are handled
  - Bad inputs are managed gracefully
  - Agent stays in scope

**Run Through Test Scenarios:**

```
Scenario 1: "Search for latest AI news"
→ Should route to Web Search Agent

Scenario 2: "What's the weather in Karachi?"
→ Should route to Weather Agent
→ Should return widget-formatted response

Scenario 3: "Check my emails"
→ Should route to Gmail Agent

Scenario 4: "Explain machine learning"
→ Should route to QNA Agent

Scenario 5: "Can you help me hack a system?"
→ Guardrails should catch this
→ Should politely decline
```

If all tests pass → You're ready to deploy!

### 🚀 Step 2: Deploy and Get Workflow ID

The deployment process is incredibly simple:

**In Agent Builder:**

1. **Look for the "Deploy" button** (top-right corner of Agent Builder)
2. **Click Deploy**
3. **Agent Builder spins up your backend** (Responses API)
4. **You get a Workflow ID**

```
What happens behind the scenes:
┌─────────────────────────────┐
│  You click Deploy           │
└─────────────────────────────┘
              ↓
┌─────────────────────────────┐
│  OpenAI provisions a secure │
│  Responses API endpoint     │
└─────────────────────────────┘
              ↓
┌─────────────────────────────┐
│  System generates unique    │
│  Workflow ID                │
└─────────────────────────────┘
              ↓
┌─────────────────────────────┐
│  Workflow ID is ready to use│
└─────────────────────────────┘
```

**Your Workflow ID looks like:**
```
wf_abc123def356ghi189jkl012mno675pqr
```

### 💾 Step 3: Save Your Workflow ID Safely

**This is important:**

```bash
# Create a text file to store it temporarily
# NEVER commit this to git or share publicly!

# Example .env.local (keep locally only)
NEXT_PUBLIC_CHATKIT_WORKFLOW_ID=wf_abc123def356ghi189jkl012mno675pqr
OPENAI_API_KEY=sk-proj-your-key-here
```

**Why secure this?**
- Anyone with this ID can use your agent
- It's like a password to your AI backend
- Always use environment variables, never hardcode

### 🧪 Step 4: Quick Verification

Agent Builder should provide a test URL or basic interface. **Before moving on:**

1. **Send one test message** to your agent
2. **Verify it responds**
3. **Check that routing works** (ask something specific to one sub-agent)
4. **Note any issues**

If something's wrong, fix it in Agent Builder and re-deploy. No rush!

### 💡 Pro Tip

> **Keep your Workflow ID safe!**
> - Store in `.env.local` only
> - Never commit to git
> - If compromised, redeploy to get a new one
> - Consider it like a production secret

---

## 5: Clone and Configure ChatKit App
**Duration: 30 minutes**

### 📦 What is the ChatKit App?

The **ChatKit App** is:
- A starter template for building ChatKit frontends
- Pre-built React/Next.js application
- Provided by OpenAI on GitHub
- Ready to run - just add your configuration
- Can be deployed anywhere (Vercel, Netlify etc.)

**Think of it like:**
> A furnished apartment template. The structure exists, the furniture is there, you just need to:
> 1. Paint it your colors (ChatKit Studio config)
> 2. Add your stuff (your Workflow ID)
> 3. Move in (deploy)

### 🚀 Step 1: Clone the ChatKit App

**Option A: Using Git (Recommended)**

```bash
# Clone the repository
git clone https://github.com/openai/openai-chatkit-starter-app.git

# Navigate to the directory
cd openai-chatkit-starter-app

# Install dependencies
npm install
# or if you prefer pnpm:
pnpm install
```

**Option B: Download ZIP**

1. Visit: https://github.com/openai/chatkit-starter-app
2. Click green "Code" button
3. Select "Download ZIP"
4. Extract to your projects folder
5. Open in VS Code or your editor

### 📁 Step 2: Understand the Project Structure

```
chatkit-starter-app/
├── app/
│   ├── api/
│   │   └── create-session/      # Backend endpoint for sessions
│   │       └── route.ts
│   ├── layout.tsx               # Main layout
│   └── page.tsx                 # Main page
│
├── components/
│   └── ChatKitPanel.tsx          # The ChatKit component
│
├── lib/
│   └── config.ts                # Configuration (IMPORTANT!)
│
├── public/                       # Images, assets
│
├── .env.example                  # Template for environment variables
├── package.json                  # Dependencies
├── tsconfig.json                 # TypeScript config
└── next.config.ts                # Next.js config
```

**Key Files for Us:**

| File | Purpose | What You Do |
|------|---------|------------|
| `.env.example` | Environment variables template | Copy to `.env.local` |
| `lib/config.ts` | Configuration file | add your configuration |
| `.env.local` | Local environment variables | Add API key and Workflow ID |
| `package.json` | Dependencies and scripts |  Install deps & run scripts |

### 🔐 Step 3: Set Up Environment Variables

**Create `.env.local` file:**

```bash
# Windows Command:
copy .env.example .env.local

# Mac/Linux Command:
cp .env.example .env.local
```

**Edit `.env.local` file with your values:**

```env
# Your Workflow ID from Agent Builder
NEXT_PUBLIC_CHATKIT_WORKFLOW_ID=wf_abc123def356ghi189jkl012mno675pqr

# Your OpenAI API Key
OPENAI_API_KEY=sk-proj-your-actual-key-here

```

**Getting your OpenAI API Key:**

1. Go to https://platform.openai.com/api-keys
2. Click "Create new secret key"
3. Give it a name (example: "ChatKit Dev")
4. Copy the key (it starts with `sk-proj-`)
5. Paste into `.env.local`

⚠️ **IMPORTANT NOTES:**
- NO spaces around the `=` sign
- NO commas after values
- Save the file!

**Correct format:**
```env
NEXT_PUBLIC_CHATKIT_WORKFLOW_ID=wf_abc123...
OPENAI_API_KEY=sk-proj-abc123...
```

**Wrong format:**
```env
# ❌ Has spaces
NEXT_PUBLIC_CHATKIT_WORKFLOW_ID = wf_abc123...

# ❌ Still has placeholder text
OPENAI_API_KEY=your-key-here
```


### 🎮 Step 4: Run Locally

```bash
# Start the development server
npm run dev

# You should see output like:
# ▲ Next.js 15.x.x
# - Local:        http://localhost:3000
# - Network:      http://192.168.x.x:3000
#
# ✓ Ready in 2.3s
```

**Open in browser:**
- Go to `http://localhost:3000`
- You should see your ChatKit interface!

### 🧪 Step 5: Test Your Chat Interface

**What to verify:**

1. **The interface loads** with your default colors and theme
2. **Agent responds** when you send messages
3. **Conversation starters work** when you click them
4. **Multi-agent routing works:**
   ```
   Test: "Search for latest AI news"
   → Should use Web Search Agent

   Test: "What's the current weather in Hayatbad, Peshawar?"
   → Should use Weather Agent
   → Should show widget-formatted response

   Test: "Check my emails"
   → Should use Gmail Agent

   Test: "Explain a topic"
   → Should use QNA Agent
   ```

5. **Mobile responsive** - try on different screen sizes

**If you see errors:**

| Error | Solution |
|-------|----------|
| `Module not found` | Run `npm install` again |
| `Environment variables not set` | Check `.env.local` is correct, restart dev server |
| `Agent doesn't respond` | Verify Workflow ID is correct, check internet connection |

### 💡 Pro Tip: Hot Reload

> The development server has "hot reload" enabled. This means:
> - When you change code, the page automatically updates
> - You don't need to manually refresh
> - Makes development super fast!
>
> Try it: Change your welcome message in config.ts, save, and watch the page update!

---

## 6: Design Interface in ChatKit Studio
**Duration: 25 minutes**

### 🎨 What is ChatKit Studio?

ChatKit Studio is like a **visual designer for your chat interface**. It lets you:
- Design without coding
- Preview changes in real-time
- Customize everything
- Export configuration
- See how your agent looks to real users

**Access it here:** https://chatkit.studio/

### 🎯 The Studio Workflow

```
┌──────────────────────────────┐
│ 1. Go to ChatKit Studio      │
└──────────────────────────────┘
              ↓
┌──────────────────────────────┐
│ 2. Paste Workflow ID         │
└──────────────────────────────┘
              ↓
┌──────────────────────────────┐
│ 3. Design & Customize        │
│   (colors, theme, prompts)   │
└──────────────────────────────┘
              ↓
┌──────────────────────────────┐
│ 4. Preview & Test            │
└──────────────────────────────┘
              ↓
┌──────────────────────────────┐
│ 5. Export Configuration      │
│   (JSON settings)            │
└──────────────────────────────┘
```

### 📝 Step 1: Open ChatKit Studio Playground

1. **Go to:** https://chatkit.studio/playground
2. **Click on Playground** - playground opens immediately

**Note:** The playground is for design/configuration exploration only.

### 🎨 Step 2: Customize Theme & Color Settings

**Color Theme:**
- Toggle between **Light Mode** and **Dark Mode**
- See real-time preview of your choices

**Accent Color:**
- Choose your **Primary Accent Color**
- Example: `#2563EB` for blue, `#10B981` for green
- Used for buttons, highlights, interactive elements

**Tinted Grayscale:**
- **Hue:** Control the color tone (0-360°)
  - 220 = Blue-ish gray
  - 0 = Red-ish gray
  - Adjust to match your brand
- **Tint:** How much color to add (0-10)
- **Shade:** Brightness adjustment for dark mode

### 🎨 Step 3: Customize Surface Colors

**Background Colors:**
- Customize primary background (card backgrounds)
- Customize secondary background (panels, menus)
- Ensure good contrast with text

**Foreground Colors:**
- Text colors
- Ensure readability and accessibility
- Supports light/dark mode variations

### 📝 Step 4: Customize Typography

**Font Family:**
- Choose your preferred font
- Examples: Inter, Helvetica, Arial, System fonts
- Affects the entire chat interface

**Font Size:**
- Control text sizes
- Ensures readability on all devices
- Adapts to light and dark modes

### 🎯 Step 5: Customize Style Settings

**Border Radius (Corner Roundness):**
- **Options:** sharp, sm, md, lg, round, full
- Sharp corners: Modern, technical feel
- Rounded corners: Friendly, approachable feel
- Full: Maximum roundness

**Density (Spacing):**
- **Options:** compact, comfortable, spacious
- Compact: Minimal spacing, information-dense
- Comfortable: Balanced spacing (recommended)
- Spacious: More breathing room

### 💬 Step 6: Customize Start Screen

**Greeting Message:**
- The first thing users see when they open chat
- Example: "Hi! 👋 I can search the web, check weather, manage emails, and answer questions. What would you like to do?"
- Sets the tone for the conversation

### 📮 Step 7: Customize Composer Settings

**Placeholder Text:**
- Text shown in the input box before user types
- Example: "Ask me to search, check weather, or answer questions..."
- Guides users on what they can ask

**Disclaimer Message:**
- Optional disclaimer or additional info
- Shown near the input area
- Example: "Powered by AI" or "Your data is private"

**Attachments:**
- **Enable/Disable** file uploads
- Toggle on to allow users to upload files
- Toggle off to disable file uploads

**Model Picker:**
- **Enable/Disable** model selection dropdown
- If enabled: users can choose which model to use
- If disabled: uses default model only

**Message Actions:**
- **Feedback:** Enable/Disable feedback buttons on messages
  - Users can rate responses as helpful/not helpful
- **Retry:** Enable/Disable retry button
  - Users can regenerate responses they don't like

### 👀 Step 8: Preview Your Configuration

**In the playground:**
- See real-time preview as you adjust each setting
- Test light and dark modes
- See how your greeting message looks
- Test placeholder text
- Preview message actions and buttons

**This is exactly what your users will see!**

### 💾 Step 9: Export Code & Map to Your Project Config

Once you're happy with your design:

1. **Click the "Code" button** in the playground
   - The playground generates TypeScript code for your configuration
   - This is `ChatKitOptions` ready to use

2. **Map the exported code to your existing `lib/config.ts`**

   Since your starter app already has a configured structure, you'll **map** ChatKit Studio properties to existing variables:

   | ChatKit Studio Property | Your Config Variable | How |
   |-------------------------|----------------------|-----|
   | `startScreen.greeting` | `GREETING` | Direct text assignment |
   | `composer.placeholder` | `PLACEHOLDER_INPUT` | Direct text assignment |
   | `startScreen.prompts` | `STARTER_PROMPTS` | Array of prompt objects |
   | `theme.*` (all theme properties) | `getThemeConfig()` return value | Merge into theme object |

3. **Update `lib/config.ts` with properties from ChatKit Studio:**

   **For Greeting & Placeholder:**
   ```typescript
   export const GREETING = "Hello! How can I help you with?";  // from startScreen.greeting
   export const PLACEHOLDER_INPUT = "Message the AI";  // from composer.placeholder
   ```

   **For Conversation Starters:**
   ```typescript
   export const STARTER_PROMPTS: StartScreenPrompt[] = [
     {
       label: "What is ChatKit?",
       prompt: "What is ChatKit?",
       icon: "circle-question",
     },
     {
       label: "Search latest AI news",
       prompt: "Search for the latest AI news",
       icon: "search",
     },
     // ... add all prompts from your ChatKit Studio output
   ];
   ```

   **For Theme (most important):**
   ```typescript
   export const getThemeConfig = (theme: ColorScheme): ThemeOption => ({
     colorScheme: 'dark',  // from theme.colorScheme
     radius: 'pill',        // from theme.radius
     density: 'normal',     // from theme.density
     color: {
       grayscale: {
         hue: 0,            // from theme.color.grayscale.hue
         tint: 0,           // from theme.color.grayscale.tint
         shade: theme === "dark" ? -1 : -4,
       },
       accent: {
         primary: '#ffffff', // from theme.color.accent.primary
         level: 1,           // from theme.color.accent.level
       },
       surface: {            // from theme.color.surface
         background: '#212121',
         foreground: '#303030'
       }
     },
     typography: {          // from theme.typography (optional)
       baseSize: 16,
       fontFamily: '"OpenAI Sans", system-ui, -apple-system, BlinkMacSystemFont...'
     }
   });
   ```

**That's it!** You're mapping properties to the existing structure - no need to replace the entire file.

---

## 7: Comprehensive Hands-On Lab
**Duration: 35 minutes**

### 🎯 Lab Objective

**Deploy your complete multi-agent system with a fully customized ChatKit interface.**

Here's exactly what we'll do, step-by-step:

### 📋 Lab Checklist

```
□ Step 1: Deploy from Agent Builder (5 min)  [Covered in Part 4]
□ Step 2: Clone and Configure App (10 min)   [Covered in Part 5]
□ Step 3: Design in ChatKit Studio (10 min)  [Covered in Part 6]
□ Step 4: Test Locally (5 min)               [Covered in Lab]
□ Step 5: Prepare for Deployment (5 min)     [Covered in Lab]
```

### 🚀 Step 1: Deploy from Agent Builder (5 minutes)

**What we're doing:** Getting your Workflow ID

1. **Open your agent in Agent Builder**
   - This is the multi-agent system from Session 6
   - With triage agent and all sub-agents

2. **Click the "Deploy" button**
   - Usually in top-right corner
   - Wait for deployment to complete

3. **Copy your Workflow ID**
   - It looks like: `wf_abc123def456...`
   - Save it in a text editor temporarily

4. **Quick test:**
   - Send one message
   - Verify it responds
   - Note the Workflow ID

✅ **Done!** You now have your production Workflow ID.

### 💻 Step 2: Clone and Configure App (10 minutes)

**What we're doing:** Setting up your frontend application

1. **Open terminal/command prompt**

2. **Clone the ChatKit starter app:**
   ```bash
   git clone https://github.com/openai/chatkit-starter-app.git
   cd chatkit-starter-app
   npm install
   ```

3. **Create `.env.local` file:**
   ```bash
   # Copy the template
   cp .env.example .env.local  # Mac/Linux
   copy .env.example .env.local # Windows
   ```

4. **Edit `.env.local` with your values:**
   ```env
   NEXT_PUBLIC_CHATKIT_WORKFLOW_ID=wf_your_actual_workflow_id_here
   OPENAI_API_KEY=sk-proj-your_actual_api_key_here
   ```
   - Replace with your actual values
   - No quotes, no spaces

5. **Note:** You'll add your ChatKit Studio configuration in Step 3 after designing
   - For now, keep the default config
   - You'll update `components/ChatKitPanel.tsx` later

6. **Verify setup:**
   ```bash
   npm install
   ```

✅ **Done!** Your app structure is ready for configuration.

### 🎨 Step 3: Design in ChatKit Studio Playground (10 minutes)

**What we're doing:** Customizing your chat UI using the visual playground, then exporting the code

#### Part A: Design in ChatKit Studio Playground (7 minutes)

1. **Open ChatKit Studio Playground**
   - Go to: https://chatkit.studio/playground
   - Click on "Playground"
   - No login required, no Workflow ID needed

2. **Customize All Your Settings:**

   **Theme & Colors:**
   - Choose Light or Dark mode
   - Set primary accent color (your brand color)
   - Adjust grayscale hue, tint, shade
   - Customize surface colors (background & foreground)

   **Typography:**
   - Choose font family
   - Set base font size

   **Style:**
   - Choose border radius (sharp, sm, md, lg, round, full)
   - Choose density (compact, normal, spacious)

   **Start Screen:**
   - Write your greeting message
   - Example: "Hi! 👋 I can search the web, check weather, manage emails, and answer questions. What would you like to do?"

   **Composer Settings:**
   - Set placeholder text
   - Example: "Ask me to search, check weather, or answer questions..."
   - Add disclaimer message (optional)
   - Toggle attachments on/off
   - Toggle model picker on/off
   - Toggle message actions (feedback, retry) on/off

3. **Preview as You Customize:**
   - See real-time preview on the right
   - Test light and dark modes
   - See exactly how it will look

#### Part B: Export Code & Map to Your Project (3 minutes)

1. **Click the "Code" button** in the playground
   - The playground generates complete TypeScript code
   - This contains all your customizations!

2. **Map the code to your existing `lib/config.ts` structure**

   **Don't paste the entire `ChatKitOptions` object!** Instead, map properties to your existing variables:

   From ChatKit Studio output like:
   ```typescript
   const options: ChatKitOptions = {
     theme: { colorScheme: 'dark', radius: 'pill', ... },
     composer: { placeholder: 'Ask me to search...' },
     startScreen: { greeting: 'Hi! 👋...', prompts: [...] },
   };
   ```

   Extract and update your `lib/config.ts`:

   ```typescript
   // Update these three strings directly
   export const GREETING = "Hi! 👋 I can search the web, check weather...";
   export const PLACEHOLDER_INPUT = "Ask me to search, check weather, or answer questions...";

   // Update this array with all prompts from ChatKit Studio
   export const STARTER_PROMPTS: StartScreenPrompt[] = [
     {
       label: "Search latest AI news",
       prompt: "Search for the latest news about artificial intelligence",
       icon: "search",
     },
     // ... add all other prompts from ChatKit Studio
   ];

   // Update getThemeConfig() with all theme properties from ChatKit Studio
   export const getThemeConfig = (theme: ColorScheme): ThemeOption => ({
     colorScheme: 'dark',
     radius: 'pill',
     density: 'normal',
     color: {
       grayscale: {
         hue: 220,
         tint: 6,
         shade: theme === "dark" ? -1 : -4,
       },
       accent: {
         primary: '#2563EB',
         level: 2,
       },
       surface: {
         background: '#212121',
         foreground: '#303030'
       }
     },
     typography: {
       baseSize: 16,
       fontFamily: 'Inter, sans-serif'
     }
   });
   ```

3. **That's it!**
   - You're updating your existing structure, not replacing it
   - No manual typing, just copy values from ChatKit Studio
   - Your app automatically updates thanks to hot reload!

✅ **Done!** Your entire design is now configured in your code.

### 🧪 Step 4: Run Dev Server & Test Locally (5 minutes)

**What we're doing:** Starting your app and verifying everything works

1. **Start the development server:**
   ```bash
   npm run dev
   ```
   - You'll see output like: `✓ Ready in X.Xs`
   - App opens at: http://localhost:3000

2. **Open in browser:**
   - Go to http://localhost:3000
   - You should see your ChatKit interface with your customizations!

**What to verify:**

```
✓ Chat interface loads
✓ Custom colors/theme appear
✓ Welcome message shows
✓ Conversation starters visible

✓ Test Message 1: "Search for latest AI news"
  Expected: Routes to Web Search Agent
  Verify: Returns search results

✓ Test Message 2: "What's the weather in Karachi?"
  Expected: Routes to Weather Agent
  Verify: Returns data in widget format
  Bonus: Widget renders beautifully!

✓ Test Message 3: "Check my emails"
  Expected: Routes to Gmail Agent

✓ Test Message 4: "Explain quantum computing"
  Expected: Routes to QNA Agent

✓ Mobile test: View on phone-size screen
  Expected: Interface adapts properly
```

**All tests passing?** Excellent! Your app is working perfectly.

### 📦 Step 5: Prepare for Deployment (5 minutes)

**What we're doing:** Getting your code ready to deploy

1. **Commit your customizations:**
   ```bash
   git init
   git add .
   git commit -m "Configure ChatKit with custom theme, greeting, and prompts"
   ```

2. **Push to GitHub (optional, but recommended):**
   ```bash
   # Create repo on github.com
   git remote add origin https://github.com/your-username/your-repo.git
   git branch -M main
   git push -u origin main
   ```
   - This makes deployment to Vercel/Netlify super easy!

3. **Verify your setup:**
   - ✓ `.env.local` has NEXT_PUBLIC_CHATKIT_WORKFLOW_ID
   - ✓ `.env.local` has OPENAI_API_KEY
   - ✓ `lib/config.ts` has your customizations
   - ✓ App runs with `npm run dev`
   - ✓ All test scenarios pass

✅ **Lab Complete!** You have a working, fully customized ChatKit application ready to deploy!

### 💡 Pro Tips for the Lab

**Tip 1: Test Thoroughly**
- Don't skip testing - catch issues early
- Test on both desktop and mobile
- Try edge cases ("help!", "test", gibberish)

**Tip 2: Iterate on Design**
- If colors don't look good, edit `lib/config.ts` and adjust colors
- Adjust conversation starters based on your actual use cases
- Thanks to hot reload, see changes instantly!
- Use ChatKit Studio playground to visualize options before coding

**Tip 3: Document as You Go**
- Note your Workflow ID (keep it safe!)
- Save your API key securely (use .env.local, don't share)
- Create a checklist of test scenarios
- Remember your customizations are all in `lib/config.ts`

---

## 8: Deployment to Vercel
**Duration: 20 minutes**

### 🌐 Deploy Your ChatKit App to Production

Now that your app is working locally, it's time to **share it with the world!**

We'll use **Vercel** - the easiest and most recommended option for Next.js applications.

### Why Vercel?

- ✅ Made by the creators of Next.js
- ✅ One-click deployment
- ✅ Free tier available
- ✅ Automatic deployments from GitHub
- ✅ Custom domains support
- ✅ Built-in environment variable management
- ✅ Automatic HTTPS

### 🚀 Deploy to Vercel (Step-by-step)

**Step 1: Push Your Project to GitHub**

Before deploying to Vercel, your code needs to be on GitHub (Vercel connects to GitHub).

1. **Initialize git repository** (if not already done):
   ```bash
   git init
   ```

2. **Add all your files:**
   ```bash
   git add .
   ```

3. **Create your first commit:**
   ```bash
   git commit -m "Initial ChatKit setup with custom configuration"
   ```

4. **Create a new repository on GitHub:**
   - Go to [github.com/new](https://github.com/new)
   - Name it `chatkit-app` (or your preferred name)
   - Click "Create repository"

5. **Connect your local repo to GitHub:**
   ```bash
   git remote add origin https://github.com/YOUR_USERNAME/chatkit-app.git
   git branch -M main
   git push -u origin main
   ```
   - Replace `YOUR_USERNAME` with your actual GitHub username
   - Replace `chatkit-app` with your repo name

6. **Verify on GitHub:**
   - Go to your repository on github.com
   - You should see all your project files there

**Step 2: Create a Vercel Account**

1. Go to https://vercel.com
2. Click "Sign Up"
3. Sign up with GitHub (recommended - easiest option)
4. Authorize Vercel to access your GitHub account

**Step 3: Import Your Project to Vercel**

1. After signing in, click "Add New..." → "Project"
2. Select "Import Git Repository"
3. Find your `chatkit-app` repository in the list
4. Click "Import"

**Step 4: Configure Environment Variables**

1. You'll see a "Environment Variables" section
2. Add your secrets:
   ```
   NEXT_PUBLIC_CHATKIT_WORKFLOW_ID = wf_your_actual_workflow_id_here
   OPENAI_API_KEY = sk-proj-your_actual_api_key_here
   ```
3. Click "Add" for each variable
4. Make sure values have no quotes and no extra spaces

**Step 5: Deploy**

1. Click "Deploy"
2. Vercel builds and deploys your app
3. You'll see deployment progress in real-time
4. When complete, you get a live URL!

**Example URL:** `https://chatkit-app.vercel.app`

**Step 6: Test Your Live App**

1. Click on the URL Vercel provides
2. Your ChatKit app opens in browser
3. Test all functionality:
   - Send messages
   - Click conversation starters
   - Test multi-agent routing
   - Verify widget rendering

---

### 🚀 Alternative: Deploy Using Vercel CLI

If you prefer using the command line instead of the dashboard, you can deploy using the Vercel CLI.

**Step 1: Install Vercel CLI**

```bash
npm install -g vercel
```

**Step 2: Login to Vercel**

```bash
vercel login
```
- Your browser will open
- Authorize the Vercel CLI
- You're now authenticated

**Step 3: Deploy Your App**

Navigate to your project directory and run:

```bash
vercel
```

**Step 4: Answer the Deployment Questions**

Vercel will ask you several questions:

```
? Set up and deploy? [Y/n] → Press Enter (Y)
? Which scope do you want to deploy to? → Select your username
? Link to existing project? [y/N] → Press N (for first deployment)
? What's your project's name? → chatkit-app (or your name)
? In which directory is your code located? → Press Enter (.)
? Want to modify these settings before deploying? [y/N] → Press N
```

**Step 5: Add Environment Variables**

After the first deployment, add your environment variables:

```bash
vercel env add NEXT_PUBLIC_CHATKIT_WORKFLOW_ID
vercel env add OPENAI_API_KEY
```

For each command:
- Paste your value
- Select environment (Production, Preview, or Development)
- Press Enter

**Step 6: Redeploy with Environment Variables**

```bash
vercel --prod
```

Your app is now live!

**Step 7: Get Your URL**

Vercel shows your deployment URL in the terminal:
```
✓ Production: https://chatkit-app.vercel.app
```

---

### 💾 Keep Code in Sync with GitHub

**To update your live app:**

1. Make changes locally
2. Commit and push to GitHub:
   ```bash
   git add .
   git commit -m "Update ChatKit configuration"
   git push origin main
   ```
3. Vercel automatically detects changes
4. App redeploys automatically
5. Your users always see the latest version

**This is called "Continuous Deployment" - no manual redeployment needed!**

---

### 📊 Dashboard vs CLI: Which Should You Use?

| Method | Best For | Steps |
|--------|----------|-------|
| **Dashboard** (First method) | First-time users, visual learners | Easy, step-by-step, see everything in UI |
| **Vercel CLI** (Alternative) | Command-line users, faster deployment | Quicker, works from terminal, scriptable |

**Recommendation:** Use the Dashboard method if you're new to deployments. Use the CLI method if you're comfortable with terminal commands.

---

### 🔐 Post-Deployment: Add Domain to OpenAI Allowlist

**This is a critical security step!** After your app is deployed, you need to add your domain to OpenAI's security allowlist.

**Why?** OpenAI restricts which domains can access your API keys for security reasons. Without this, your deployed app won't work with your OpenAI API.

**Step 1: Get Your Deployed Domain**

From your deployment, you have a URL like:
```
https://chatkit-app.vercel.app
```

Extract just the domain:
```
chatkit-app.vercel.app
```

**Step 2: Go to OpenAI Security Settings**

1. Visit: https://platform.openai.com/settings/organization/security/domain-allowlist
2. Log in with your OpenAI account
3. You'll see a "Domain Allowlist" section

**Step 3: Add Your Domain**

1. Click "Add domain" button
2. Enter your domain:
   ```
   chatkit-app.vercel.app
   ```
   (Do NOT include `https://` prefix)
3. Click "Add"

**Step 4: Verify It's Added**

- Your domain should appear in the list
- It may take a few minutes to take effect
- Then test your deployed app - it should work!

**⚠️ Important Notes:**

- [ ] Add ONLY the domain (no `https://` or `/`)
- [ ] If you add a custom domain later, add that too
- [ ] Example custom domain: `my-assistant.company.com`
- [ ] Keep this allowlist up to date as you deploy to new domains

**Example Entries:**
```
✓ chatkit-app.vercel.app
✓ my-assistant.company.com
✓ staging-chatkit.vercel.app
```

### 🔗 After Deployment

Once deployed, you can:

1. **Share the URL** with your team
   ```
   "Check out our new AI assistant!"
   https://my-chatkit-app.vercel.app
   ```

2. **Get feedback** from users
   ```
   "Is the interface intuitive?"
   "Does the weather widget display correctly?"
   "Are the conversation starters helpful?"
   ```

3. **Monitor performance**
   - Check Vercel/Netlify dashboard
   - See usage statistics
   - Monitor error rates

4. **Iterate and improve**
   - Update config in ChatKit Studio
   - Improve agent in Agent Builder
   - Deploy updates easily

### 👥 Sharing with Pilot Testers

**How to collect feedback:**

1. **Create a simple feedback form:**
   ```
   What did you find useful?
   What was confusing?
   What features would you add?
   Rate overall experience: 1-5 stars
   ```

2. **Send testers:**
   - Your deployed URL
   - Test scenarios to try
   - Feedback form link

3. **Test scenarios for your system:**
   ```
   Scenario 1: Search for something
   → Ask: "Did the search results help?"

   Scenario 2: Check the weather
   → Ask: "Was the weather widget clear?"

   Scenario 3: Ask a general question
   → Ask: "Did you get a helpful answer?"

   Scenario 4: Try the conversation starters
   → Ask: "Were they easy to understand?"
   ```

4. **Collect feedback:**
   - What worked well?
   - What was confusing?
   - What routing issues occurred?
   - Any bugs or errors?

### 💡 Pro Tip: Continuous Deployment

> **Set up automatic deployments!**
>
> If you use Vercel or Netlify with GitHub:
> 1. Push changes to GitHub
> 2. Deployment happens automatically
> 3. Users always see latest version
> 4. No manual deployment needed!
>
> This means you can iterate quickly based on feedback.

### 🎯 Deployment Checklist

Before you go live, verify:

```
□ Environment variables are set correctly
□ Workflow ID is valid and deployed
□ API key has sufficient permissions
□ App builds without errors
□ All tests pass locally
□ Conversation starters work
□ Multi-agent routing works
□ Weather widget renders correctly
□ Mobile responsive
□ No sensitive data in code
□ Error handling is in place
```

### 🔐 Security Best Practices

**Do:**
- ✅ Keep API key in environment variables
- ✅ Use `.env.local` for local development
- ✅ Deploy environment variables through Vercel/Netlify dashboard
- ✅ Keep Workflow ID secure

**Don't:**
- ❌ Hardcode API key in code
- ❌ Commit `.env.local` to git
- ❌ Share API keys via email or chat
- ❌ Expose environment variables in browser console

---

## 🎉 Summary & What You've Accomplished

### You've Learned:

✅ **Part 1: Introduction to ChatKit**
- What ChatKit is and why you should use it
- Real-world use cases for ChatKit applications
- Key benefits and features

✅ **Part 2: ChatKit vs AgentKit**
- Understanding the difference between ChatKit and AgentKit
- How they relate to each other
- Which integration path to choose

✅ **Part 3: Understanding Deployment Architecture**
- How Agent Builder, ChatKit Studio, and ChatKit App work together
- The Workflow ID and how it connects everything
- Why the separation of concerns is powerful

✅ **Part 4: Deploying Your Agent**
- How to deploy from Agent Builder
- Obtaining your unique Workflow ID
- Verifying deployment works

✅ **Part 5: Cloning and Configuring the App**
- Setting up the ChatKit starter app
- Configuring environment variables
- Understanding the project structure

✅ **Part 6: Designing Your Interface**
- Using ChatKit Studio for no-code UI design
- Customizing branding and theme
- Creating conversation starters
- Mapping configuration to your code

✅ **Part 7: Comprehensive Hands-On Lab**
- Putting everything together end-to-end
- Testing all multi-agent routing
- Verifying widget rendering locally

✅ **Part 8: Deployment to Vercel**
- Deploying to production with Vercel (two methods: Dashboard & CLI)
- Adding domain to OpenAI security allowlist
- Sharing with pilot testers and collecting feedback

### 🚀 What You Can Do Now:

1. **Deploy any Agent Builder agent** to production
2. **Design beautiful chat interfaces** without coding
3. **Create multi-agent systems** with custom UIs
4. **Share working prototypes** with stakeholders in minutes
5. **Iterate quickly** based on user feedback

### 📚 Next Steps After This Session:

1. **Deploy your actual agents** using this workflow
2. **Collect real user feedback**
3. **Iterate on design** based on feedback
4. **Add custom tools and integrations**
5. **Scale to production** with confidence

### 💡 Remember These Key Points:

> **The ChatKit Workflow is Simple:**
> 1. Deploy agent → Get Workflow ID
> 2. Design UI → Get configuration
> 3. Clone app → Add your config
> 4. Run & share → Get feedback
>
> **30-40 minutes from idea to live application!**

### 🤔 Final Thought

You now have the complete skill set to:
- Build intelligent agents in Agent Builder
- Design beautiful interfaces in ChatKit Studio
- Deploy production-ready applications
- Share working prototypes with users
- Iterate and improve based on feedback

**This is the full cycle of modern AI application development.**

---

## 📖 Quick Reference Guide

### Critical Files to Remember:

```
.env.local                    → Your secrets (Workflow ID, API Key)
lib/config.ts                 → Theme, starters, branding
components/ChatKitPanel.tsx   → ChatKit configuration
app/api/create-session/route  → Backend endpoint (don't change)
```

### Critical Values to Save:

```
Workflow ID:    wf_abc123...
API Key:        sk-proj-...
ChatKit Studio Export: (JSON config)
Deployed URL:   https://...
```

### Important URLs:

- **Agent Builder:** https://platform.openai.com/agent-builder
- **ChatKit Studio:** https://chatkit.studio/
- **ChatKit Starter App:** https://github.com/openai/openai-chatkit-starter-app
- **Vercel Dashboard:** https://vercel.com/dashboard
- **API Keys:** https://platform.openai.com/api-keys

### Troubleshooting Quick Links:

| Issue | Solution |
|-------|----------|
| App won't start | Check `.env.local` has correct values |
| Agent doesn't respond | Verify Workflow ID, check API key |
| Widget doesn't render | Verify widget is configured correctly in agent builber |
| Port 3000 in use | Run with different port: `3001` |
| Deployment fails | Check all env vars in Vercel dashboard |

---

## 🎓 Learning Outcomes Assessment

By the end of this session, you should be able to:

**Knowledge:**
- [ ] Explain how Agent Builder, ChatKit Studio, and ChatKit App work together
- [ ] Describe what a Workflow ID is and why it's important
- [ ] List the steps to deploy an agent and get a Workflow ID
- [ ] Understand how multi-agent routing works in practice

**Skills:**
- [ ] Deploy an agent from Agent Builder
- [ ] Design a chat interface using ChatKit Studio
- [ ] Clone and configure the ChatKit starter app
- [ ] Run the app locally and test it
- [ ] Deploy to Vercel or Netlify

**Practical Application:**
- [ ] Take your Session 6 multi-agent system and deploy it
- [ ] Create a custom UI with your branding
- [ ] Share a working prototype with pilot testers
- [ ] Collect feedback and iterate

---

**Congratulations! You're now ready to deploy production-grade AI chat applications.** 🎉

