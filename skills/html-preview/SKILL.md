---
name: html-preview
description: Renders any markdown document as styled HTML and opens it in the browser. Useful for previewing documents, briefings, or any content before sharing.
triggers:
  - "preview"
  - "show me"
  - "render"
  - "open in browser"
---

# HTML Preview Skill

Takes a markdown file (or inline markdown content) and renders it as a styled HTML page, then opens it in the default browser via a temporary file.

## When to Use

Use whenever you want to see a formatted preview of a document — briefings, plans, emails, articles, templates.

Triggers: "preview", "show me", "render", "open in browser"

## Steps

1. **Identify the content to render**
   - If the user specifies a file, read it.
   - If the user says "preview this" or "show me", use the most recently discussed document.
   - If there is no clear target, ask: "Which document do you want to preview?"

2. **Generate the HTML**
   Wrap the markdown content in a full HTML page using this template:

   ```html
   <!DOCTYPE html>
   <html lang="en">
   <head>
     <meta charset="UTF-8">
     <meta name="viewport" content="width=device-width, initial-scale=1.0">
     <title>[Document Title]</title>
     <style>
       body {
         font-family: Georgia, 'Times New Roman', serif;
         background: #f5f0e8;
         color: #1a1a1a;
         max-width: 720px;
         margin: 48px auto;
         padding: 0 24px;
         line-height: 1.7;
         font-size: 17px;
       }
       h1 { font-size: 2em; margin-bottom: 0.25em; }
       h2 { font-size: 1.4em; margin-top: 2em; border-bottom: 1px solid #ccc; padding-bottom: 4px; }
       h3 { font-size: 1.1em; margin-top: 1.5em; }
       a { color: #2563eb; }
       code { background: #e8e0d0; padding: 2px 6px; border-radius: 3px; font-size: 0.9em; }
       pre { background: #e8e0d0; padding: 16px; border-radius: 6px; overflow-x: auto; }
       blockquote { border-left: 3px solid #999; margin-left: 0; padding-left: 16px; color: #555; }
       table { border-collapse: collapse; width: 100%; margin: 1em 0; }
       th, td { border: 1px solid #ccc; padding: 8px 12px; text-align: left; }
       th { background: #e8e0d0; }
       ul, ol { padding-left: 1.5em; }
       li { margin: 0.3em 0; }
       hr { border: none; border-top: 1px solid #ccc; margin: 2em 0; }
     </style>
   </head>
   <body>
     [RENDERED MARKDOWN CONTENT]
   </body>
   </html>
   ```

   Convert markdown to HTML manually:
   - `# Heading` → `<h1>`, `## ` → `<h2>`, etc.
   - `**bold**` → `<strong>`, `*italic*` → `<em>`
   - `` `code` `` → `<code>`, fenced blocks → `<pre><code>`
   - `- item` → `<ul><li>`
   - `[text](url)` → `<a href="url">text</a>`
   - `---` → `<hr>`
   - `| table |` → `<table>`
   - Blank lines between paragraphs → `<p>`
   - `- [ ] task` → `<input type="checkbox" disabled> task`
   - `- [x] task` → `<input type="checkbox" checked disabled> task`

3. **Write to a temp file**
   Write the HTML to `/tmp/big-brain-preview-[timestamp].html`.

4. **Open in browser**
   ```bash
   open /tmp/big-brain-preview-[timestamp].html
   ```

5. **Confirm**
   Tell the user the file was opened. Do not describe the content — they can see it.

## Rules

- Never modify the source markdown file — this skill is read-only.
- Use the cream theme (`#f5f0e8` background) — it is easier on the eyes than white.
- If the content is very long (>10,000 characters), warn the user before rendering.
- Clean up old temp files if you notice them (files older than today).
