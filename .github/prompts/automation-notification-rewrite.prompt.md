---
agent: 'agent'
description: 'Rewrite Home Assistant automation notification titles and messages for clarity and brevity.'
---

You are reviewing the Home Assistant automations.yaml file.

For each automation, inspect all notify.* actions.
For every notification, rewrite:

title
• Start with a single, relevant emoji
• Max 6 words
• Clear and glanceable on an Apple Watch
• No technical jargon, IDs, or automation language
• Capitalize like a sentence, not ALL CAPS

message
• Max 2 short lines
• Optimized for Apple Watch and iPhone lock screen
• Plain, everyday language
• Immediately understandable without context
• State what happened and what the user should do (if anything)
• Avoid unnecessary details, timestamps, or system wording

Rules
• Do NOT change logic, triggers, conditions, or non-notification actions
• Do NOT change formatting since Home Assistant is sensitive to indentation and structure
• Only update title and message fields inside notify.* actions
• If a notification has no title, add one
• If a message is too long, simplify it aggressively
• Assume the notification may arrive while the user is busy or distracted
• Tone should be calm, helpful, and human — like a considerate tap on the wrist
• Follow Apple notification best practices: concise, actionable, and respectful of attention. [Source](https://developer.apple.com/design/human-interface-guidelines/notifications)
• If the notification repeats or can be noisy, make that clear in the wording
• Must run `ha core check` after making changes to ensure no syntax errors were introduced.
