# Hermes — Personal AI Assistant Experiment

> Ongoing experimentation with persistent AI assistant workflows, skill-based automation and operational AI tooling.

---

# Overview

This project is a hands-on exploration of how a persistent AI assistant can support practical everyday workflows through structured skills, memory, automation and integrations.

The assistant runs on a self-hosted VPS using Hermes Agent with Anthropic Claude as the underlying model. Interaction happens primarily through Telegram, allowing the assistant to be available continuously without a dedicated frontend.

The project is not intended as a commercial product. Its primary purpose is to better understand:

* Persistent AI workflows
* Agent-based interaction patterns
* AI-assisted automation
* Workflow orchestration
* Practical operational considerations for self-hosted AI systems

---

# Project Goal

The goal is to explore how a persistent AI assistant can:

* Reduce friction in recurring workflows
* Structure and retrieve context over time
* Integrate with external tools and APIs
* Support lightweight automation tasks
* Operate reliably on modest infrastructure

The project is treated primarily as a workflow and product exploration exercise rather than a traditional software engineering project.

---

# High-Level Architecture

```text
Telegram
   ↓
Hermes Agent (VPS-hosted)
   ↓
Claude API
   ↓
Skills / Workflows / Integrations
```

Key design principles:

* One persistent assistant rather than multiple standalone bots
* Skill-based workflows for structured task handling
* Persistent memory and context over isolated prompting
* Read-only integrations by default unless explicitly expanded

---

# VPS & Runtime Setup

The assistant runs continuously on a self-hosted Linux VPS using container-based deployment.

The VPS setup is primarily used to:

* Keep workflows available continuously
* Separate experiments from local devices
* Better understand operational aspects of persistent AI systems
* Explore lightweight self-hosted infrastructure patterns

Current experimentation includes:

* Persistent runtime configuration
* Skill-based workflow organization
* Scheduled automation tasks
* Telegram-based interaction workflows
* API and MCP integration exploration

---

# Skill-Based Workflow Structure

Skills are the primary mechanism for extending the assistant's capabilities.

Each skill defines:

* When it should activate
* What it should produce
* Constraints and formatting rules
* Workflow-specific instructions

Example structure:

```text
~/.hermes/skills/
└── productivity/
    └── meal-planner/
        └── SKILL.md
```

The current focus is less about building large autonomous systems and more about understanding how smaller, focused skills can improve workflow reliability and reduce repetitive prompting.

---

# Telegram Interaction Model

Telegram was chosen as the primary interface because it:

* Requires no custom frontend
* Supports lightweight interaction workflows
* Makes the assistant accessible across devices
* Enables rapid iteration of conversational workflows

Current interaction patterns include:

* Conversational task execution
* Skill-triggered workflows
* Lightweight automation commands
* Context-aware assistant interactions

---

# API & MCP Exploration

The project also explores lightweight integrations through APIs and MCP-compatible workflows.

Areas currently being explored include:

* External data retrieval
* Task and workflow integrations
* Context-aware summaries
* AI-assisted information filtering
* Persistent workflow orchestration

The primary interest is not raw data access itself, but how AI assistants can transform fragmented information into usable workflow support.

---

# Operational Considerations

One of the more interesting learnings from the project is that persistent AI workflows quickly become operational systems rather than simple chatbot experiments.

Even relatively small setups introduce considerations around:

* Reliability
* Context persistence
* Workflow organization
* Runtime management
* Integration boundaries
* Cost vs. capability tradeoffs

This has made the project particularly valuable as a practical learning exercise in operational AI thinking.

---

# Selected Screenshots

Example screenshots are available in the `/screenshots/hermes` directory.

Included examples currently cover:

* Skill architecture overview
* VPS runtime overview
* Telegram-based interaction workflows

---

# Key Learnings

## Persistent memory matters more than expected

One recurring observation is that workflow quality often depends more on context structure and memory handling than on raw model capability alone.

---

## AI-assisted development improves workflow iteration

Modern AI tooling makes it significantly easier to prototype workflows, validate ideas and structure product concepts before investing heavily in implementation.

This has been especially useful for:

* Workflow experimentation
* Skill design
* Rapid iteration
* Operational prototyping
* Exploring integration patterns

---

## Small focused workflows outperform generic prompting

Smaller, structured skills tend to produce more reliable and repeatable outputs than broad generic prompts.

The combination of:

* Persistent context
* Focused skills
* Lightweight integrations

appears significantly more useful than treating the assistant as a standalone chatbot.

---

## Adoption is primarily a product problem

One of the most important observations so far is that successful AI-assisted workflows depend less on technical capability and more on usability and friction.

The key questions are:

* Does the workflow save time?
* Is the interaction model intuitive?
* Is the assistant reliable enough to trust?
* Does the workflow fit naturally into existing habits?

This has reinforced the idea that persistent AI systems are as much a product and workflow design problem as a technical one.

---

*This project is built and iterated on as a personal learning exercise focused on AI-assisted workflows and operational experimentation.*
