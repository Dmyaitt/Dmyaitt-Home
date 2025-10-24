# n8n Workflow Development with Claude Code

This project is configured for building production-ready n8n workflows using Claude Code with the n8n-mcp MCP server and 7 expert skills.

## 🎯 What's Configured

### MCP Server: n8n-mcp
- **41 n8n tools** for workflow management, execution, and documentation
- **525+ nodes** searchable and documented
- **2,653+ workflow templates** for examples
- **Full API integration** with your n8n instance at https://dmyaitt.app.n8n.cloud

### Expert Skills (7 total)
1. **n8n-expression-syntax** - Master {{}} expression syntax
2. **n8n-mcp-tools-expert** ⭐ - Learn correct MCP tool usage (HIGHEST PRIORITY)
3. **n8n-workflow-patterns** - Apply 5 proven architectural patterns
4. **n8n-validation-expert** - Fix validation errors efficiently
5. **n8n-node-configuration** - Configure nodes correctly
6. **n8n-code-javascript** - Write effective Code node JavaScript
7. **n8n-code-python** - Use Python Code nodes properly

**Skills work seamlessly with n8n-mcp** to provide expert guidance throughout the workflow building process!

## 🚀 How to Work with n8n

### Building Workflows

**Skills automatically activate** based on your queries:

```
"Build a webhook to Slack workflow"
→ n8n-workflow-patterns identifies the pattern
→ n8n-mcp-tools-expert searches for nodes
→ n8n-node-configuration guides setup
→ n8n-code-javascript helps with data processing
→ n8n-expression-syntax assists with data mapping
→ n8n-validation-expert validates the result
```

### Available Capabilities

**Workflow Management:**
- Create, read, update, delete workflows
- List and search workflows
- Activate/deactivate workflows
- Import/export workflows

**Execution Management:**
- Execute workflows manually or with parameters
- Monitor running executions
- View execution history and logs
- Retry failed executions

**Node Documentation:**
- Search 525+ available n8n nodes
- Get detailed node configuration info
- Browse nodes by category or functionality
- View real examples from templates

**Code Development:**
- Write JavaScript Code nodes (recommended for 95% of use cases)
- Write Python Code nodes (when standard library is sufficient)
- Access webhook data correctly (`$json.body` in expressions, `$input.first().json.body` in Code)
- Use built-in functions ($helpers, DateTime, $jmespath)

## 💡 Common Tasks

### 1. Search for Nodes
```
"Find me a Slack node"
"Search for nodes that can send emails"
"What nodes work with Google Sheets?"
```

### 2. Build Workflows
```
"Build a webhook that receives data and sends it to Slack"
"Create a scheduled workflow that backs up database data"
"Design an AI agent workflow for customer support"
```

### 3. Write Code
```
"How do I access webhook data in a Code node?"
"Write JavaScript to transform this API response"
"Can I use pandas in a Python Code node?" (Answer: No, use JavaScript)
```

### 4. Fix Errors
```
"Why is my expression {{$json.data}} not working?"
"This validation error says 'required property missing'"
"My webhook workflow isn't receiving the body data"
```

### 5. Get Examples
```
"Show me a webhook processing pattern"
"What's the best way to handle HTTP API calls?"
"Give me an example of a database backup workflow"
```

## 🔑 Key Concepts

### Critical Gotchas (Avoid Common Mistakes!)

1. **Webhook Data Location:**
   - ❌ `{{$json}}` - This is the wrapper object
   - ✅ `{{$json.body}}` - This is your actual webhook data
   - ✅ Code node: `$input.first().json.body`

2. **Code Node Return Format:**
   - ❌ `return data;`
   - ✅ `return [{json: data}];`

3. **Expression vs Code Node:**
   - Use expressions for **simple data mapping**
   - Use Code nodes for **complex logic, loops, conditions**

4. **Python Limitations:**
   - ❌ No external libraries (requests, pandas, numpy)
   - ✅ Standard library only (json, datetime, re, etc.)
   - 💡 Use JavaScript for 95% of use cases

5. **Node Type Format:**
   - In `get_node_info`: Use `n8n-nodes-base.slack`
   - In `search_nodes`: Use `@n8n/n8n-nodes-base.Slack`
   - MCP tools will guide you on the correct format

### Validation Profiles

When validating workflows, choose the right profile:

- **minimal** - Quick check, catches major errors only
- **runtime** - Standard validation (recommended for development)
- **ai-friendly** - Allows placeholders and incomplete configs
- **strict** - Full validation for production workflows

### Workflow Patterns

Use proven patterns from 2,653+ real templates:

1. **Webhook Processing** - Receive and process incoming data
2. **HTTP API Integration** - Connect to external services
3. **Database Operations** - CRUD operations with databases
4. **AI Agent Workflows** - Build AI-powered automations
5. **Scheduled Tasks** - Cron-based recurring workflows

## 📚 Documentation

Detailed guides are available in this repository:

- **MCP_CONFIGURATION_GUIDE.md** - Complete MCP setup and troubleshooting
- **README_MCP_SETUP.md** - Environment overview and status
- **N8N_SKILLS_INSTALLATION.md** - Skills documentation and usage
- **MCP_SETUP.md** - Original setup notes

## 🔧 Configuration

### Local Setup (For Team Members)

If you're setting up this project locally:

1. **Install MCP Server:**
   ```bash
   npm install -g n8n-mcp better-sqlite3
   ```

2. **Configure Your API Key:**
   ```bash
   cp .mcp.json.example .mcp.json
   # Edit .mcp.json with your n8n API key
   ```

3. **Install Skills:**
   ```bash
   cp -r .claude/skills/* ~/.claude/skills/
   ```

4. **Restart Claude Code** - MCP server will start automatically

### Tips

- **Local n8n:** Use `http://localhost:5678` as `N8N_API_URL`
- **API Credentials Optional:** Without them, you get documentation and validation tools only
- **With API Credentials:** You get full workflow management capabilities
- **Scope Settings:**
  - `--scope local` (default): Keep API credentials private
  - `--scope project`: Share configuration with team (use environment variables for credentials)
- **Auto-start:** Claude Code automatically starts the MCP server when you begin a conversation

### Environment Variables (Alternative to .mcp.json)

Instead of storing credentials in `.mcp.json`:

```bash
# Add to ~/.bashrc or ~/.zshrc
export N8N_API_URL=https://your-instance.app.n8n.cloud
export N8N_API_KEY=your_api_key_here
```

## 🎓 Learning Resources

### Expression Syntax
```javascript
// Access current item data
{{$json.fieldName}}

// Access webhook body
{{$json.body.fieldName}}

// Access previous node data
{{$node["Node Name"].json.fieldName}}

// Use built-in variables
{{$now}} - Current timestamp
{{$env.VARIABLE}} - Environment variable
```

### Code Node Patterns
```javascript
// Access all input items
const items = $input.all();

// Access first item
const item = $input.first();

// Access webhook data
const webhookData = $input.first().json.body;

// Return properly formatted data
return items.map(item => ({
  json: {
    processedField: item.json.originalField.toUpperCase()
  }
}));
```

### HTTP Request Helper
```javascript
// Make HTTP requests in Code nodes
const response = await $helpers.httpRequest({
  method: 'GET',
  url: 'https://api.example.com/data',
  headers: {
    'Authorization': 'Bearer token123'
  }
});

return [{json: response}];
```

## 🚨 Common Issues & Solutions

### "Webhook data is undefined"
- ✅ **Solution:** Use `$json.body` instead of `$json`

### "Validation fails with 'required property missing'"
- ✅ **Solution:** Use `ai-friendly` profile during development, or check node configuration dependencies

### "Python Code node: 'requests' module not found"
- ✅ **Solution:** Use JavaScript Code node instead, or use standard library only

### "Expression {{$json.data.field}} returns null"
- ✅ **Solution:** Check webhook data structure, use `{{$json.body.data.field}}`

### "MCP tools not available"
- ✅ **Solution:** Restart Claude Code to load the MCP server

## 🤝 Contributing

When adding new workflows or patterns to this project:

1. **Validate before committing** - Use `n8n-validation-expert` skill
2. **Document patterns** - If you create a new pattern, document it
3. **Test thoroughly** - Test with actual n8n instance
4. **Follow conventions** - Use the skills' guidance for consistency

## 📊 Project Stats

- **MCP Server:** n8n-mcp v2.21.1
- **Tools Available:** 41 n8n workflow tools
- **Skills Installed:** 7 expert skills (501KB)
- **Nodes Supported:** 525+
- **Template Examples:** 2,653+
- **Code Patterns:** 10 production-tested patterns
- **Documentation Lines:** 22,000+ lines of expert guidance

## 🎯 Success Criteria

You'll know the environment is working correctly when:

- ✅ Skills auto-activate based on your queries
- ✅ You can search for and find n8n nodes
- ✅ You can create and validate workflows
- ✅ You can access your n8n instance via API
- ✅ Code suggestions follow n8n best practices
- ✅ Validation errors are caught and explained clearly

## 🔗 Related

- **n8n Instance:** https://dmyaitt.app.n8n.cloud
- **n8n-mcp GitHub:** https://github.com/czlonkowski/n8n-mcp
- **n8n-skills GitHub:** https://github.com/czlonkowski/n8n-skills
- **n8n Documentation:** https://docs.n8n.io

---

**Ready to build flawless n8n workflows?** Just start asking questions and the skills will guide you!
