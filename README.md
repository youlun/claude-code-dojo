# Claude Code Dojo (Archived)

A system for improving both sides of human-AI collaboration — helping Claude build better infrastructure for itself, and helping the human catch their own mistakes and improve. It worked, just not the way we expected.

## What this was

A `/dojo` skill that debriefed sessions, identified whether friction came from the Claude side (missing rules, hooks, skills) or the human side (prompting habits, workflow choices, mental models), and filed findings into structured learnings files. Recurring findings were meant to "graduate" into actionable changes for whichever side needed them.

## Why it's archived

The intent — a self-improving loop where Claude builds its own infrastructure and the human refines their approach — is the right goal. But we over-engineered the implementation. A 7-step process with templates, graduation criteria, recurrence tracking, and domain files produced a knowledge base when what we actually needed was a workshop.

The insight: effective Claude Code users don't build reflection systems. They build **verification systems** — hooks that enforce behavior deterministically, a tight CLAUDE.md that prevents specific observed mistakes, and the habit of restarting sessions early when conversations degrade. The reflection still happens, but the output is always a concrete artifact, never a learnings entry waiting to be consulted.

## What replaced it

Version-controlling `~/.claude` directly. CLAUDE.md, hooks, skills, and settings already live there. The changelog is `git log`. The "why" behind each rule is `git blame`. A separate repo for learnings *about* your config was an abstraction layer that didn't need to exist.

The dual-sided improvement still happens — it just looks different:
- **Claude side:** After friction, add a CLAUDE.md rule or a hook. Claude gets better immediately, not after a graduation process.
- **Human side:** Recognize when a conversation is degrading and `/clear` instead of pushing through. Prompt with constraints and verification, not step-by-step instructions.

## The takeaway

If you want Claude to self-improve and you want to improve alongside it:

1. `git init ~/.claude`
2. After a frustrating session, ask: was that a missing rule, a missing hook, or a prompting habit?
3. If rule or hook — build it and commit. If habit — practice it next session.

That's the whole system. The reflection is a moment, not a process.
