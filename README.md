# K8s AI Troubleshooting Agent - Hackathon Project

An AI-powered agent that connects to Kubernetes via MCP to diagnose and troubleshoot application issues.

## 🎯 Project Status

### Completed ✅
- Docker Desktop Kubernetes cluster running
- WordPress + MySQL deployed in `wordpress` namespace
- MCP K8s server tested (`@strowk/mcp-k8s`)

### Next Steps 🚧
- [ ] Build Python AI agent with LLM integration
- [ ] Create "broken" test scenarios for demo
- [ ] End-to-end troubleshooting tests

---

## 📦 What's Running

### Kubernetes Cluster
```bash
# Check cluster status
kubectl get nodes

# Check WordPress deployment
kubectl get pods -n wordpress
kubectl get svc -n wordpress
```

### WordPress Access
- **URL**: http://localhost:30080
- Or port-forward: `kubectl port-forward svc/wordpress 8080:80 -n wordpress`

---

## 🔧 MCP K8s Server

### Run the MCP Server
```bash
npx @strowk/mcp-k8s
```

### Test with Inspector (Web UI)
```bash
npx @modelcontextprotocol/inspector npx @strowk/mcp-k8s
# Opens at http://localhost:5173
```

### Available MCP Tools
| Tool | Description |
|------|-------------|
| `list-k8s-contexts` | List K8s cluster contexts |
| `list-k8s-namespaces` | List namespaces |
| `list-k8s-nodes` | List cluster nodes |
| `get-k8s-pod-logs` | Get container logs |
| `k8s-resource-get` | Get any K8s resource |

---

## 🏗️ Architecture

```
┌─────────────────────┐     MCP (stdio)      ┌──────────────────┐
│  Python AI Agent    │ ◄──────────────────► │  mcp-k8s-go      │
│  (LLM + Logic)      │                      │  MCP Server      │
└─────────────────────┘                      └────────┬─────────┘
                                                      │ kubectl
                                                      ▼
                                             ┌──────────────────┐
                                             │  Kubernetes      │
                                             │  - WordPress     │
                                             │  - MySQL         │
                                             └──────────────────┘
```

---

## 🔜 Building the AI Agent (Next Session)

### Requirements
- Python 3.11+
- LLM API key (choose one):
  - OpenAI (GPT-4)
  - Anthropic (Claude)
  - Google (Gemini)

### Agent Will:
1. Connect to MCP K8s server
2. Receive troubleshooting questions from user
3. Use MCP tools to gather K8s data (pods, logs, events)
4. Send data to LLM for analysis
5. Return diagnosis + remediation steps

---

## 📁 Project Files

```
/Users/stefanhartescu/Repos/Hackathon/
├── kustomization.yaml      # K8s manifest orchestration
├── namespace.yaml          # wordpress namespace
├── mysql-secret.yaml       # Database credentials
├── mysql-deployment.yaml   # MySQL pod + service
├── wordpress-deployment.yaml # WordPress pod + service
└── README.md               # This file
```

---

## 💡 To Resume in New Conversation

Say: *"I'm building a K8s AI troubleshooting agent. Read the README.md in my Hackathon folder for context. Let's continue building the Python agent."*

Then provide:
1. Which LLM you want to use (OpenAI/Anthropic/Google)
2. That you have an API key ready
