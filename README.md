# SonarCloud Training Template

A small Spring Boot project used to practice **SonarCloud** analysis via GitHub Actions:
- minimal Employee CRUD API
- JPA + PostgreSQL
- integration test with Testcontainers (Docker Postgres)

## Requirements
- Java 21+
- Docker Desktop (for the integration tests)
- A GitHub account and a free [SonarCloud](https://sonarcloud.io) account

## Connect this project to your SonarCloud

Follow these steps to get your own analysis running.

1. **Use this template** → create your own repository from it (green "Use this template" button on GitHub).

2. **Create an organization and a project in SonarCloud**
   - Sign in to https://sonarcloud.io with your GitHub account.
   - Create an organization, then create a project for this repository.
   - Copy your **Project Key** and **Organization Key**.

3. **Put your keys into `sonar-project.properties`**
   ```properties
   sonar.projectKey=<your-project-key>
   sonar.organization=<your-organization>
   ```

4. **Turn OFF Automatic Analysis** in SonarCloud
   - Project → *Administration* → *Analysis Method* → disable **Automatic Analysis**.
   - This is required, otherwise it conflicts with the CI-based analysis in this repo.

5. **Add the `SONAR_TOKEN` secret in GitHub**
   - In SonarCloud: *My Account* → *Security* → generate a token.
   - In GitHub: *Settings* → *Secrets and variables* → *Actions* → **New repository secret**
     named `SONAR_TOKEN`.

6. **Push and view results**
   - `git commit` + `git push` (or open a pull request).
   - Open the **Actions** tab, wait for the *SonarCloud Analysis* workflow to finish,
     then check your project on https://sonarcloud.io.

## How the analysis is wired
- `sonar-project.properties` — the single source of Sonar settings (keys, sources, exclusions).
- `.github/workflows/sonarcloud.yml` — builds/tests the project, then runs the
  SonarCloud scan which reads `sonar-project.properties`.

## Run tests locally
```
./mvnw test
```

## Run the app locally
Set DB env vars (or run a local Postgres on `localhost:5432`):
- `DB_URL`
- `DB_USERNAME`
- `DB_PASSWORD`

Then:
```
./mvnw spring-boot:run
```

## API
Base URL: `/api/v1/employees`
- `GET    /api/v1/employees`
- `GET    /api/v1/employees/{id}`
- `POST   /api/v1/employees`
- `PUT    /api/v1/employees/{id}`
- `DELETE /api/v1/employees/{id}`
