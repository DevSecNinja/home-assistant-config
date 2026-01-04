---
agent: 'agent'
description: 'Rewrite Home Assistant automation titles and descriptions to be user-friendly and clear.'
---

You are reviewing the Home Assistant automations.yaml file.

For each automation, rewrite:

alias (title)
• Max 10 words
• Clear, simple, no technical jargon
• Understandable by someone with no Home Assistant knowledge

description
• Max 4 short lines
• Plain, everyday language
• Explain what happens, when, and why, from a user’s perspective
• Avoid technical terms like trigger, entity, service, state, automation

Rules
• Do not change any logic, triggers, conditions, or actions
• Only update alias and description fields
• If a description is missing, add one
• Keep tone friendly and human, as if explaining it to a partner at home
• If the automation could be confusing or surprising, explicitly mention that behavior
• Must run `ha core check` after making changes to ensure no syntax errors were introduced.
