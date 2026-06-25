---
layout: 	post
title:  	"Using Mistral AI in VS Code"
date:   	2026-01-31
published:	true
tags:		[ai, llm, mistral, vs code]
comments:   true
---

1. First install the [CLine Extension](https://marketplace.visualstudio.com/items?itemName=saoudrizwan.claude-dev) in VS Code. 
2. Create a Mistral AI API key in the [Workspace API keys settings](https://console.mistral.ai/home?workspace_dialog=apiKeys) (not in the [Codestral page](https://console.mistral.ai/codestral), as those API keys are not the same)
3. Use the following API configuration in the CLine Extension settings:
```
API Provider: Mistral
Mistral API key: <the API key from above>
Model: devstral-2512 (for example)
```
4. Go.