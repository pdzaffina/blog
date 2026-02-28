---
layout: post
title: "Run Your Own AI Stack for Budget Season: Ollama + OpenCode for Leaders"
published: true
tags:
  - AI
  - Artificial Intelligence
  - OpenCode
  - AI Agents
---
I wrote [previously](https://peter.zaffina.net/blog/Agentic-Mindshift/) about a new way of working. I'm sharing a 
method to set up a system like I described for yourself.

Budget season is one of the most document-heavy, judgment-intensive stretches of any leader's year. You're synthesizing team inputs, justifying initiative costs, making hard prioritization calls, and packaging it all into something the CFO and board will actually approve. **Ollama** and **OpenCode** give you a private, local AI assistant that can help you do all of that faster, without sensitive financial data ever leaving your machine.

![Business professional working through budget documents and planning spreadsheets on a laptop](https://images.unsplash.com/photo-1554224155-6726b3ff858f?w=1200&q=80)
*Your AI budget-season co-pilot. Runs locally, privately, with no API bill attached.*

---

## What We're Building

By the end of this guide you'll have:

- **Ollama** installed and serving a 7-14B parameter LLM on your machine
- **OpenCode** wired to Ollama and running in your terminal
- A complete budget planning package produced with the stack: initiative briefs, a cost and headcount breakdown, a prioritization framework, and an executive summary ready for leadership review

---

## Part 1: Install Ollama

[Ollama](https://ollama.com) is the cleanest way to download and run open-weight language models (Llama, Mistral, Qwen, Gemma, and many more) directly on your computer. It handles model downloads, hardware acceleration (Apple Silicon, NVIDIA CUDA, AMD ROCm), and exposes a simple REST API on `localhost:11434`.

![Ollama website homepage showing model download interface](https://images.unsplash.com/photo-1558494949-ef010cbdcc31?w=1200&q=80)
*Ollama treats models like packages: pull, run, done.*

### macOS and Windows

Head to [ollama.com](https://ollama.com) and click **Download**. Run the installer and follow the prompts. Ollama will appear in your menu bar (macOS) or system tray (Windows) and start its background service automatically.

### Linux (one-liner)

```bash
# Download and run the official install script
curl -fsSL https://ollama.com/install.sh | sh
```

The script detects your GPU drivers and configures the service automatically. After it finishes, Ollama runs as a `systemd` service and starts on every boot.

### Verify the installation

```bash
ollama --version
# Expected output: ollama version 0.x.x
```

### Pull your first model

For business knowledge work, a 7-14B parameter model strikes the best balance between speed and quality. `llama3.1:8b` is a great general-purpose starting point; `qwen2.5:14b` excels at reasoning and structured output.

```bash
# Pull the 8B Llama 3.1 model (~4.7 GB)
ollama pull llama3.1:8b

# Or pull Qwen 2.5 14B for stronger reasoning (~8.2 GB)
ollama pull qwen2.5:14b

# List what you have downloaded
ollama list
```

> **Storage note:** Models are stored in `~/.ollama/models` on macOS/Linux or `%USERPROFILE%\.ollama\models` on Windows. Make sure you have at least 10 GB free before pulling a 14B model.

### Quick sanity check

```bash
ollama run llama3.1:8b "Summarize the key benefits of agile project management in two sentences."
```

You should see a coherent two-sentence response stream into your terminal within seconds. Ollama is ready.

---

## Part 2: Install OpenCode

[OpenCode](https://opencode.ai) is a terminal-based agentic AI interface built by the SST team. Think of it as an interactive task assistant that can read and write files, run shell commands, and work through multi-step problems, all while using whichever LLM backend you point it at.

![OpenCode terminal interface showing an AI session in progress](https://images.unsplash.com/photo-1461749280684-dccba630e2f6?w=1200&q=80)
*OpenCode works inside your terminal alongside your existing workflow.*

### Prerequisites

OpenCode requires **Node.js 18+**. Check what you have and upgrade if needed:

```bash
node --version
# Should print v18.x.x or higher

# If not installed, use a version manager:
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | sh
nvm install 20
nvm use 20
```

### Install OpenCode via npm

```bash
# Install globally
npm install -g opencode-ai

# Confirm it's available
opencode --version
```

### Configure OpenCode to use Ollama

OpenCode uses a config file to know which model provider to talk to. Create or edit `~/.config/opencode/config.json`:

```json
{
  "model": "ollama/llama3.1:8b",
  "provider": {
    "ollama": {
      "url": "http://localhost:11434"
    }
  }
}
```

> **Switching models:** Change the `"model"` value to any model you've pulled with Ollama, e.g. `"ollama/qwen2.5:14b"`. No restart required.

### Launch OpenCode

```bash
# Navigate to the folder you want to work in
cd ~/my-business-project

# Start OpenCode
opencode
```

The OpenCode TUI opens in your terminal. At the top it displays which model is active. Type a message and press `Enter` to begin. OpenCode can see all files in your current directory and can read, create, and edit them on your behalf.

---

## Part 3: Apply It to Budget Season

Now for the good part. Let's use the stack to produce a full budget planning package from your raw inputs.

![A leader reviewing annual initiatives and financial projections at a desk](https://images.unsplash.com/photo-1460925895917-afdab827c52f?w=1200&q=80)

### The scenario

You're a department head going into the annual budget cycle. You have a list of next year's proposed initiatives, rough headcount and tooling costs jotted down, and a strategic priority ranking from your leadership offsite. You need to turn all of that into a formal budget proposal: initiative briefs, a consolidated cost model, a prioritization rationale, and an executive pitch the CFO and CEO will approve.

---

### Step 3a: Gather your raw inputs

Create a working directory and capture what you already know into a plain text file: rough initiative ideas, estimated costs, headcount needs, and strategic goals. It doesn't need to be polished; OpenCode will structure it.

```bash
mkdir budget-2027 && cd budget-2027

cat > raw-inputs.txt << 'EOF'
STRATEGIC GOALS FOR FY2027:
- Expand into enterprise segment
- Reduce customer churn below 5%
- Launch mobile product
- Improve internal tooling and eng velocity

PROPOSED INITIATIVES:
1. Enterprise sales motion - need 3 AEs, 1 SE, Salesforce expansion. Rough cost ~$850k
2. Customer success platform - new CSM tool + 2 CSM hires. Rough cost ~$380k
3. Mobile app (iOS + Android) - 4 engineers, 12 month effort. Rough cost ~$720k
4. Internal developer tooling overhaul - 2 eng, CI/CD investment. Rough cost ~$210k
5. Data & analytics infrastructure - 1 data engineer, new warehouse. Rough cost ~$190k

CONSTRAINTS:
- Total budget envelope likely $2.2M-$2.5M
- Must show ROI or strategic alignment for each line
- Board wants headcount growth under 15%
- Q1 spend needs to be conservative (cash position)
EOF

opencode
```

---

### Step 3b: Write individual initiative briefs

Inside OpenCode, enter this prompt:

> Read **raw-inputs.txt**. For each of the 5 proposed initiatives, write a structured one-page initiative brief saved together in **initiative-briefs.md**. Each brief should include: initiative name, strategic goal it supports, description (2-3 sentences), proposed investment (people + tools/software), expected outcomes and KPIs, key risks, and a recommended start quarter. Use a consistent heading structure for each brief.

OpenCode will read your notes and produce a full `initiative-briefs.md` with five polished briefs, each structured identically, ready to share with your leadership team or finance partner.

---

### Step 3c: Build the consolidated budget model

> Using the initiative details in **initiative-briefs.md** and the cost estimates in **raw-inputs.txt**, create a consolidated budget summary saved as **budget-model.md**. Include: a summary table showing each initiative with headcount added, tooling/software cost, total cost, and strategic priority (High/Medium/Low). Add a totals row. Then write a short narrative (150 words) explaining how the total fits within the $2.2M-$2.5M envelope and which initiatives are phased to manage Q1 cash conservatively.

> **Tip:** If you have actual numbers from finance or HR, paste them directly into the prompt to replace the rough estimates. OpenCode will recalculate and rewrite accordingly.

---

### Step 3d: Prioritization framework and trade-off analysis

This is where the AI earns its keep. Budget conversations always involve cuts. Get ahead of them:

> Based on **budget-model.md**, write a prioritization analysis saved as **prioritization.md**. Score each initiative on three dimensions: strategic alignment (1-5), estimated revenue or retention impact (1-5), and execution risk (1-5, where 5 = lowest risk). Build a weighted score. Then write a "What if we need to cut 20%?" section that recommends which initiative to defer and why, with a brief explanation of the trade-off and what we'd be giving up.

This gives you a defensible, data-backed answer the moment someone in the room asks what happens if finance only approves $2M.

---

### Step 3e: Executive pitch summary

> Write a concise executive budget pitch saved as **exec-pitch.md**, suitable for a 10-minute slot in a leadership team meeting. It should cover: the strategic context for this budget request (2 sentences), the three highest-priority initiatives and their expected impact, total investment requested and headcount delta, how Q1 will be managed conservatively, and a closing ask. Tone should be direct and confident. Target length: 400-450 words. Avoid jargon.

> **What you'll have at this point:** `raw-inputs.txt`, `initiative-briefs.md`, `budget-model.md`, `prioritization.md`, and `exec-pitch.md`. A complete budget proposal package built from scratch, in minutes, with no sensitive data sent to any external server.

---

### Step 3f: Iterate as the numbers change

Budget season is never one-and-done. OpenCode handles changes cleanly:

> Finance came back and said the total envelope is $2.1M, not $2.5M. Update **budget-model.md** with the new constraint and revise **prioritization.md** to reflect which initiative we should defer to H2 or drop entirely. Then update the totals and the Q1 phasing narrative.

> The mobile app initiative just got a sponsor from the CEO. Revise its strategic priority to High in **prioritization.md** and update its initiative brief in **initiative-briefs.md** to reflect expanded scope: tablet support included.

> Condense all four documents into a single **budget-package.md** file with a clean table of contents, suitable for sharing as a PDF with the finance team.

---

## Tips for Great Results

### Use a larger model for synthesis tasks

If your machine has 16 GB of RAM, switch to `qwen2.5:14b` or `llama3.1:70b-q4` (quantized) for the writing and analysis steps. Smaller models are fast for iteration; larger models produce noticeably sharper reasoning, more consistent document structure, and better handling of numerical trade-off logic.

### Give OpenCode a finance-savvy system persona

Add a `systemPrompt` key to your config so every session starts with the right lens:

```json
{
  "model": "ollama/qwen2.5:14b",
  "systemPrompt": "You are a senior finance and strategy advisor helping a department leader build an annual budget proposal. Be direct, structured, and evidence-based. Always quantify trade-offs where possible. Use clear headings and tables in long documents.",
  "provider": {
    "ollama": {
      "url": "http://localhost:11434"
    }
  }
}
```

### Keep your numbers in a separate source-of-truth file

Rather than embedding cost figures in your prompts, keep a `numbers.txt` file with your latest estimates and headcount figures. Tell OpenCode to read it before any calculations. When finance revises a number, you update one file, not five documents.

### Keep Ollama running in the background

On Linux, enable the systemd service so Ollama starts on boot and is always ready when you open OpenCode:

```bash
sudo systemctl enable --now ollama
```

### What tasks work best in budget season?

The Ollama + OpenCode stack is especially strong at drafting structured business documents from bullet-point notes, building consistent formats across multiple initiative briefs, generating trade-off narratives, and rapidly reformatting content for different audiences (finance vs. board vs. your team). For tasks requiring live data pulls from your ERP or financial system, you'll still need to export and paste in the numbers manually. The reasoning and writing around those numbers is where the AI shines.

---

## Wrapping Up

Budget season doesn't have to mean late nights staring at a blank doc. With Ollama and OpenCode, you can go from rough initiative notes to a full, defensible budget package in an afternoon and revise it in minutes when the numbers inevitably change.

Start with the 8B model for speed, upgrade to 14B when you need sharper reasoning on the prioritization and trade-off sections, and keep your raw inputs file updated so OpenCode always has the latest ground truth to work from.

---

*Resources: [ollama.com](https://ollama.com) · [opencode.ai](https://opencode.ai) · [github.com/sst/opencode](https://github.com/sst/opencode) · [ollama.com/library](https://ollama.com/library)*
