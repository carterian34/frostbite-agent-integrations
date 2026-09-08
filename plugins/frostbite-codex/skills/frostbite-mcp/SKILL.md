---
name: frostbite-mcp
description: Use Frostbite MCP tools for authenticated skating, rink, journal, and social workflows. Apply when responding to requests that use Frostbite account data or actions.
---

# Frostbite MCP

Use Frostbite MCP tools to act on behalf of the authenticated user. Frostbite is the authority for authentication, authorization, feature access, administrator access, and privacy enforcement.

## Privacy and authorization

Do not inspect another user's privacy settings to predict whether an action will be permitted. Attempt the appropriately scoped action, then report the server's permitted result or denial.

## Rink-session filters

Before concluding that a requested session does not exist, retrieve saved rink-session filters and consider whether they exclude it. When saved filters conflict with the requested search, save the complete original object, temporarily apply appropriate filters, search, and restore the exact original object even after a failed or empty search.

## Rink-session dates

For one local calendar date, `end_date` is exclusive. For September 8, query with `start_date: "2026-09-08"` and `end_date: "2026-09-09"`; do not use the same date for both values.

## Rink-session rink filters

Use `rink_ids` as a list even for a single rink, such as `rink_ids: [5]`. Do not use `rink_id` with the rink-session tool.

## Journal entries

Skills and exercises refer to the same tracked skating work. Resolve a mentioned skill before creating or updating a journal entry, and record it in `entry.exercises` when it can be identified.
