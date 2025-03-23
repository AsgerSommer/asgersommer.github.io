---
layout: default
title: Socials
weight: 5
---

<script type="module" src="https://cdn.jsdelivr.net/npm/bsky-embed/dist/bsky-embed.es.js" async></script>
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Center Div with Flexbox</title>
    <style>
        .parent {
            display: flex;
            justify-content: center;
            align-items: flex-start;
			height: 100vh; /* Full viewport height for demonstration */
        }
        .child {
            width: 400px;
            height: 600px;
        }
    </style>
</head>
<body>
    <div class="parent">
        <div class="child">
        		<iframe src="https://pixelfed.social/asger_sommer/embed" class="pixelfed__embed" style="max-width: 100%; border: 0" width="400" height="1600" allowfullscreen="allowfullscreen"></iframe>
        </div>
    </div>
    <bsky-embed
    username="asger-sommer.bsky.social"
    mode="dark"
    limit="5"
    link-target="_blank"
    link-image="true"
    load-more="true"
    disable-styles="false"
    custom-styles=".border-slate-300 { border-color: red; }"
    date-format='{"type":"absolute","locale":"de-DE","options":{"weekday":"long","year":"numeric","month":"long","day":"numeric"}}'>
  </bsky-embed>
</body>
<div>