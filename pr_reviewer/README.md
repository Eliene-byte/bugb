# Claude Review Agent

CLI agent that reviews a GitHub pull request diff and returns a structured Markdown review comment.

## Setup

No third-party dependencies are required.

```bash
python pr_reviewer/claude_review.py --help
```

Optionally place the repository root on your `PATH` so the `claude-review` shim is available.

## Usage

Review a public GitHub pull request:

```bash
claude-review --pr https://github.com/owner/repo/pull/123
```

On Windows from the repository root:

```cmd
.\claude-review.cmd --pr https://github.com/owner/repo/pull/123
```

Review a local diff file:

```bash
python pr_reviewer/claude_review.py --diff-file samples/octocat-hello-world-6.diff
```

Write the Markdown review to a file:

```bash
claude-review --pr https://github.com/owner/repo/pull/123 --output review.md
```

## Output Format

The generated Markdown contains:

- Summary of changes
- Identified risks
- Improvement suggestions
- Confidence score: Low, Medium, or High

## Verification

```bash
python -m py_compile pr_reviewer/claude_review.py pr_reviewer/test_claude_review.py
python pr_reviewer/test_claude_review.py
```

Sample outputs are included under `samples/`.
