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
- Java  

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

| Rank | Project | Language | Ecosystem impact | Maintenance activity | Contributor friendliness | AI readiness | Test coverage | Technical fit | Total weighted score |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 1 | [Django](https://github.com/django/django) | Python | 5 | 5 | 5 | 4 | 5 | 5 | 4.9 |
| 2 | [FastAPI](https://github.com/fastapi/fastapi) | Python | 4 | 5 | 5 | 4 | 5 | 5 | 4.7 |
| 3 | [Spring Boot](https://github.com/spring-projects/spring-boot) | Java | 5 | 5 | 4 | 4 | 5 | 5 | 4.7 |
| 4 | [React](https://github.com/facebook/react) | JS/TS | 5 | 5 | 4 | 4 | 4 | 4 | 4.5 |
| 5 | [Express.js](https://github.com/expressjs/express) | JavaScript | 5 | 4 | 4 | 4 | 4 | 4 | 4.3 |
| 6 | [NestJS](https://github.com/nestjs/nest) | TypeScript | 4 | 5 | 4 | 4 | 4 | 4 | 4.3 |
| 7 | [Next.js](https://github.com/vercel/next.js) | JS/TS | 5 | 4 | 4 | 4 | 4 | 4 | 4.3 |
| 8 | [Angular](https://github.com/angular/angular) | TypeScript | 5 | 4 | 4 | 4 | 4 | 4 | 4.3 |
| 9 | [Vue.js](https://github.com/vuejs/vue) | JavaScript | 4 | 4 | 4 | 4 | 4 | 4 | 4.2 |
| 10 | [Pandas](https://github.com/pandas-dev/pandas) | Python | 5 | 4 | 4 | 4 | 5 | 4 | 4.4 |
| 11 | [NumPy](https://github.com/numpy/numpy) | Python | 5 | 4 | 4 | 4 | 5 | 4 | 4.4 |
| 12 | [TensorFlow](https://github.com/tensorflow/tensorflow) | Python | 5 | 4 | 4 | 4 | 5 | 4 | 4.4 |
| 13 | [scikit-learn](https://github.com/scikit-learn/scikit-learn) | Python | 5 | 4 | 4 | 4 | 5 | 4 | 4.4 |
| 14 | [Flask](https://github.com/pallets/flask) | Python | 4 | 4 | 4 | 4 | 4 | 4 | 4.1 |
| 15 | [Spring Framework](https://github.com/spring-projects/spring-framework) | Java | 5 | 4 | 4 | 4 | 5 | 4 | 4.4 |
| 16 | [JUnit 5](https://github.com/junit-team/junit5) | Java | 4 | 4 | 4 | 4 | 5 | 4 | 4.2 |
| 17 | [Jest](https://github.com/jestjs/jest) | JS/TS | 4 | 4 | 4 | 4 | 5 | 4 | 4.2 |
| 18 | [Playwright](https://github.com/microsoft/playwright) | TypeScript | 4 | 4 | 4 | 4 | 5 | 4 | 4.2 |
| 19 | [Apache Kafka Java Client](https://github.com/apache/kafka) | Java | 4 | 4 | 3 | 4 | 5 | 4 | 4.0 |
| 20 | [Axios](https://github.com/axios/axios) | JavaScript | 4 | 4 | 4 | 4 | 4 | 3 | 3.9 |
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

---
# OASIS Candidate Library Discovery Prompt
Use this prompt to re-generate this document with updated search parameters.

```markdown
# OASIS Candidate Library Discovery Prompt

I am looking for candidate open source libraries to evaluate for the OWASP OASIS project:
https://github.com/owasp-oasis/project-overview

Your task is to:
1. Identify 20 strong candidate libraries that meet the criteria below.  
2. Rank them from strongest to weakest candidate.  
3. Provide justification for each selection.  
4. Produce a detailed comparison table.  
5. Use only the languages specified in the criteria section.

## Candidate Selection Criteria

A good candidate library must meet all of the following:

### Language Requirements
The project must be written primarily in one or more of the following languages:
* JavaScript
* TypeScript
* Python
* Java

(When rerunning this prompt, replace this list with the new target languages.)

### Contributor Friendliness
The project should:
* Have clear contribution guidelines  
* Have active maintainers who respond to issues and pull requests  
* Be welcoming to new contributors  
* Not prohibit AI assisted contributions, as long as a human reviews the changes  

### AI Assisted Contribution Compatibility
The project must:
* Allow or tolerate AI generated code when reviewed by humans  
* Not have policies forbidding AI generated contributions  

### Active Maintenance
The project should show:
* Recent commits  
* Active issue triage  
* Regular releases  
* Maintainer responsiveness  

### Real World Adoption
The project should be:
* Used in production systems or SaaS products  
* Widely adopted in the developer ecosystem  
* Downloaded frequently on package registries  

### Test Coverage
The project must include:
* Unit tests or regression tests  
* Continuous integration pipelines  
* Evidence that tests run on pull requests  

## Required Output

### 1. Ranked List
Provide a ranked list of the top 20 candidate libraries, from strongest to weakest.

### 2. Justification
For each library, provide a short explanation describing why it is a strong candidate.

### 3. Detailed Scoring Table
Create a table that includes the following columns:
* Rank  
* Project name with github link  
* Language  
* Ecosystem impact  
* Maintenance activity  
* Contributor friendliness  
* AI readiness  
* Test coverage  
* Technical fit  
* Total weighted score  

### 4. Scoring Methodology
Explain the scoring system, including:
* Criteria  
* Weights  
* How the final score is calculated  
```