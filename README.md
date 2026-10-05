# skill-ats-job-boards

An agent skill that reads the open jobs of one company from its public Greenhouse, Lever or Ashby job board. It uses plain GET requests, so it needs no API key, no account and no token. It also tells you which of the three systems a company's careers page runs on.

It is a `SKILL.md` folder, so it works in Claude Code, Codex, Cursor, OpenCode and other agents that read Agent Skills.

## Install

```bash
npx skills add donmangudata-ops/skill-ats-job-boards
```

Or copy it by hand:

```bash
git clone https://github.com/donmangudata-ops/skill-ats-job-boards.git
cp -r skill-ats-job-boards ~/.claude/skills/ats-job-boards
```

## Ask your agent

- "What roles is Dropbox hiring for right now?"
- "Which system does the careers page at https://example.com/careers use?"
- "How many open roles does Ramp have by department?"
- "Give me Spotify's open postings as a CSV."

## What it does

1. Detects the ATS and the board slug from a careers link, from the page HTML, or by trying the three feeds once each.
2. Fetches the public JSON with `curl` or the agent's web fetch tool, one request per second. Agents can call these public endpoints directly, with no key.
3. Maps each posting to the same fields: id, title, location, department, team, employment type, workplace, url, published and updated dates.
4. Answers with the count, the company, the ATS and the time the feed was read.

## What it does not do

It reads one company at a time. It does not search across companies, does not read Workday, SmartRecruiters or iCIMS, and never collects names, emails or profiles of people.

## Optional hosted API

Everything here works without any account. A hosted version that returns the normalized shape in one call is optional: https://ats-jobs-api.don-mangu-data.workers.dev

```bash
curl -s "https://ats-jobs-api.don-mangu-data.workers.dev/jobs?ats=greenhouse&board=dropbox&limit=5&src=skill"
```

## License and credit

MIT, see [LICENSE](LICENSE). Data tooling by Don Mangu. [https://donmangudata-ops.github.io](https://donmangudata-ops.github.io)

Not affiliated with Greenhouse, Lever or Ashby. The data is public job-board content owned by each company.
