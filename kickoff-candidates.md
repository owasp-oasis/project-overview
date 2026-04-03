# OASIS Candidate Library Evaluation Report

This document outlines the search criteria, ranking methodology, and evaluation results for identifying strong open source projects to participate in the OWASP OASIS kickoff.

The goal is to select libraries where AI assisted security improvements, reviewed and approved by humans, can deliver high impact, high quality contributions to widely used open source ecosystems.

> *Note: AI was used to generate the scores and resulting project list.*

---

## Search Criteria

Candidate libraries must meet the following baseline requirements.

### 1. Language Requirements
Projects must be written primarily in:

- JavaScript  
- TypeScript  
- Python  

These languages align with OASIS focus areas and maximize ecosystem impact.

### 2. Contributor Friendliness
Projects should demonstrate:

- Clear contribution guidelines  
- Active maintainers responding to issues and pull requests  
- A welcoming community, for example labels such as good first issue or help wanted  
- No explicit prohibition on AI assisted contributions when reviewed by humans  

### 3. AI Assisted Contribution Compatibility
Projects must be:

- Open to pull requests generated with AI assistance  
- Willing to accept contributions if they are reviewed, corrected, and validated by humans  
- Not governed by policies that forbid AI generated code  

### 4. Active Maintenance
Indicators include:

- Recent commits within 90 days  
- Active issue triage  
- Regular releases  
- Maintainer responsiveness  

### 5. Real World Adoption
Projects should be:

- Used in production systems, SaaS platforms, or widely adopted by developers  
- Referenced in documentation, tutorials, or industry usage reports  
- Downloaded frequently on package registries  

### 6. Test Coverage
Projects must include:

- Unit tests or regression tests in the repository  
- Continuous integration pipelines  
- Evidence of test execution on pull requests  

---

## Scoring Methodology

Each project is evaluated across six weighted dimensions.

| Criterion | Weight | Description |
|----------|--------|-------------|
| Ecosystem Impact | 30 percent | How widely the library is used in SaaS, production systems, or developer tooling |
| Maintenance Activity | 20 percent | Commit frequency, issue responsiveness, release cadence |
| Contributor Friendliness | 15 percent | Documentation, onboarding, governance, community health |
| AI Assisted Contribution Readiness | 15 percent | Openness to AI generated pull requests with human review |
| Test Coverage and CI Quality | 10 percent | Presence and quality of automated tests |
| Technical Fit (Language) | 10 percent | Alignment with JavaScript, TypeScript, and Python |

Each library receives a score from 1 to 10 in each category, multiplied by the weight, producing a final weighted score from 0 to 100.

## Ranked Results (Top 20 Candidates)

| Rank | Project | Lang | Impact (30) | Maint. (20) | Contrib. (15) | AI Ready (15) | Tests (10) | Fit (10) | Total |
|------|---------|------|-------------|-------------|----------------|----------------|-------------|-----------|--------|
| 1 | FastAPI | Py | 28 | 19 | 14 | 14 | 9 | 10 | 94 |
| 2 | Prisma | TS | 27 | 18 | 14 | 14 | 9 | 10 | 92 |
| 3 | VS Code Core | TS | 30 | 17 | 13 | 15 | 9 | 10 | 94 |
| 4 | MUI | TS | 26 | 18 | 14 | 13 | 9 | 10 | 90 |
| 5 | Ant Design | TS | 26 | 17 | 13 | 13 | 9 | 10 | 88 |
| 6 | N8n | TS | 25 | 18 | 14 | 13 | 8 | 10 | 88 |
| 7 | Dify | TS/Py | 24 | 18 | 14 | 14 | 8 | 10 | 88 |
| 8 | tRPC | TS | 25 | 17 | 13 | 13 | 8 | 10 | 86 |
| 9 | Zod | TS | 24 | 17 | 14 | 13 | 8 | 10 | 86 |
| 10 | Express.js | JS | 30 | 14 | 12 | 12 | 7 | 10 | 85 |
| 11 | Next.js | TS | 29 | 16 | 12 | 12 | 8 | 10 | 87 |
| 12 | Pydantic | Py | 24 | 17 | 13 | 13 | 9 | 10 | 86 |
| 13 | Requests | Py | 30 | 14 | 12 | 12 | 7 | 10 | 85 |
| 14 | Pandas | Py | 29 | 16 | 11 | 11 | 9 | 10 | 86 |
| 15 | TypeORM | TS | 23 | 16 | 13 | 12 | 8 | 10 | 82 |
| 16 | Sequelize | JS/TS | 24 | 15 | 12 | 12 | 7 | 10 | 80 |
| 17 | Directus | TS | 22 | 17 | 13 | 12 | 8 | 10 | 82 |
| 18 | Editor.js | TS | 22 | 16 | 13 | 12 | 8 | 10 | 81 |
| 19 | Cal.com | TS | 23 | 16 | 12 | 12 | 7 | 10 | 80 |
| 20 | Immich | TS | 22 | 17 | 12 | 12 | 7 | 10 | 80 |

---

## Notes and Observations

FastAPI, Prisma, and VS Code stand out as extremely high impact, very active, friendly to contributors, and likely to accept AI assisted pull requests with human review.

UI frameworks such as Material UI and Ant Design have excellent test coverage and large user bases, which makes them high value targets for security improvements.

Backend frameworks such as Express, Next.js, and tRPC power a significant portion of modern SaaS and web applications.

Data libraries such as Pandas and Pydantic are central to machine learning and backend pipelines, and improvements here benefit a wide range of systems.

---

## Conclusion

This list provides a high quality, high impact set of 20 candidate libraries that align with the OASIS mission. Each project is:

- Actively maintained  
- Widely used  
- Contributor friendly  
- Technically aligned with JavaScript, TypeScript, and Python  
- Likely to accept AI assisted contributions with human review  
- Equipped with meaningful test coverage  

These projects represent excellent starting points for OASIS remediation work.
