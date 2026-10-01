# Jira To Tickets Codex Skill

`jira-to-tickets` turns an approved plan, specification, or current conversation into reviewed, dependency-aware Jira implementation tickets.

## Install

In a Codex chat, ask the built-in installer:

> `$skill-installer install the skill from https://github.com/cdracars/jira-to-tickets/tree/main/skills/jira-to-tickets`

The skill will be available in your next turn. Invoke it with `$jira-to-tickets`.

For a manual installation, copy `skills/jira-to-tickets/` into `~/.codex/skills/jira-to-tickets/`.

## Dependency

This skill relies on authenticated Jira access to create the approved implementation tickets and their blocking relationships. Configure a Jira integration or a compatible Jira skill before publishing.

## Origin

Adapted from Matt Pocock's [`to-tickets`](https://github.com/mattpocock/skills/tree/main/skills/engineering/to-tickets) skill and specialized for Jira publishing.

## License

This project is licensed under the [MIT License](LICENSE). It retains the upstream copyright notice.
