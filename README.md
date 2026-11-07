# Foundations of Security Assessment

An open, syllabus-aligned learning resource for people getting into
penetration testing and security assessment. The content is mapped to the
**CREST CPSA** syllabus and written as **defensive reference material** —
conceptual explanations of how weaknesses arise, how an assessor identifies
them, and how they are remediated. It is deliberately **not** exam recall and
contains no past exam questions.

Built with [MkDocs](https://www.mkdocs.org/) and
[Material for MkDocs](https://squidfunk.github.io/mkdocs-material/).

## Run it locally

```bash
python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
pip install -r requirements.txt
mkdocs serve
```

Then open <http://127.0.0.1:8000>.

## Build

```bash
mkdocs build --strict
```

Output lands in `site/`.

## Deploy (GitHub Pages)

1. Create a new GitHub repo and push this project to the `main` branch.
2. In the repo: **Settings → Pages → Build and deployment → Source =
   GitHub Actions**.
3. Edit `mkdocs.yml` and replace every `CHANGE-ME` with your GitHub username /
   repo name / LinkedIn handle.
4. Push. The workflow in `.github/workflows/deploy.yml` builds and publishes
   automatically on every push to `main`.

## Before you publish — read this

- **CREST NDA.** Candidates sign an NDA covering exam content. Keep everything
  framed as general, published knowledge mapped to the *public* syllabus.
  Never add recalled or reconstructed exam questions. The "concept check"
  prompts in these pages are open questions for self-study, not exam items —
  keep any Q&A you add in that same style.
- **Employer policy.** Check your firm's policy on personal publishing and
  use of its name. Consider whether they want to co-brand or cross-promote.
- **Framing.** Pages are written defensively (weakness → how it's assessed →
  remediation) rather than as attack recipes. Keep new contributions in that
  register.

## License

Content is licensed under
[CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/).
See [LICENSE](LICENSE).

CPSA and CREST are trademarks of their respective owners. This is an
independent study resource and is not affiliated with or endorsed by CREST.
