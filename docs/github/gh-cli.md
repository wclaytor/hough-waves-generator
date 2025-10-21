# GitHub CLI Issues Management Guide

A comprehensive guide to managing GitHub issues using the `gh` command line tool.

## Getting Started with gh CLI

### Installation

First, you'll need to install the GitHub CLI. You can find installation instructions at https://cli.github.com, but here are the common methods:

- **macOS**: `brew install gh`
- **Windows**: `winget install --id GitHub.cli` or `scoop install gh`
- **Linux**: Check your distribution's package manager or download from the releases page

### Authentication

After installation, authenticate with GitHub:

```bash
gh auth login
```

Follow the interactive prompts to authenticate via browser or with a token.

## Working with Issues

### Listing Issues

View issues in the current repository:

```bash
gh issue list
```

Common filtering options:

```bash
# Show only open issues assigned to you
gh issue list --assignee @me

# Show closed issues
gh issue list --state closed

# Filter by labels
gh issue list --label "bug" --label "priority"

# Show issues you've authored
gh issue list --author @me

# Limit the number of results
gh issue list --limit 10

# Search for specific text
gh issue list --search "navigation bug"
```

### Viewing Issue Details

View a specific issue:

```bash
# View issue #123
gh issue view 123

# View in web browser
gh issue view 123 --web

# View issue comments
gh issue view 123 --comments
```

### Creating Issues

Create a new issue interactively:

```bash
gh issue create
```

Create with specific details:

```bash
# Create with title and body
gh issue create --title "Bug: Navigation broken" --body "The navigation menu doesn't open on mobile"

# Create with labels and assignee
gh issue create --title "Add dark mode" --label "enhancement" --assignee @me

# Create with a milestone
gh issue create --title "Update documentation" --milestone "v2.0"

# Create from a file
gh issue create --title "Feature request" --body-file feature-description.md
```

### Editing Issues

Edit an existing issue:

```bash
# Edit interactively
gh issue edit 123

# Update specific fields
gh issue edit 123 --title "Updated title"
gh issue edit 123 --body "New description"
gh issue edit 123 --add-label "bug" --remove-label "enhancement"
gh issue edit 123 --add-assignee username --remove-assignee olduser
gh issue edit 123 --milestone "v1.2"
```

### Managing Issue State

Close and reopen issues:

```bash
# Close an issue
gh issue close 123

# Close with a comment
gh issue close 123 --comment "Fixed in PR #456"

# Reopen an issue
gh issue reopen 123
```

### Working with Comments

Add comments to issues:

```bash
# Add a comment
gh issue comment 123 --body "I'm working on this now"

# Add comment from file
gh issue comment 123 --body-file comment.md

# Edit your last comment (interactive)
gh issue comment 123 --edit-last
```

### Transferring Issues

Transfer an issue to another repository:

```bash
gh issue transfer 123 owner/new-repo
```

### Pinning Issues

Pin or unpin issues (requires appropriate permissions):

```bash
# Pin an issue
gh issue pin 123

# Unpin an issue
gh issue unpin 123
```

## Advanced Usage

### Working with Different Repositories

Specify a different repository:

```bash
# List issues from a specific repo
gh issue list --repo owner/repo-name

# Create an issue in a different repo
gh issue create --repo owner/repo-name
```

### Output Formats

Change the output format for scripting:

```bash
# JSON output
gh issue list --json number,title,state

# Custom formatting with Go templates
gh issue list --json number,title,assignees --template '{{range .}}#{{.number}}: {{.title}} ({{.assignees}}){{"\n"}}{{end}}'

# Export to CSV-like format
gh issue list --json number,title,state --jq '.[] | [.number, .title, .state] | @csv'
```

### Batch Operations

Process multiple issues using shell scripting:

```bash
# Close all issues with a specific label
gh issue list --label "wont-fix" --json number --jq '.[].number' | xargs -I {} gh issue close {}

# Add a label to multiple issues
for issue in 123 124 125; do
  gh issue edit $issue --add-label "needs-review"
done
```

### Using Templates

Create issues from templates:

```bash
# List available templates
gh issue create --web

# Use a specific template (if configured in .github/ISSUE_TEMPLATE/)
gh issue create --template bug_report.md
```

## Useful Aliases

You can create aliases for common commands:

```bash
# Set up aliases
gh alias set my-issues 'issue list --assignee @me'
gh alias set bugs 'issue list --label bug'
gh alias set recent 'issue list --state all --limit 10'

# Use aliases
gh my-issues
gh bugs
gh recent
```

## Tips and Best Practices

1. **Default Repository**: The `gh` command automatically detects the repository based on your current directory's git remote. Make sure you're in the right repository directory.

2. **Interactive vs Direct**: Many commands support both interactive mode (just the base command) and direct mode (with flags). Interactive mode is great for exploration, while direct mode is better for scripts.

3. **Combine with Other Tools**: The JSON output makes it easy to combine `gh` with tools like `jq`, `grep`, and other Unix utilities for powerful workflows.

4. **Check Permissions**: Some operations require specific repository permissions. If a command fails, verify you have the necessary access rights.

5. **Use `--help`**: Every command has detailed help available via `gh issue <command> --help`.

## Quick Reference

| Command | Description |
|---------|-------------|
| `gh issue list` | List issues in the repository |
| `gh issue view <number>` | View a specific issue |
| `gh issue create` | Create a new issue |
| `gh issue edit <number>` | Edit an existing issue |
| `gh issue close <number>` | Close an issue |
| `gh issue reopen <number>` | Reopen a closed issue |
| `gh issue comment <number>` | Add a comment to an issue |
| `gh issue transfer <number> <repo>` | Transfer issue to another repo |
| `gh issue pin <number>` | Pin an issue |

## Common Workflows

### Daily Issue Triage

```bash
# View all your assigned open issues
gh issue list --assignee @me --state open

# Check recent issues that need attention
gh issue list --label "needs-triage" --limit 20
```

### Bug Management

```bash
# List all open bugs
gh issue list --label "bug" --state open

# Find high-priority bugs
gh issue list --label "bug" --label "high-priority"
```

### Sprint Planning

```bash
# View issues for a specific milestone
gh issue list --milestone "Sprint 23"

# Add issues to a milestone
gh issue edit 123 --milestone "Sprint 24"
```

## Additional Resources

- [GitHub CLI Documentation](https://cli.github.com/manual/)
- [GitHub Issues Documentation](https://docs.github.com/en/issues)
- [GitHub CLI Repository](https://github.com/cli/cli)

---

This guide covers the essential features for managing GitHub issues via the command line. The `gh` tool is actively developed, so check `gh issue --help` for the most up-to-date options and features.
