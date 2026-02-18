---
title: "What is Kiro and How to Use It"
description: "A comprehensive guide to Kiro CLI - AWS's AI-powered command-line assistant that helps with development, infrastructure, and more"
publishDate: "18 Feb 2026"
tags: ["ai", "cli", "aws", "tools", "productivity"]
coverImage:
  src: "./cover.png"
  alt: "Kiro CLI - AI-powered terminal assistant"
---

## Introduction to Kiro CLI

Kiro is an AI-powered command-line assistant built by Amazon Web Services (AWS) that brings the power of large language models directly to your terminal. It's designed to help developers with coding, infrastructure management, AWS operations, and general productivity tasks.

## What Makes Kiro Special?

Unlike traditional CLI tools, Kiro combines:

- **Conversational AI** - Natural language interaction with Claude and other LLMs
- **Code Intelligence** - LSP integration for semantic code understanding
- **File Operations** - Read, write, and modify files with AI assistance
- **AWS Integration** - Native AWS CLI operations with intelligent suggestions
- **Extensibility** - MCP (Model Context Protocol) server support for custom tools

## Getting Started

### Installation

First, install Kiro CLI (requires AWS Builder ID or Identity Center):

```bash
# Installation instructions vary by platform
# Check official AWS documentation for latest method
```

### Authentication

```bash
kiro-cli login
```

This opens your browser to authenticate with AWS Builder ID or Identity Center.

### Starting a Chat Session

```bash
kiro-cli chat
```

You're now in an interactive session where you can ask questions, request code changes, or get help with tasks.

## Key Features

### 1. Code Intelligence

Initialize LSP for your project:

```bash
/code init
```

This enables semantic code understanding, symbol search, and intelligent refactoring across TypeScript, Python, Rust, Go, Java, Ruby, and C/C++.

### 2. File References

Include files in your conversation using the `@` syntax:

```
Can you review @src/components/Header.tsx and suggest improvements?
```

### 3. Agent System

Switch between specialized agents for different tasks:

```bash
/agent          # List and switch agents
/plan           # Switch to planning agent
/help           # Switch to help agent
```

### 4. Model Selection

Choose your preferred AI model:

```bash
/model          # Interactive model selection
```

### 5. Session Management

Save and resume conversations:

```bash
/chat save my-session
/chat load my-session
/chat list
```

## Common Use Cases

### Code Review and Refactoring

```
Review the authentication logic in @src/auth/ and suggest security improvements
```

### Infrastructure as Code

```
Help me write a Terraform configuration for an AWS Lambda function with API Gateway
```

### Debugging

```
I'm getting this error: [paste error]. Here's the relevant code: @src/utils/api.ts
```

### AWS Operations

Kiro can execute AWS CLI commands with intelligent suggestions:

```
List all my EC2 instances in us-east-1 and show their status
```

## Advanced Features

### MCP Servers

Extend Kiro with Model Context Protocol servers:

```bash
kiro-cli mcp add <server-name>
/mcp            # View loaded servers
```

### Knowledge Base

Store information across sessions:

```bash
/experiment     # Enable knowledge feature
/knowledge add "Project uses React 18 with TypeScript"
/knowledge search "React"
```

### Tangent Mode

Explore side topics without disrupting your main conversation:

```bash
/experiment     # Enable tangent mode
# Press configured key (default: Ctrl+T) to branch conversation
```

## Tips and Best Practices

1. **Be Specific** - Provide context and file references for better results
2. **Use Code Intelligence** - Initialize LSP for semantic understanding
3. **Save Sessions** - Don't lose important conversations
4. **Experiment with Agents** - Different agents excel at different tasks
5. **Trust Gradually** - Review tool permissions with `/tools`

## Useful Commands

| Command | Description |
| ------- | ----------- |
| `/help` | Get help about Kiro features |
| `/tools` | View and manage tool permissions |
| `/context` | View context window usage |
| `/clear` | Clear conversation history |
| `/quit` | Exit Kiro |

## Configuration

Customize Kiro behavior:

```bash
kiro-cli settings list                          # View all settings
kiro-cli settings set chat.defaultModel claude  # Set default model
kiro-cli settings set chat.enableThinking true  # Enable thinking mode
```

## Conclusion

Kiro CLI transforms how developers interact with AI assistance. By bringing conversational AI directly to your terminal with deep integration into your development workflow, it becomes an indispensable tool for modern software development.

Whether you're writing code, managing infrastructure, or debugging issues, Kiro is there to help - right where you work.

## Learn More

- Run `/help` in Kiro for interactive documentation
- Check `/changelog` for latest features
- Use `/experiment` to try beta features
- Visit [kiro.dev](https://kiro.dev) for official documentation

---

*This post was written with assistance from Kiro CLI itself - a meta example of its capabilities!*
