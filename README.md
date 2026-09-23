# Refactoring UI — Claude Skill

A [Claude Code](https://claude.com/claude-code) / Claude [Agent Skill](https://docs.claude.com/en/docs/claude-code/skills) that teaches Claude practical visual-design rules for building and reviewing user interfaces. It covers hierarchy, spacing, typography, color palettes, depth and shadows, images, and finishing touches.

The principles are summarized and paraphrased from the excellent book **[Refactoring UI](https://www.refactoringui.com/)** by Adam Wathan & Steve Schoger. This project is not affiliated with or endorsed by the authors. If you find it useful, **buy the book**: it's full of before/after visuals that a text summary can't capture.

## What it does

- **Building UI:** Claude starts from features rather than layout and gets the hierarchy right in grayscale first. It takes spacing, type, color and shadows from constrained scales, and uses your existing design system or Tailwind config when one exists.
- **Reviewing UI:** Claude audits a screen against a checklist ordered by visual impact and reports each problem as *element → rule → exact fix*.
- It triggers automatically on UI work, including vague requests like "make this look better" or "this feels cluttered".

## Structure

```
refactoring-ui/
├── SKILL.md                      # triggers, workflow, core rules
└── references/
    ├── principles.md             # every rule, with rationale and CSS examples
    ├── review-checklist.md       # audit checklist + report format
    └── design-tokens.md          # starter spacing/type/color/shadow scales + recipes
```

## Install

**Claude Code (personal, all projects):**

```bash
git clone https://github.com/fdrissi/refactoring-ui-skill.git
cp -R refactoring-ui-skill/refactoring-ui ~/.claude/skills/
```

**Claude Code (one project):** copy `refactoring-ui/` into `<project>/.claude/skills/`.

**Claude.ai:** zip the `refactoring-ui/` folder and upload it under *Settings → Capabilities → Skills*.

## License

MIT for the text and code in this repository. The ideas belong to their original authors; see *Refactoring UI*.
