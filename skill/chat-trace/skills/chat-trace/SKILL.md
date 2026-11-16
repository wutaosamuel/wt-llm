---
name: chat-trace
description: Archive complete selected questions from the current session in Chinese and English with original-language labels and concise AI response summaries in bilingual PROJECT_TRACE Markdown files. Use when the user asks to record questions or save conversation history, including 记录提问, 保存历史提问, 保存对话记录, and 整理问答. Always confirm question selection first, then present both language previews for approval before writing.
compatibility: opencode
metadata:
  audience: developers
  scope: session-question-archive
---

# Chat Trace

## Purpose

Archive the user's selected questions from the current session in full,
translated into each file's language when needed, together with concise
summaries of the corresponding AI responses. Identify each question's
original language.

Maintain two Markdown files in the current working directory (workspace root):

- `PROJECT_TRACE.zh-cn.md` — Simplified Chinese questions and AI summaries
- `PROJECT_TRACE.en.md` — English questions and AI summaries

Preserve questions verbatim in the version matching their original language.
In the other version, translate the complete question without omission or
summarization. Keep code, paths, and links unchanged.

This SKILL.md is written in English. Use this skill for requests in either
English or Chinese.

## Workflow (follow strictly)

### Step 1: Define the scope

Review all conversations in the current session, excluding the message that
invokes this skill. Use whichever AI response content is currently readable.

Do not search other sessions or introduce time-range or history-source
selection.

If a question's original text is not readable, mark it as unavailable.
Do not reconstruct it from memory or a conversation summary. If the user
selects that question, request its original text before including it in
the final archive.

### Step 2: Display the question selection table

List user questions in conversation order. Number them using 1, 2, 3,
and so on.

Use only these two columns:

| No. | User question (complete original text) |
|-----|----------------------------------------|
| 1 | [Complete original question] |
| 2 | [Complete original question] |

Do not generate or display AI response summaries at this stage.

Ask the user to select question numbers, select all, or cancel.
Then stop and wait for explicit selection confirmation.
Do not proceed automatically.

Preserve line breaks, code, punctuation, links, and paths in user questions.
Markdown escaping must not change their content. If a question cannot be
displayed intact inside a table, place its complete original text below
the table under the same number and reference it from the table.
Never abbreviate a question or replace its content with ellipses.

### Step 3: Generate the selected Q&A previews

Include only selected questions, retaining their original numbers and order.

Present the full proposed content for both files:
- Simplified Chinese questions and summaries for `PROJECT_TRACE.zh-cn.md`.
- English questions and summaries for `PROJECT_TRACE.en.md`.

Use the archive template below. Both versions must contain the same selected
questions and equivalent summaries.

Translate each complete question into the target language when needed; do not
summarize it. Preserve original text when it already matches the target language.
Keep code, paths, and links unchanged in translations.

Include an original-language column for each question in both previews and files.
For a Chinese original, use `zh-cn (original)` in the Chinese version and
`zh-cn (translated to en)` in the English version. For an English original,
use `en (original)` in the English version and `en (translated to zh-cn)` in
the Chinese version. Identify other or mixed original languages accurately
rather than forcing an English or Chinese label.

Summary requirements:
- Faithfully summarize the actual response without adding conclusions or advice.
- Prioritize conclusions, key reasons, and necessary actions.
- Normally use 1–3 sentences; use short bullet points when needed.
- If no corresponding AI response is readable, use “无可读取的 AI 回答”
  in Chinese and “No readable AI response available” in English.

State the actual save paths and whether each file will be created or appended
to. Create missing files; append to existing files without overwriting content.

Begin each batch with a level-two timestamp heading. Use the same heading
for the corresponding batch in both files. Explain that the timestamp will
be taken from the actual save time, not guessed.

### Step 4: Wait for final confirmation

Write only after the user explicitly confirms the final content and save plan.

If the user requests changes, update the previews and wait for confirmation again.

If the user cancels, do not write any archive content.

## Archive template

Each saved batch uses the following structure. Replace placeholders with
the actual timestamp, selected questions, original-language labels, and approved
summaries.

```markdown
## YYYY-MM-DD HH:mm ±HH:mm

| No. | Complete user question | Original language | Concise AI response summary |
|-----|------------------------|-------------------|-----------------------------|
| [Original number] | [Original text or complete translation] | [Original language and translation status] | [Approved summary] |
```

Use Chinese column headings, questions, and summaries in the Chinese file,
and English column headings, questions, and summaries in the English file.

For complex questions, the complete-question sections referenced by the table
are part of both the preview and the saved batch. Apply the same target-language
and original-language labeling rules to these sections.

## Hard rules

- Preserve original questions verbatim in the selection table and matching-language
  archive; translate them completely in the other archive. Summarize only AI responses.
- Identify each question's original language and whether its text is translated.
- Never fabricate unreadable questions or responses.
- Keep the Chinese and English batches aligned.
- Do not combine or skip the two confirmations.
- Never write archive content before final approval.
- Append rather than overwrite existing content.
- Use an actual save timestamp, identical in both files.
- Keep saving within Step 4; do not add a fifth workflow step.
