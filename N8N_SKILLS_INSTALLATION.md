# n8n Skills Installation

## ✅ Installed Successfully

7 expert Claude Code skills for building n8n workflows have been installed.

## 📦 Installed Skills

### 1. **n8n-expression-syntax**
- **Purpose:** Validate n8n expression syntax and fix common errors
- **Activates when:** Writing n8n expressions, using {{}} syntax, accessing $json/$node variables
- **Key Features:**
  - Core variables ($json, $node, $now, $env)
  - Critical gotcha: Webhook data is under `$json.body`
  - Common mistakes catalog with fixes

### 2. **n8n-mcp-tools-expert** ⭐ (HIGHEST PRIORITY)
- **Purpose:** Expert guide for using n8n-mcp MCP tools effectively
- **Activates when:** Searching for nodes, validating configurations, accessing templates
- **Key Features:**
  - Tool selection guide (which tool for which task)
  - nodeType format differences (nodes-base.* vs n8n-nodes-base.*)
  - Validation profiles (minimal/runtime/ai-friendly/strict)
  - Smart parameters and auto-sanitization

### 3. **n8n-workflow-patterns**
- **Purpose:** Proven workflow architectural patterns
- **Activates when:** Building new workflows, designing workflow structure
- **Key Features:**
  - 5 proven patterns (webhook processing, HTTP API, database, AI, scheduled)
  - Workflow creation checklist
  - Real examples from 2,653+ n8n templates
  - Connection best practices

### 4. **n8n-validation-expert**
- **Purpose:** Interpret validation errors and guide fixing
- **Activates when:** Validation fails, debugging workflow errors
- **Key Features:**
  - Validation loop workflow
  - Real error catalog
  - Auto-sanitization behavior
  - False positives guide

### 5. **n8n-node-configuration**
- **Purpose:** Operation-aware node configuration guidance
- **Activates when:** Configuring nodes, understanding property dependencies
- **Key Features:**
  - Property dependency rules (e.g., sendBody → contentType)
  - Operation-specific requirements
  - AI connection types (8 types for AI Agent workflows)
  - Common configuration patterns

### 6. **n8n-code-javascript**
- **Purpose:** Write effective JavaScript code in n8n Code nodes
- **Activates when:** Writing JavaScript in Code nodes, troubleshooting errors
- **Key Features:**
  - Data access patterns ($input.all(), $input.first(), $input.item)
  - Critical gotcha: Webhook data under `$json.body`
  - Correct return format: `[{json: {...}}]`
  - Built-in functions ($helpers.httpRequest(), DateTime)
  - Top 5 error patterns with solutions (62%+ of failures)

### 7. **n8n-code-python**
- **Purpose:** Write Python code in n8n Code nodes
- **Activates when:** Writing Python in Code nodes, need to know limitations
- **Key Features:**
  - Important: Use JavaScript for 95% of use cases
  - Python data access (_input, _json, _node)
  - Critical limitation: No external libraries (requests, pandas, numpy)
  - Standard library reference
  - Workarounds for missing libraries

## 📍 Installation Locations

### User-Level (Active in ALL sessions)
```
~/.claude/skills/
├── n8n-code-javascript/
├── n8n-code-python/
├── n8n-expression-syntax/
├── n8n-mcp-tools-expert/
├── n8n-node-configuration/
├── n8n-validation-expert/
└── n8n-workflow-patterns/

Total: 501K (7 skills)
```

### Project-Level (Version controlled)
```
.claude/skills/
├── n8n-code-javascript/
├── n8n-code-python/
├── n8n-expression-syntax/
├── n8n-mcp-tools-expert/
├── n8n-node-configuration/
├── n8n-validation-expert/
└── n8n-workflow-patterns/
```

## 🎯 How Skills Work

Skills activate **automatically** based on your queries:

```
"How do I write n8n expressions?"
→ Activates: n8n-expression-syntax

"Find me a Slack node"
→ Activates: n8n-mcp-tools-expert

"Build a webhook workflow"
→ Activates: n8n-workflow-patterns

"Why is validation failing?"
→ Activates: n8n-validation-expert

"How do I configure the HTTP Request node?"
→ Activates: n8n-node-configuration

"How do I access webhook data in a Code node?"
→ Activates: n8n-code-javascript

"Can I use pandas in Python Code node?"
→ Activates: n8n-code-python
```

## 🤝 Skills Work Together

When you ask: **"Build and validate a webhook to Slack workflow"**

1. **n8n-workflow-patterns** identifies webhook processing pattern
2. **n8n-mcp-tools-expert** searches for webhook and Slack nodes
3. **n8n-node-configuration** guides node setup
4. **n8n-code-javascript** helps process webhook data with proper .body access
5. **n8n-expression-syntax** helps with data mapping in other nodes
6. **n8n-validation-expert** validates the final workflow

All skills compose seamlessly!

## ✨ Key Benefits

- ✅ **Correct MCP tool usage** - No more guessing which tool to use
- ✅ **Avoid validation loops** - Understand and fix errors quickly
- ✅ **Proven patterns** - Build workflows based on 2,653+ real examples
- ✅ **Expression mastery** - Get the {{}} syntax right every time
- ✅ **Code node expertise** - Avoid the top 62% of common errors
- ✅ **Python awareness** - Know when to use JavaScript instead

## 🚀 Next Steps

**Skills are now active!** No restart required. Just start asking questions about n8n workflows and the relevant skills will automatically activate.

Try asking:
- "Show me how to build a webhook workflow"
- "How do I search for a Slack node?"
- "What's the correct way to access webhook data in expressions?"
- "Help me fix this validation error: [paste error]"

## 📚 Source

**Repository:** https://github.com/czlonkowski/n8n-skills
**Author:** Romuald Członkowski (www.aiadvisors.pl/en)
**License:** MIT
**Part of:** n8n-mcp project ecosystem

## 🔗 Related

- **n8n MCP Server:** See `MCP_CONFIGURATION_GUIDE.md`
- **n8n API:** https://dmyaitt.app.n8n.cloud
- **n8n Documentation:** https://docs.n8n.io

## 📊 What's Included

- **7** complementary skills that work together
- **525+** n8n nodes supported
- **2,653+** workflow templates for examples
- **10** production-tested Code node patterns
- **Comprehensive** error catalogs and troubleshooting guides

---

**Installed on:** October 24, 2025
**Skills Version:** Latest from GitHub main branch
