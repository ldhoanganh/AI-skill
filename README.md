# AI Skills for QE

This repository contains reusable Codex skills for Quality Engineers.

## Included Skills

### `review-prd`

Reviews PRDs, Jira tickets, and feature specifications through Business, User, and Senior QE lenses.

It helps QEs identify requirement gaps, clarification questions, test-readiness conditions, and release risks before testing starts.

### `ai-bug-guardian`

Creates a structured English bug-report draft from QE-provided information and evidence.

It also checks related Jira issues and flags potential duplicate bugs before a new issue is created. QE reviews and approves the final report before creating Jira.

## Installation

Copy the required skill folder into your local Codex skills directory:

```bash
mkdir -p ~/.codex/skills
cp -R skills/review-prd ~/.codex/skills/
cp -R skills/ai-bug-guardian ~/.codex/skills/
