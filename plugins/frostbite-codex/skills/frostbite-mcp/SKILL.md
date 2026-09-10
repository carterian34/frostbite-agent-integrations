---
name: frostbite-mcp
description: Use Frostbite MCP tools for authenticated skating, rink, journal, and social workflows. Apply when responding to requests that use Frostbite account data or actions.
---

# Frostbite MCP

Use the Frostbite MCP tools to act on behalf of the authenticated Frostbite user. The MCP server is the authority for authentication, authorization, feature access, administrative access, and privacy enforcement.

## Privacy and authorization

Do not inspect another user's privacy settings to predict whether an action will be permitted. Do not decline a requested Frostbite action based on an independent privacy judgment.

Attempt the requested, appropriately scoped tool call. The server evaluates the target user's sharing preferences and the authenticated caller's relationship, then returns the permitted result or denies access.

`privacy_settings_get_user_privacy_settings` and `privacy_settings_update_user_privacy_settings` are for the authenticated user's own settings only. Do not use either one to preflight an action involving another user.

## Rink-session attendances

For attendance records belonging to a specified user, call `rink_session_attendances_list_user_rink_session_attendances` with that user's ID and any relevant rink, session, date, or pagination filters.

For attendance records visible across the authenticated user's permitted connections, use `rink_session_attendances_list_rink_session_attendances`.

In both cases, let the server determine access. If it denies the request, report that outcome without attempting to retrieve the target user's privacy settings.

## Rink-session search filters

`rink_session_filters_get_rink_session_filters` returns persistent filters saved on the authenticated user's Frostbite profile. Frostbite applies these filters to every rink-session search, including `rink_sessions_list_rink_sessions`; they are not limited to one search request.

Before concluding that a requested session does not exist, retrieve these filters and consider whether they would exclude it. For example, a saved name filter for “freestyle” can hide a requested public skate.

When the saved filters conflict with the user's requested search:

1. Save the complete original filter object from `rink_session_filters_get_rink_session_filters`.
2. Use `rink_session_filters_update_rink_session_filters` to temporarily replace it with filters appropriate to the request, or neutral filters when no filtering is appropriate.
3. Search with `rink_sessions_list_rink_sessions`.
4. Restore the exact original filter object with `rink_session_filters_update_rink_session_filters` after the search, including if the search fails or produces no results.

Do not persistently change these filters unless the user explicitly asks to change their saved rink-session preferences.

## Rink-session dates

When users ask for sessions on a single local calendar date, treat `end_date` as an exclusive upper bound. Query `rink_sessions_list_rink_sessions` with:

```json
{
  "start_date": "<requested date>",
  "end_date": "<following calendar date>"
}
```

For example, to find sessions on September 8, use `start_date: "2026-09-08"` and `end_date: "2026-09-09"`. Do not set both dates to the same day, since that returns no sessions.

## Journal entries and skating exercises

In a skating journal entry, **skills** and **exercises** refer to the same tracked skating work. When a user describes practicing an identifiable skating move, record it in `entry.exercises`, not only in the entry name or notes.

Before creating or updating an entry:

1. Use `skating_skills_list_skating_skills` to resolve each mentioned skill to its `skating_skill_id`.
2. If the user identifies a way the skill was performed, use `skating_skill_variations_list_skating_skill_variations` to resolve a `variation_id` when applicable.
3. Include stated repetitions and duration in the exercise record. Preserve the user's date, notes, and other journal details.

Use `journals_create_user_journal_entry` to save a new entry and `journals_update_user_journal_entry` to replace an existing one. Do not invent a skill or variation ID when the skill cannot be resolved; ask for clarification when needed.

## Skating-skill suggestions

Use `skating_skills_suggest_skating_skill` when a user wants to propose a new skill. A suggestion remains associated with its creator until an administrator approves it.

Before updating or deleting a skating skill, use `skating_skills_list_skating_skills` to inspect its `user_id`. Users who are neither administrators nor moderators may update or delete only a skill whose `user_id` is their own. Treat deleting a pending suggestion as declining it. Once a skill is approved, its `user_id` is removed and its original suggester may no longer update or delete it.

Administrators and moderators may create approved skills, approve pending suggestions, and create, update, or delete skating-skill variations.
