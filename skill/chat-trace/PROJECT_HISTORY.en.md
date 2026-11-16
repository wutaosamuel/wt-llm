# Project History

## Project Overview

Chat Trace is an OpenCode skill for archiving Q&A from the current session.
Selected questions are presented completely in each archive's target language,
corresponding AI responses are summarized concisely, and bilingual Markdown
files are produced.

## Current Status

- Feature specification saved: `docs/specs/chat-trace.md`.
- English skill saved and read back: `skills/chat-trace/SKILL.md`.
- The skill was updated to translate questions completely into each archive's
  target language and identify each question's original language.
- Not installed under `.opencode`; actual Q&A archiving has not been validated.
- The specification has not yet incorporated subsequent approved rule changes.

## Design & Key Decisions

- Fixed four-step workflow: define scope, display question selection,
  generate selected Q&A previews, and await final confirmation before saving.
- Require two separate confirmations: question selection, then final content
  and save plan.
- Scope covers the current session, excluding the invoking message.
  Do not search other sessions.
- Preserve questions verbatim. Mark unreadable originals rather than
  reconstructing them from memory. Selected unreadable questions require
  the original text before archiving.
- The selection table has only number and question columns, using numeric
  conversation-order numbering. Final previews retain selected numbers
  and order.
- The skill itself is English; its description includes Chinese triggers
  such as “记录提问”.
- Archive files are `PROJECT_TRACE.zh-cn.md` and `PROJECT_TRACE.en.md`,
  saved by default in the current working directory.
- Questions in the Chinese archive use Simplified Chinese; questions in the
  English archive use English. When a question's original language differs
  from the archive language, translate it completely and identify the original
  language and translation status. Keep code, paths, and links unchanged.
- AI summaries are written in Chinese and English respectively.
- Create missing files; append to existing files without overwriting content.
- Separate each batch with matching level-two timestamp headings in both
  files, using the actual save time.
- Complex questions may use numbered complete-original-text sections below
  the table. Never replace content with ellipses.

## Pitfalls & Lessons Learned

- Earlier question originals may be unreadable in long sessions.
  Summaries must not be presented as original text.
- Markdown table formatting must not lose line breaks, code, or pipe characters
  from questions.
- Question translations must preserve the complete meaning and accurately
  identify the original language and translation status.
- Saving a specification, saving a skill, and archiving Q&A are distinct
  operations. Saving the skill does not approve archiving this conversation.

## Development History

| Date | Summary |
|------|---------|
| 2026-11-13 | Organized and saved the Chat Trace specification and English skill. Established the four-step workflow, two confirmations, verbatim questions, bilingual archives, create-or-append behavior, and timestamp separators. Deferred OpenCode installation. |
| 2026-11-16 | Updated the English skill to translate questions completely into each archive's target language and label the original language and translation status. Questions now use Simplified Chinese or English according to the archive. The four-step workflow remains unchanged. |

## Next Steps

- Synchronize the specification with the question-translation, original-language
  labeling, and bilingual archive rules.
- Validate both confirmations, cancellation, complex-question fidelity,
  translation completeness, and bilingual file creation and appending.
- Defer OpenCode installation until separately requested by the user.
