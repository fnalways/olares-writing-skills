# Example transformation

A sample showing how a Chinese input becomes a polished English use case.

## Chinese input

> 我想写一个关于在 Olares 上安装使用 n8n 的教程。n8n 是一个工作流自动化工具，可以连接各种服务。版本是 1.2.3。需要先安装 Ollama，然后在 Market 安装 n8n，配置 webhook。

## English output

```markdown
---
outline: deep
description: Set up n8n on Olares for workflow automation. Connect services and build automated workflows while maintaining full data control.
head:
  - - meta
    - name: keywords
      content: Olares, n8n, workflow automation, self-hosted
app_version: "1.2.3"
doc_version: "1.0"
doc_updated: "2025-03-10"
authors: ["@your-username"]
---

# Automate workflows with n8n

n8n is an open-source workflow automation tool that connects various services and applications through visual workflows. Running n8n on Olares ensures your automation data stays under your control.

## Learning objectives

In this guide, you will learn how to:
- Install and configure n8n on Olares
- Set up webhook endpoints for external integrations
- Create your first automated workflow

## Prerequisites

- [Ollama installed](ollama.md) and running for local AI model support
- Olares admin privileges
- Basic understanding of HTTP/webhook concepts

## Install n8n

1. Open Market and search for "n8n".
2. Click **Get**, then **Install**, and wait for installation to complete.

## Configure webhook access

:::tip Enable external access
For webhooks to receive events from external services, ensure LarePass VPN is enabled on your device.
:::

[Continue with specific steps...]
```
