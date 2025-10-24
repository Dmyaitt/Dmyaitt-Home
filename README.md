# Dmyaitt-Home

Personal development workspace configured for building production-ready n8n workflows with Claude Code.

## 🎯 Quick Start

**New to this project?** Read **[CLAUDE.md](./CLAUDE.md)** for complete instructions on working with n8n workflows.

## 🚀 What's Configured

This workspace includes:

### n8n-mcp MCP Server
- **41 n8n workflow tools** for complete workflow lifecycle management
- **525+ searchable nodes** with detailed documentation
- **2,653+ workflow templates** for examples and patterns
- **Full API integration** with n8n instance

### 7 Expert Skills
1. **n8n-expression-syntax** - Master {{}} expression syntax
2. **n8n-mcp-tools-expert** ⭐ - Learn correct MCP tool usage
3. **n8n-workflow-patterns** - Apply 5 proven architectural patterns
4. **n8n-validation-expert** - Fix validation errors efficiently
5. **n8n-node-configuration** - Configure nodes correctly
6. **n8n-code-javascript** - Write effective Code node JavaScript
7. **n8n-code-python** - Use Python Code nodes properly

**Skills work seamlessly with n8n-mcp** to provide expert guidance throughout the workflow building process!

## 📚 Documentation

- **[CLAUDE.md](./CLAUDE.md)** - 🎯 **START HERE** - Main project instructions
- **[MCP_CONFIGURATION_GUIDE.md](./MCP_CONFIGURATION_GUIDE.md)** - Complete MCP setup guide
- **[N8N_SKILLS_INSTALLATION.md](./N8N_SKILLS_INSTALLATION.md)** - Skills documentation
- **[README_MCP_SETUP.md](./README_MCP_SETUP.md)** - Environment summary
- **[MCP_SETUP.md](./MCP_SETUP.md)** - Original setup notes

## 🔧 Setup for Team Members

If you're cloning this repository:

```bash
# 1. Install MCP server
npm install -g n8n-mcp better-sqlite3

# 2. Configure your n8n API key
cp .mcp.json.example .mcp.json
# Edit .mcp.json with your API key from your n8n instance

# 3. Install skills
cp -r .claude/skills/* ~/.claude/skills/

# 4. Restart Claude Code
# MCP server will start automatically when you begin a conversation
```

See [MCP_CONFIGURATION_GUIDE.md](./MCP_CONFIGURATION_GUIDE.md) for detailed setup instructions.

## 💡 Usage Examples

### Build a Workflow
```
"Build a webhook that receives data and sends it to Slack"
"Create a scheduled workflow that backs up database data"
```

### Search for Nodes
```
"Find me a Slack node"
"What nodes can send emails?"
```

### Write Code
```
"How do I access webhook data in a Code node?"
"Write JavaScript to transform this API response"
```

### Fix Errors
```
"Why is my expression {{$json.data}} not working?"
"This validation error says 'required property missing'"
```

## 🔑 Key Tips

- **Webhook data:** Access via `{{$json.body}}` not `{{$json}}`
- **Code node returns:** Must be `[{json: data}]` format
- **Python limitations:** No external libraries - use JavaScript for 95% of use cases
- **Local n8n:** Use `http://localhost:5678` as `N8N_API_URL`
- **Auto-start:** Claude Code automatically starts MCP server on conversation start

## 📊 Environment Stats

- **MCP Tools:** 41 n8n workflow management tools
- **Expert Skills:** 7 skills (501KB total)
- **Nodes Supported:** 525+
- **Template Examples:** 2,653+
- **Documentation:** 22,000+ lines of expert guidance

## 🤝 Contributing

When adding workflows or patterns:

1. Validate before committing (use `n8n-validation-expert` skill)
2. Document new patterns if you create them
3. Test with actual n8n instance
4. Follow the skills' guidance for consistency

## 🔗 Links

- **n8n-mcp:** https://github.com/czlonkowski/n8n-mcp
- **n8n-skills:** https://github.com/czlonkowski/n8n-skills
- **n8n Documentation:** https://docs.n8n.io

## 📝 License

MIT

---

**Ready to build workflows?** Open [CLAUDE.md](./CLAUDE.md) and start asking questions!
