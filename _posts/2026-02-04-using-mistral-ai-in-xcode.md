---
layout: 	post
title:  	"Using Mistral AI in Xcode"
date:   	2026-02-04
published:	true
tags:		[ai, llm, mistral, xcode]
comments:   true
---

1. Create a Mistral AI API key in the [Workspace API keys settings](https://console.mistral.ai/home?workspace_dialog=apiKeys) (not in the [Codestral page](https://console.mistral.ai/codestral), as those API keys are not the same)
2. Open Xcode, then go to Settings > Intelligence > "Add a Model Provider"
3. Use the following Model Provider configuration:
```
API key: <the API key from above>
API key header: <empty>
```
4. Then select a model, e.g. codestral or devstral.