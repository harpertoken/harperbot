# HarperBot Standalone Repository

This is a standalone repository for HarperBot, extracted from the Friday Gemini AI project. HarperBot is an automated code review tool that uses Google's Gemini AI to analyze GitHub pull requests and provide feedback.

## Repository Structure

```
harperbot-standalone/
├── .github/workflows/harperbot.yml    # GitHub Actions CI/CD workflow
├── api/webhook.py                     # Webhook integration for Flask deployments
├── bin/setup-harperbot                # Installation script for adding to other repos
├── docs/README.md                     # Detailed documentation (copied from main project)
├── harperbot/                         # Core HarperBot code
│   ├── HarperBot.md                   # Additional documentation
│   ├── config.yaml                    # Configuration file
│   ├── harperbot.py                   # Main script (CLI and webhook modes)
│   ├── harperbot_apply.py             # Code application utilities
│   ├── manual.js                      # Manual review interface
│   └── suggestions.js                 # Suggestion handling
├── pyproject.toml                     # Python package configuration
├── setup-checksums.sha256             # Checksums for integrity verification
└── test/test_harperbot.py              # Unit tests
```

## Quick Start

1. **Clone or copy this repository** to your desired location.

2. **Install dependencies**:
   ```bash
   pip install -e .
   ```

3. **Configure**:
   - Copy `harperbot/config.yaml` and modify as needed
   - Set environment variables: `GEMINI_API_KEY`, `GITHUB_TOKEN` (for GitHub App mode) or `GITHUB_TOKEN` (for personal access token)

4. **Run**:
   - **CLI mode**: `python harperbot/harperbot.py --repo owner/repo --pr 123`
   - **Webhook mode**: Set up Flask server and configure GitHub webhook

## Development

- **Run tests**: `python -m pytest test/test_harperbot.py`
- **Linting**: Install pre-commit and run `pre-commit run --all-files`
- **Build package**: `python -m build`

## Contributing (Working on PRs)

To start working on pull requests for this repository:

1. **Access**: Ensure you have push access to `harpertoken/harperbot` or fork it and work via PRs.

2. **Setup**:
   - Clone: `git clone https://github.com/harpertoken/harperbot.git`
   - Install Python 3.8+ and deps: `pip install -e .`
   - Install pre-commit: `pip install pre-commit && pre-commit install`
   - Set env vars: `GEMINI_API_KEY` (from Google AI Studio), `GITHUB_TOKEN` (personal access token)

3. **Testing**:
   - Run tests: `python -m pytest test/`
   - For full functionality, set up a test GitHub repo and PR

4. **Workflow**:
   - Create branch: `git checkout -b feature/your-feature`
   - Code, commit (use conventional commits), push
   - Create PR on GitHub

5. **Documentation**: Update `README.md` or `docs/README.md` for new features.

## Integration

- **Add to another repo**: Run `bin/setup-harperbot` in the target repository
- **Webhook setup**: Use `api/webhook.py` with a WSGI server like Gunicorn
- **GitHub Actions**: Copy `.github/workflows/harperbot.yml` to your repo

## Configuration

Edit `harperbot/config.yaml` to customize:
- AI model (default: gemini-2.5-flash-lite)
- Analysis focus (all, security, performance, quality)
- Safety settings
- Authoring features (PR creation, commits)

## Notes

- This is extracted from the main Friday Gemini AI project
- Webhook integration in `api/webhook.py` is included for full functionality
- Checksums in `setup-checksums.sha256` ensure file integrity
- Documentation in `docs/README.md` provides comprehensive usage instructions

For issues or contributions, refer to the main project's GitHub repository.
