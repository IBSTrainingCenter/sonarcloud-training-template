# Trainer notes

Outline for walking students through the SonarCloud setup. The student-facing
instructions live in `README.md`.

## Talking points
1. **`sonar-project.properties`** — show and explain each line:
   - `projectKey` / `organization` — unique per SonarCloud account (students fill these in).
   - `sources` / `tests` / `java.binaries` / `junit.reportPaths` — what Sonar analyzes.
   - `sonar.exclusions` — files ignored by the analyzers (`model/**`).
   - `sonar.coverage.exclusions` — analyzed but excluded from coverage (`DemoApplication`).
2. **`.github/workflows/sonarcloud.yml`** — explain the CI steps:
   checkout with `fetch-depth: 0` → build & test with Maven → `sonarqube-scan-action`
   reads `sonar-project.properties`. Note `SONAR_TOKEN` comes from repo secrets.
3. **GitHub configuration** — where `SONAR_TOKEN` lives, when the workflow triggers
   (push to main/master, and pull requests).
4. **Automatic Analysis OFF** — must be disabled so CI analysis is the single method.

## Common pitfalls to highlight
- Forgetting to disable Automatic Analysis → conflicting analyses.
- Wrong `projectKey`/`organization` → analysis lands in the wrong (or no) project.
- Missing `SONAR_TOKEN` secret → workflow fails at the scan step.

## Optional extensions (not included by default)
- Add JaCoCo so real coverage shows up in SonarCloud
  (currently `sonar.coverage.exclusions` is set but no coverage engine runs).
- Introduce a couple of intentional code smells / bugs for students to find in the report.
