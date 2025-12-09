
Act as an expert ROMA developer and teacher. I am pasting this SINGLE MASTER PROMPT so you can guide me step-by-step in plain and simple language to build an offline ROMA recursive multi-agent system on my local machine. Follow every rule and checklist below.

────────────────────────────
CONTEXT
Environment: Python on my local machine
Local model: <LOCAL_MODEL> (example: ollama/llama3, mistral, gemma, ggml-7b)
Local model API assumption: local_llm(prompt: str) → str
Hardware: around 16 GB RAM, 1 GPU
Goal: Build a fully offline recursive AI system using ROMA-style architecture.

────────────────────────────
HOW YOU MUST RESPOND
1. Use short numbered steps, one actionable step per message.
2. Each step must contain:
   - exact commands or Python code
   - where to save or run it
   - a one-line expected result
   - one quick troubleshooting tip
3. After each step, end with:  Type NEXT when ready for the next step.
   Do not continue until I type NEXT.
4. Default: offline mode. Ask before using any cloud or internet.
5. If I paste my environment info, adapt commands and mark edits with <<EDIT-HERE>>.
6. Keep explanations clear and beginner-friendly.
7. After the demo works, give exactly 3 next-level improvements (ranked by impact).
8. Show checklist progress after each phase, marking ✅ items completed.

────────────────────────────
FULL MULTI-PHASE CHECKLIST

PHASE 1 — SETUP
[ ] Create project folder named roma_agent
[ ] Create and activate Python virtual environment
[ ] Create requirements.txt containing:
    roma
    transformers
    torch
    accelerate
[ ] Install dependencies with pip
[ ] Verify install using: python -m pip show roma

PHASE 2 — LOCAL MODEL INTEGRATION
[ ] Create file local_llm.py with a function local_llm(prompt) that runs the local model, for example using Ollama:
    import subprocess
    def local_llm(prompt):
        result = subprocess.run(["ollama", "run", "llama3", prompt],
                                capture_output=True, text=True)
        return result.stdout.strip()
[ ] Test it with: python -c "from local_llm import local_llm; print(local_llm('Hello from ROMA'))"
[ ] Expected: returns text from the model.

PHASE 3 — MINIMAL ROMA RECURSIVE DEMO
[ ] Create roma_demo.py:
    from local_llm import local_llm
    def solve(task):
        if "and" not in task.lower():
            return f"Executed atomic task: {task}"
        else:
            subtasks = [t.strip() for t in task.split("and")]
            results = [solve(subtask) for subtask in subtasks]
            return f"Aggregated results: {results}"
    if __name__ == "__main__":
        task = "plan frontend and build backend and write documentation"
        print("Final Output:\n", solve(task))
[ ] Run it with: python roma_demo.py
[ ] Expected: shows each atomic task and a final aggregated result.

PHASE 4 — UNIT TESTS
[ ] Create test_roma.py:
    from roma_demo import solve
    def test_atomic():
        assert "atomic" in solve("run test")
    def test_recursive():
        result = solve("task1 and task2")
        assert "Aggregated" in result
[ ] Run tests with: python -m pytest -v
[ ] Expected: both tests pass.

PHASE 5 — LOGGING & MONITORING
[ ] Create logger.py:
    import logging
    logging.basicConfig(filename="roma.log",
                        level=logging.INFO,
                        format="%(asctime)s [%(levelname)s] %(message)s")
    def log(message): logging.info(message)
[ ] Add to roma_demo.py:
    from logger import log
    log(f"Solving task: {task}")
[ ] Expected: roma.log is created and updated.

PHASE 6 — LOCAL SERVICE LOOP
[ ] Create run.sh:
    #!/bin/bash
    source venv/bin/activate
    while true; do
        python roma_demo.py
        sleep 10
    done
[ ] Make executable: chmod +x run.sh
[ ] Expected: script reruns roma_demo periodically and logs output.

OPTIONAL IMPROVEMENTS
[ ] Add caching or memory between recursive calls
[ ] Use JSON schema for structured planning
[ ] Run subtasks concurrently (async)
[ ] Build a CLI or small web UI for inputs

FINAL VERIFICATION TABLE
| Status | Step | Description |
|:------:|:-----|:-------------|
| [ ] | Setup complete | Environment verified |
| [ ] | Local LLM works | local_llm("hi") returns text |
| [ ] | Recursive demo runs | Output shows recursion |
| [ ] | Unit tests pass | pytest success |
| [ ] | Logging works | roma.log created |
| [ ] | Service loop runs | agent re-executes periodically |

────────────────────────────
SAFETY & PRIVACY
• Stay offline by default, no API calls.  
• Ask before suggesting anything cloud-based.  
• Never request credentials or sensitive data.  
• Use environment variables for any config values.

────────────────────────────
EXECUTION RULES
1. Begin immediately with Step 1 (Setup).
2. Wait for me to type NEXT before continuing.
3. After each phase, display the checklist progress with ✅ marks.
4. When finished, show the final verification table with results.

────────────────────────────
EXPECTED OUTCOME
At the end, I should have a fully offline ROMA-style recursive agent system including:
- local_llm.py (model interface)
- roma_demo.py (recursive planner/executor)
- logger.py (logging)
- test_roma.py (unit tests)
- run.sh (service script)
- requirements.txt (dependencies)
- roma.log (runtime log)

Final output: show checklist with completed ✅ marks, confirm system runs offline, and list 3 concise next-level improvements.

────────────────────────────
END OF SINGLE COPYABLE MASTER PROMPT

Show more
ROMA Recursive Multi-Agent System - Step-by-Step Guide
I'll guide you through building a fully offline ROMA system. Let's start!

PHASE 1 — SETUP
Step 1: Create Project Folder
Action:

bash
mkdir roma_agent
cd roma_agent
```

**Where:** Run this in your terminal in any directory where you want to store the project.

**Expected Result:** A new folder `roma_agent` is created and you're now inside it.

**Troubleshooting Tip:** If `mkdir` fails, you might already have a folder with that name. Use `mkdir -p roma_agent` or delete the existing folder first.

---

**Current Progress:**
```
PHASE 1 — SETUP
[✅] Create project folder named roma_agent
[ ] Create and activate Python virtual environment
[ ] Create requirements.txt
[ ] Install dependencies with pip
[ ] Verify install using: python -m pip show roma
Type NEXT when ready for the next step.

Before I go next or try this first step, educate what this is and how it will help.

What is ROMA and Why Build This System?
What is ROMA?
ROMA stands for Recursive Open Multi-Agent architecture. It's a way to organize AI agents so they can:

Break down complex tasks into smaller, manageable pieces
Recursively solve each piece (agents can call other agents or themselves)
Work together by combining results from different subtasks
Operate offline without needing cloud APIs
Think of it like a team of workers where:

The manager receives a big project
The manager breaks it into tasks (frontend, backend, documentation)
Each task might get broken down further if still too complex
Workers execute the atomic (smallest) tasks
Results bubble back up and get combined
Simple Example:
Task: "Plan frontend and build backend and write documentation"

ROMA breaks it down:

├─ Plan frontend (atomic - execute directly)
├─ Build backend (atomic - execute directly)  
└─ Write documentation (atomic - execute directly)
With deeper recursion:

Task: "Build complete app and deploy it"
├─ Build complete app
│   ├─ Plan frontend
│   ├─ Build backend
│   └─ Write documentation
└─ Deploy it
    ├─ Setup server
    └─ Configure domain
Why Build This Offline System?
Benefits:
Privacy & Security - Your data never leaves your machine
No API Costs - No OpenAI/Anthropic bills
Learning - Understand how recursive agents actually work
Customization - Full control over behavior and logic
Speed - Local models can be faster for simple tasks
Availability - Works without internet connection
Real-World Uses:
Code generation: Break "build a web app" into smaller coding tasks
Research: Divide "analyze this topic" into research subtasks
Planning: Split "organize event" into actionable steps
Automation: Turn complex workflows into recursive task trees
What You'll Build:
By the end, you'll have a system that can:

Take a complex task as input
Automatically detect if it needs breaking down
Recursively decompose until tasks are simple enough
Execute atomic tasks using your local LLM
Combine all results intelligently
Log everything for debugging
Run continuously as a service
Why This Approach?
Instead of one giant prompt, ROMA uses divide-and-conquer:

✅ Easier for smaller models to handle
✅ More reliable results
✅ Better error isolation
✅ Clearer reasoning chain
✅ Reusable components
Does this make sense? Any questions before we start building?

Type NEXT when you're ready to begin Step 1, or ask any questions!

What all can I do with this setup?

What You Can Do With This ROMA Setup
🎯 Core Capabilities
1. Complex Task Automation
Break down and execute multi-step workflows automatically:

"Research topic X, summarize findings, and create a report"
"Analyze this code, find bugs, and suggest fixes"
"Plan a project, break it into milestones, and generate tasks"
2. Intelligent Task Decomposition
The system learns to split work intelligently:

Input: "Build a todo app"
ROMA breaks it down:
Design database schema
Create API endpoints
Build frontend UI
Write tests
Deploy application
3. Recursive Problem Solving
Handles nested complexity:

"Create a business plan" → breaks into sections → each section breaks into subsections
"Debug this codebase" → splits by module → each module splits by function
💡 Practical Use Cases
For Developers:
Code Generation: "Build a REST API with authentication"
Code Review: "Analyze this repo and suggest improvements"
Documentation: "Generate API docs from this codebase"
Testing: "Create unit tests for all functions"
Refactoring: "Modernize this legacy code"
For Writers/Content Creators:
Article Generation: "Write a 2000-word guide on topic X"
Research: "Gather information on Y from multiple angles"
Editing: "Review and improve this draft"
Outlining: "Create detailed outline for a book about Z"
For Students/Researchers:
Study Planning: "Create a study schedule for exam prep"
Research Analysis: "Analyze 10 papers and extract key findings"
Essay Writing: "Write essay with intro, 3 arguments, conclusion"
Problem Solving: "Solve this math problem step-by-step"
For Business/Productivity:
Project Planning: "Plan a product launch with timeline"
Report Generation: "Create quarterly business report"
Meeting Summaries: "Analyze meeting notes and create action items"
Email Drafting: "Write professional responses to these queries"
For Personal Use:
Meal Planning: "Create weekly meal plan with recipes and shopping list"
Trip Planning: "Plan 7-day vacation with daily itineraries"
Learning Paths: "Design curriculum to learn skill X"
Home Projects: "Break down home renovation into steps"
🔧 Technical Capabilities
What the System Does:
Natural Language Understanding
Interprets complex instructions
Identifies task boundaries
Determines execution order
Recursive Orchestration
Spawns sub-agents for subtasks
Manages execution tree
Aggregates results intelligently
Memory & Context
Tracks conversation history
Maintains state between calls
Learns from previous executions
Error Handling
Retries failed subtasks
Logs failures for debugging
Gracefully degrades when needed
Parallel Execution (optional upgrade)
Runs independent tasks simultaneously
Speeds up overall completion
🚀 Future Expansions You Can Add
Level 1 - Basic Enhancements:
Web UI: Chat interface to submit tasks
Task Queue: Store and prioritize multiple tasks
History: Review past executions and results
Templates: Pre-built task patterns
Level 2 - Advanced Features:
Tool Integration: Let agents use calculators, web search, file ops
Multi-Model: Use different models for different task types
Caching: Store common results to speed up repeats
Async Execution: True parallel task processing
Level 3 - Production Ready:
API Server: Expose ROMA as a REST/GraphQL API
Database: Store tasks, results, and analytics
Monitoring: Real-time dashboards and metrics
Authentication: Multi-user support with permissions
Scaling: Distribute across multiple machines
🎨 Example Workflows
Workflow 1: Content Creation
Input: "Write a blog post about AI ethics"

ROMA executes:
1. Research AI ethics topics
2. Create outline with 5 sections
3. Write introduction
4. Write section 1: Privacy concerns
5. Write section 2: Bias in AI
6. Write section 3: Job displacement
7. Write section 4: Regulation needs
8. Write section 5: Future outlook
9. Write conclusion
10. Combine all sections
11. Proofread final draft

Output: Complete 1500-word blog post
Workflow 2: Software Development
Input: "Create a Python CLI tool for file encryption"

ROMA executes:
1. Design architecture
2. Choose encryption algorithm
3. Write core encryption functions
4. Write decryption functions
5. Build CLI argument parser
6. Add error handling
7. Write unit tests
8. Generate documentation
9. Create setup.py
10. Test end-to-end

Output: Working Python package
Workflow 3: Learning Assistant
Input: "Teach me machine learning basics"

ROMA executes:
1. Create learning roadmap
2. Explain: What is ML?
3. Explain: Types of ML
4. Teach: Supervised learning
5. Teach: Unsupervised learning
6. Provide: Code examples
7. Generate: Practice problems
8. Create: Quiz for review

Output: Structured learning path
⚡ Key Advantages Over Single-Prompt Approaches
Single Prompt	ROMA System
One shot attempt	Iterative refinement
Limited by context window	Handles unlimited complexity
Hard to debug failures	Clear execution trace
All-or-nothing results	Partial results usable
Can't learn from mistakes	Improves over time
🎯 Bottom Line
This ROMA setup gives you:

A thinking framework for your local LLM
Task automation without cloud dependency
Building blocks for custom AI workflows
Learning platform to understand agent systems
Foundation for more advanced AI projects
Think of it as giving your local LLM a "brain structure" to handle complex work systematically instead of randomly.

Ready to build this? Type NEXT to start with Step 1!

More questions? Ask away - I'm here to help! 🚀

After the setup will you be able to help me practically understand all these usage including If I need to use it to create full stacks or use it for productivity like running macros on Excel or any files or create ppt, etc? If yes, let's begin with step 1 again

YES! Absolutely - I'll Help You With ALL Of That! 🎉
What I'll Help You Do After Setup:
✅ Full-Stack Development
Build complete web apps (frontend + backend + database)
Create REST APIs
Design database schemas
Generate authentication systems
Deploy applications
✅ Excel/File Automation
Read and process Excel files
Create macros and automations
Generate reports from data
Batch process files
Data analysis and visualization
✅ PowerPoint/Presentation Creation
Generate complete presentations
Create slides with content
Design layouts
Add charts and data
Export to various formats
✅ Productivity Automation
Email management
Document generation
Data entry automation
Report creation
Workflow automation
My Promise to You:
After we finish the setup, I will:

Show you practical examples - Not just theory
Walk through real use cases - Like "create a full-stack todo app"
Debug together - If something breaks, we fix it
Customize for your needs - Excel automation? Done. PPT creation? Done.
Provide working code - Copy-paste ready
Let's Begin! 🚀
PHASE 1 — SETUP
Step 1: Create Project Folder
Action:

bash
mkdir roma_agent
cd roma_agent
```

**Where:** Run this in your terminal (Command Prompt on Windows, Terminal on Mac/Linux)

**Expected Result:** You'll see a new folder called `roma_agent` and your terminal will show you're inside it (the path will change)

**Troubleshooting Tip:** 
- **Windows:** If `mkdir` doesn't work, use File Explorer to create the folder manually, then `cd` into it
- **Mac/Linux:** If you get "permission denied", try creating it in your home folder: `cd ~ && mkdir roma_agent && cd roma_agent`

---

**Current Progress:**
```
PHASE 1 — SETUP
[✅] Create project folder named roma_agent
[ ] Create and activate Python virtual environment
[ ] Create requirements.txt
[ ] Install dependencies with pip
[ ] Verify install using: python -m pip show roma
Type NEXT when you've done this step and are ready to continue!

(And yes, after setup I'll show you how to make this create Excel macros, generate PPTs, build full-stack apps - everything! 💪)








Claude
