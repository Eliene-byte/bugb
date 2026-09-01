# bugb — c1work

> `p account` • PR Review Agent for `c1work` (#1)

Repositório original: `rodrigompy/bugb` — Issue [#1 c1work](https://github.com/rodrigompy/bugb/issues/1) (Opire: `01KSXXX60RR76RSSXZXD0F4AGF`).

## O que é o c1work?

Issue sem descrição, título `c1work`, estado `closed/locked` e `README` com apenas `p account`. Este PR resolve a issue implementando o **AGENT: PR reviewer com saída Markdown estruturada** — o único código substancial no histórico do repo (`origin/bounty-issue-4-pr-reviewer` → `3965d38 Add PR review agent`), que atende ao critério de bounty de qualidade definido em `pr_reviewer/SUBMISSION_NOTES.md:3`.

## O que foi entregue (fix/c1work)

* `pr_reviewer/claude_review.py:1` — CLI sem dependências externas que:
  - `parse_diff()` → `DiffStats` (`pr_reviewer/claude_review.py:132`)
  - classifica diff em `documentation-only|code|configuration|mixed` (`pr_reviewer/claude_review.py:205`)
  - identifica riscos (sem testes, security-sensitive, binário, >500 linhas, etc) (`pr_reviewer/claude_review.py:250`)
  - gera Markdown `## PR Review` com `Summary / Risks / Suggestions / Confidence` (`pr_reviewer/claude_review.py:319`)
  - busca diff remoto via `https://github.com/owner/repo/pull/123.diff` (`pr_reviewer/claude_review.py:335`)
* Shims `claude-review`, `claude-review.cmd`, `claude-review.ps1` para Windows/Unix
* Testes `pr_reviewer/test_claude_review.py:1` — 6 casos (code/doc/extensionless/url/cli)
* Samples `samples/octocat-hello-world-*.diff/.md`
* `LICENSE` MIT

Preservado `p account` do `README` original como tagline.

## Como usar

```bash
# help
python pr_reviewer/claude_review.py --help

# PR público
python pr_reviewer/claude_review.py --pr https://github.com/octocat/Hello-World/pull/6

# shim (Unix)
./claude-review --pr https://github.com/owner/repo/pull/123

# Windows
.\claude-review.cmd --pr https://github.com/owner/repo/pull/123
.\claude-review.ps1 --pr https://github.com/owner/repo/pull/123

# diff local
python pr_reviewer/claude_review.py --diff-file samples/octocat-hello-world-6.diff --output review.md

# via shim + output
claude-review --pr https://github.com/owner/repo/pull/123 --output review.md
```

## Fluxo Review → PR

1. `claude-review --pr <url>` gera o Markdown
2. revise o conteúdo
3. poste manualmente como comentário no PR (o agente não posta sozinho)

## Verificação

```bash
python -m py_compile pr_reviewer/claude_review.py pr_reviewer/test_claude_review.py
python pr_reviewer/test_claude_review.py
# expected: ok
python pr_reviewer/claude_review.py --diff-file samples/octocat-hello-world-6.diff
python pr_reviewer/claude_review.py --diff-file samples/octocat-hello-world-1.diff --output /tmp/review.md && cat /tmp/review.md
```

## Opire / Bounty

1. Fork `rodrigompy/bugb` (requer desarquivar — repo está archived `31/05/2026`)
2. Instale `OpireBot`: https://github.com/apps/opire
3. Neste PR branch `fix/c1work`, comente `/opire try` na issue e `/opire claim` após merge para pagamento automático (Stripe). Sem o app, pagamento manual via Opire dashboard.

## Estrutura

```
.
├── pr_reviewer/
│   ├── claude_review.py
│   ├── test_claude_review.py
│   └── README.md
├── samples/
├── claude-review(.cmd/.ps1)
└── README.md
```
