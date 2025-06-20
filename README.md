# gh-pr-worktree

A GitHub CLI extension that creates [git worktrees](https://git-scm.com/docs/git-worktree) for GitHub Pull Requests, making it easy to review and test PRs in isolated directories.

## Features

- 🔄 Create git worktrees for any GitHub PR
- 🍴 Supports both same-repository branches and forked PRs
- 🧹 Automatic cleanup of remotes when needed
- ✨ Simple command-line interface
- 🛡️ Error handling and validation

## Installation

### Prerequisites

- [GitHub CLI](https://cli.github.com/) (`gh`)
- [Git](https://git-scm.com/)
- [jq](https://stedolan.jq.io/) for JSON parsing

### Install the extension

```bash
gh extension install brooke-hamilton/gh-pr-worktree
```

Or clone and install locally:

```bash
git clone https://github.com/brooke-hamilton/gh-pr-worktree.git
cd gh-pr-worktree
gh extension install .
```

## Usage

```bash
gh pr-worktree <PR_NUMBER> [WORKTREE_DIR]
```

### Arguments

- `PR_NUMBER`: The GitHub PR number to checkout (required)
- `WORKTREE_DIR`: Directory for the worktree (optional, defaults to `../pr-<PR_NUMBER>`)

### Examples

Create a worktree for PR #123 in the default location:
```bash
gh pr-worktree 123
```

Create a worktree for PR #456 in a specific directory:
```bash
gh pr-worktree 456 /tmp/pr-456-review
```

## How it works

1. **Fetches PR information** using the GitHub CLI
2. **Determines the source** (same repo branch vs. fork)
3. **Adds remote if needed** (for forked PRs)
4. **Fetches the PR branch** from the appropriate remote
5. **Creates a git worktree** in the specified directory

## Cleanup

When you're done reviewing the PR, clean up the worktree:

```bash
# Remove the worktree
git worktree remove ../pr-123

# If a remote was added for a fork, remove it too
git remote remove username
```

The script will show you the exact cleanup commands when it completes.

## Error Handling

The extension includes comprehensive error handling:

- Validates PR numbers
- Checks for required dependencies
- Ensures you're in a git repository
- Prevents overwriting existing directories
- Automatically cleans up on errors

## Requirements

- Must be run from within a git repository
- GitHub CLI must be authenticated (`gh auth login`)
- Target directory must not already exist

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## Support

If you encounter any issues or have questions, please [open an issue](https://github.com/brooke-hamilton/gh-pr-worktree/issues) on GitHub.
