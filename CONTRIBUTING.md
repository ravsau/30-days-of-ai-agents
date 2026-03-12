# Contributing to 30 Days of AI Agents

Thanks for your interest in contributing! This project is an open-source learning resource for building AI agents.

## How to Contribute

### Report Issues
- Found a bug in the code? Open an issue with the day number and error message.
- Broken link or outdated info? Let us know.

### Fix or Improve Existing Days
1. Fork the repo
2. Create a branch: `git checkout -b fix/day-05-mcp-typo`
3. Make your changes
4. Run tests: `cd days/day-05 && pytest tests/`
5. Submit a PR with a clear description

### Add Resources
- Know a great article, video, or tool related to a day's topic? Add it to that day's `README.md` under a "Resources" section.

### Translate
- Want to translate a day's content? Create a `README.{lang}.md` (e.g., `README.es.md`) in the day's folder.

## Code Standards

- **Python 3.12+** with type hints
- **Format** with `ruff` (or `black`)
- **Every solution must have at least 1 passing test** in `tests/`
- Keep `.env` out of commits (use `.env.example` for templates)

## Day Folder Structure

```
days/day-NN/
├── README.md      # Topic, objectives, step-by-step instructions
├── starter/       # Starting code (learner fills in the blanks)
├── solution/      # Complete working solution
└── tests/         # pytest tests to validate
```

## Pull Request Guidelines

- One PR per fix/feature (don't bundle unrelated changes)
- Reference the day number in your PR title: `fix(day-05): update MCP server example`
- Include before/after if fixing a bug
- Make sure tests pass

## Community

- Be kind and constructive
- No spam or self-promotion
- Help others learn - we were all beginners once

## License

By contributing, you agree that your contributions will be licensed under the MIT License.
