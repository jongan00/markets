# Sportsbet Graduate Prep: Week-by-Week Checklist

**Window:** Mon 7 Sept 2026 to Sun 31 Jan 2027 (21 weeks). Start date: Mon 1 Feb 2027.
**Budget:** ~60 to 90 min weekdays, one 3 to 4 hr block each weekend day. Roughly 12 hrs/week.
**Target stack:** Java + Spring Boot, TypeScript + React, Node.js, Postgres, Git + GitHub Actions, Docker, AWS basics, testing at every layer.

## How to use this

- Tick items as you go. If a week runs over, push the remaining items into the next week rather than skipping them. Weeks 16 to 17 are deliberately light to absorb slippage.
- Every session ends with a 3-line log entry: what I did / what confused me / what's next. Keep it in `LOG.md` in the capstone repo.
- Rule for AI tools (Claude Code, Copilot, Cursor): you write the first version, then use the tool to review, explain, or generate tests. If you can't explain a line it produced, delete it and write it yourself.
- Warm-up (15 to 20 min) each weekday: one Exercism exercise, or re-read and annotate yesterday's code.

## The capstone: "Markets"

A small sports-markets app you grow across the whole plan.

- **markets-api** (Spring Boot + Postgres): fixtures, markets, selections/odds, mock bets. REST.
- **markets-web** (React + TypeScript): browse fixtures, view markets, add selections to a bet slip, place a mock bet.
- **odds-feed** (Node.js): emits odds changes on a timer; frontend consumes them live.
- Tests at every layer, GitHub Actions on every push, Docker Compose locally, one AWS deployment at the end.

Initial data model (week 5): `Sport` → `Competition` → `Fixture` (home, away, startTime, status) → `Market` (name, status) → `Selection` (name, decimalOdds, status). `Bet` (stake, placedAt, status) with `BetLeg` rows referencing selections and the odds at placement. Seed with the 2026 AFL finals and Spring Racing Carnival fixtures so it feels real.

## Core resource index

| Area | Resource |
|---|---|
| Java | dev.java/learn (Oracle's official tutorials), Exercism Java track, *Effective Java* (Bloch, 3rd ed.) |
| Spring | spring.io/guides, Spring Academy free courses (spring.academy), Baeldung |
| Testing (JVM) | JUnit 5 user guide, Mockito docs, testcontainers.com/guides |
| SQL | sqlbolt.com, pgexercises.com, use-the-index-luke.com |
| Git | *Pro Git* (git-scm.com/book), learngitbranching.js.org |
| TypeScript | TypeScript Handbook (typescriptlang.org), Total TypeScript free tutorials (totaltypescript.com) |
| React + Node | react.dev "Learn React", Full Stack Open (fullstackopen.com), Redux Toolkit "Essentials" tutorial, TanStack Query docs |
| Testing (web) | vitest.dev, testing-library.com, playwright.dev |
| Docker / CI | docs.docker.com "Get started", docs.github.com/actions |
| AWS | AWS Skill Builder free tier courses, AWS docs for ECS / Elastic Beanstalk / RDS |
| Kotlin | Kotlin Koans (play.kotlinlang.org/koans), spring.io Kotlin guide |
| System design | System Design Primer (github.com/donnemartin/system-design-primer), ByteByteGo blog |
| Practices | Google Engineering Practices "How to do a code review" (google.github.io/eng-practices), Atlassian Agile Coach |

---

## Phase 1: Hands working again (weeks 1 to 4)

### Week 1 (7 Sept): Environment and Java reboot
- [ ] Install: JDK (21 or 25, both LTS), IntelliJ IDEA Community, VS Code, Node LTS, Docker Desktop, Git, GitHub CLI (`gh`)
- [ ] GitHub account with SSH key; create `markets` repo (monorepo with `api/`, `web/`, `feed/` folders) with README and LOG.md
- [ ] Java: read dev.java "Getting Started" and "Java Language Basics"; write a console program that models fixtures and odds using records, enums, `List`/`Map`
- [ ] Exercism: join Java track, complete 5 exercises (Two Fer, Hamming, Raindrops, Isogram, Bob)
- [ ] Gradle: `gradle init` a project, understand `build.gradle.kts`, run tests from CLI
- Resources: dev.java/learn, exercism.org/tracks/java, docs.gradle.org "Getting started"

### Week 2 (14 Sept): Modern Java
- [ ] Streams, lambdas, `Optional`, generics, sealed interfaces, switch pattern matching
- [ ] Exceptions: checked vs unchecked, when to wrap, custom exception hierarchy
- [ ] Refactor week 1's console program to use streams and records properly; add JUnit 5 tests
- [ ] Exercism: 5 more (Word Count, Anagram, Grade School, Matrix, Robot Simulator)
- [ ] *Effective Java*: items 1 to 9 (creating/destroying objects) and 15 to 17 (immutability)
- [ ] Start using an AI tool for code review of your own solutions (rule above)
- Resources: dev.java "Using Lambda Expressions" and "The Stream API", Baeldung "Java Streams", JUnit 5 user guide

### Week 3 (21 Sept): Git properly, TypeScript introduced
- [ ] Learn Git Branching: all "Main" levels plus the remote levels
- [ ] Pro Git: chapters 2, 3, 7.6 (rewriting history)
- [ ] Practise: feature branches, interactive rebase, squash, conflict resolution, `git bisect`, `.gitignore`, conventional commit messages
- [ ] Write a PR template in the repo (What / Why / How tested)
- [ ] TypeScript: Handbook sections "The Basics", "Everyday Types", "Narrowing", "Functions", "Object Types"
- [ ] Total TypeScript free "Beginner's TypeScript" tutorial
- Resources: learngitbranching.js.org, git-scm.com/book, typescriptlang.org/docs/handbook, totaltypescript.com/tutorials

### Week 4 (28 Sept): Consolidate and TS depth
- [ ] TypeScript: generics, unions/discriminated unions, utility types (`Partial`, `Pick`, `Record`), `unknown` vs `any`, async/await with typed promises
- [ ] Port the week 2 domain model to TS in `feed/` as a small script that generates random odds movements and prints them
- [ ] Exercism TypeScript track: 5 exercises
- [ ] Consolidation weekend: re-read LOG.md, rewrite anything you couldn't explain from memory
- [ ] Email the Sportsbet grad coordinator: which stack for first rotation, any reading list, laptop/tooling expectations
- Resources: Handbook "Generics", "Utility Types"; exercism.org/tracks/typescript

---

## Phase 2: Backend (weeks 5 to 9)

### Week 5 (5 Oct): Spring Boot first API
- [ ] start.spring.io: Web, Validation, Data JPA, PostgreSQL driver, Actuator, Testcontainers, DevTools
- [ ] Spring Academy "Building a REST API with Spring Boot" (free)
- [ ] Implement data model from the capstone spec as JPA entities; `GET /fixtures`, `GET /fixtures/{id}`, `GET /fixtures/{id}/markets`
- [ ] Understand: `@RestController`, `@Service`, `@Repository`, constructor injection, `@Transactional`, profiles (`application-local.yml`)
- [ ] Run Postgres via Docker: `docker run -e POSTGRES_PASSWORD=... -p 5432:5432 postgres:16`
- Resources: spring.academy, spring.io/guides "Building a RESTful Web Service", "Accessing Data with JPA"

### Week 6 (12 Oct): SQL and persistence for real
- [ ] SQLBolt lessons 1 to 18; pgexercises "Basic" and "Joins"
- [ ] Flyway migrations replace `ddl-auto`; write V1 schema and V2 seed data
- [ ] Use The Index, Luke: chapters "Anatomy of an Index" and "The Where Clause"; add indexes on `fixture.start_time` and `market.fixture_id`, look at `EXPLAIN ANALYZE`
- [ ] JPA pitfalls: N+1 (fix with `@EntityGraph` or `JOIN FETCH`), lazy loading outside transactions, DTOs vs entities in responses
- [ ] Write 3 raw SQL queries with `JdbcClient`/`JdbcTemplate` (e.g. "markets with most selections per competition")
- Resources: sqlbolt.com, pgexercises.com, use-the-index-luke.com, flywaydb.org docs, Baeldung "N+1 problem in Hibernate"

### Week 7 (19 Oct): Writes, validation, errors
- [ ] `POST /bets` (stake, legs) with Bean Validation; reject closed selections; record odds at placement
- [ ] Global error handling with `@RestControllerAdvice` and RFC 7807 `ProblemDetail`
- [ ] Idempotency key on `POST /bets` (header, stored, replayed response). Betting systems care about this a lot.
- [ ] Pagination and sorting on list endpoints (`Pageable`)
- [ ] OpenAPI docs via springdoc; check Swagger UI renders
- Resources: Spring docs "Validation", "Error Handling" (ProblemDetail), springdoc.org, Stripe's idempotency blog post

### Week 8 (26 Oct): Testing the backend
- [ ] Unit tests for services with Mockito (`@ExtendWith(MockitoExtension.class)`)
- [ ] Web layer tests with `@WebMvcTest` + MockMvc
- [ ] Integration tests with `@SpringBootTest` + Testcontainers Postgres
- [ ] Test the idempotency and closed-selection rules explicitly
- [ ] Coverage report (JaCoCo). Aim for meaningful coverage of services and controllers, not a number.
- [ ] Spring Academy "Securing a REST API" first two modules only (know what a filter chain is; skip the rest)
- Resources: spring.io/guides "Testing the Web Layer", testcontainers.com/guides "Getting started with Testcontainers for Java", Mockito docs

### Week 9 (2 Nov): Docker and Actuator, backend done
- [ ] Docker "Get started" workshop parts 1 to 6
- [ ] Multi-stage Dockerfile for `api/`; `docker-compose.yml` with api + postgres
- [ ] Actuator: `/health`, `/info`, `/metrics`; add a custom health indicator for the DB
- [ ] Logging: SLF4J with Logback, consistent log lines with fixture/bet IDs; try Spring Boot's structured (JSON) logging
- [ ] Backend checkpoint: fresh clone, `docker compose up`, tests green, Swagger UI works. Fix anything that doesn't.
- Resources: docs.docker.com/get-started, Spring Boot docs "Actuator", "Logging" (structured logging section)

---

## Phase 3: Frontend and Node (weeks 10 to 14)

### Week 10 (9 Nov): React fundamentals
- [ ] react.dev "Learn React": "Describing the UI", "Adding Interactivity", "Managing State" (all of it, do the challenges)
- [ ] Vite + React + TS project in `web/`; ESLint + Prettier configured
- [ ] Build `FixtureList` and `FixtureCard` with hardcoded data; then fetch from your API (enable CORS in Spring for local)
- [ ] Learn: props, `useState`, `useEffect` (and why you'll use it less than you think), keys, lifting state
- Resources: react.dev/learn, vitejs.dev

### Week 11 (16 Nov): Data fetching, routing, state
- [ ] TanStack Query for server state: fixtures, markets; loading/error states; query keys
- [ ] React Router: `/`, `/fixtures/:id`
- [ ] Redux Toolkit "Essentials" tutorial parts 1 to 4; use RTK for the bet slip (client state), note when Query vs Redux fits
- [ ] Full Stack Open part 2 (communicating with server) as a cross-check
- [ ] Bet slip UI: add/remove selections, stake input, potential return calc
- Resources: tanstack.com/query, reactrouter.com, redux.js.org/tutorials/essentials, fullstackopen.com

### Week 12 (23 Nov): Forms, types, testing the frontend
- [ ] Place bet flow with React Hook Form + Zod validation; handle API errors (ProblemDetail) in the UI
- [ ] Generate TS types from your OpenAPI spec (openapi-typescript) so front and back agree
- [ ] Vitest + React Testing Library: test `FixtureCard`, bet slip reducer, place-bet form
- [ ] Mock the API in tests with MSW
- [ ] Accessibility pass: labels, keyboard nav, focus after placing a bet (their ad says "accessible")
- Resources: react-hook-form.com, zod.dev, vitest.dev, testing-library.com/docs/react-testing-library, mswjs.io

### Week 13 (30 Nov): Node.js odds feed
- [ ] Full Stack Open part 3 (Node/Express) or Fastify "Getting started" (pick one, Fastify is more current)
- [ ] `feed/` service in TS: every few seconds, pick random selections and drift odds; expose SSE endpoint `GET /odds/stream`
- [ ] Persist changes by calling `PATCH /selections/{id}/odds` on the Spring API (add that endpoint)
- [ ] Frontend subscribes to the stream and updates odds in place; show a flash on change
- [ ] Node testing with Vitest; Dockerfile for `feed/`; add to compose
- Resources: fullstackopen.com part 3, fastify.dev, MDN "Using server-sent events"

### Week 14 (7 Dec): End-to-end and frontend checkpoint
- [ ] Playwright: two e2e tests (browse a fixture, place a bet) against the compose stack
- [ ] Error boundaries, empty states, suspicious-input handling (negative stake, odds changed since slip)
- [ ] Read bulletproof-react (github.com/alan2207/bulletproof-react) and reorganise `web/` to a feature-based structure
- [ ] Frontend checkpoint: fresh clone, `docker compose up`, `npm test`, `npx playwright test` all green
- [ ] Consolidation weekend: rewrite LOG.md notes you can't explain from memory
- Resources: playwright.dev/docs/intro, bulletproof-react

---

## Phase 4: Production shape (weeks 15 to 18, lighter over Christmas)

### Week 15 (14 Dec): CI with GitHub Actions
- [ ] Actions quickstart; workflow per service: build, lint, test on every PR; matrix or path filters so only changed services run
- [ ] Testcontainers in CI (Docker is available on ubuntu runners)
- [ ] Branch protection on `main`: PR required, checks must pass
- [ ] Dependabot enabled; merge one Dependabot PR properly (read the changelog first)
- [ ] Cache Gradle and npm in workflows
- Resources: docs.github.com/actions "Quickstart", "Building and testing Java with Gradle", "Building and testing Node.js"

### Week 16 (21 Dec): AWS basics, then stop
- [ ] AWS account with budget alarm set to a few dollars; IAM user, no root use
- [ ] AWS Skill Builder: "AWS Cloud Practitioner Essentials" modules on compute, storage, networking, databases only (roughly 3 hrs)
- [ ] Deploy `markets-api` with Elastic Beanstalk (simplest) or ECS Fargate (closer to real), RDS Postgres, CloudWatch logs
- [ ] **Take Christmas week off from this plan (24 to 28 Dec at minimum).**
- Resources: skillbuilder.aws, AWS docs "Getting started with Elastic Beanstalk" / "Getting started with Amazon ECS"

### Week 17 (28 Dec): Light week
- [ ] Optional: deploy `web/` to S3 + CloudFront, or Vercel/Netlify if AWS is fighting you
- [ ] Optional: GitHub Actions deploy-on-merge for the API using OIDC (no long-lived AWS keys)
- [ ] Read only: Atlassian Agile Coach "Scrum" and "Kanban" pages, "How to do a code review" (Google eng practices)
- [ ] Tear down anything costing money before the new year

### Week 18 (4 Jan): Observability and resilience
- [ ] Micrometer metrics from Actuator; count bets placed, time the place-bet path
- [ ] Run Prometheus + Grafana in compose; one dashboard, one alert rule (error rate on `POST /bets`)
- [ ] Correlation IDs across web → api → feed logs
- [ ] Simulate a live event: script that hammers `POST /bets`; watch the dashboard; find the bottleneck
- [ ] Health checks and graceful shutdown in Docker
- Resources: Spring Boot docs "Metrics", grafana.com/docs "Get started", prometheus.io "Getting started"

---

## Phase 5: Taper and widen (weeks 19 to 21)

### Week 19 (11 Jan): Kotlin and code reading
- [ ] Kotlin Koans: Introduction, Classes, Conventions, Collections
- [ ] Convert one Spring service (e.g. bet placement) to Kotlin in a branch; note what got shorter
- [ ] Read Spring PetClinic (github.com/spring-projects/spring-petclinic): trace "create a visit" from controller to DB
- [ ] Read one mature React/TS codebase (e.g. Excalidraw or Cal.com): trace one feature end to end
- Resources: play.kotlinlang.org/koans, spring.io/guides "Building web applications with Spring Boot and Kotlin"

### Week 20 (18 Jan): System design at grad level
- [ ] System Design Primer: sections on scalability, load balancing, caching, CDN, queues, consistency
- [ ] Sketch on paper: how "place a bet during the Grand Final" flows through LB → API → DB → queue; where idempotency, caching and rate limiting sit; what you'd monitor
- [ ] Read about microservices basics: sync vs async, why teams use Kafka/SQS (concepts only, don't build)
- [ ] Refactor capstone: remove dead code, tidy names, one README per service with "how to run" and "how it's tested"
- Resources: system-design-primer, ByteByteGo blog, Sam Newman "Building Microservices" chapters 1 to 2 (optional)

### Week 21 (25 Jan): Land it
- [ ] Final capstone walkthrough: record yourself explaining the architecture in 5 minutes, then in 90 seconds
- [ ] Rehearse your "what have you built" story: AMOG HAZOP app (refactor, GitLab CI) and Markets (stack, tests, deploy)
- [ ] Skim: git commands cheat sheet, Spring annotations cheat sheet, React hooks cheat sheet
- [ ] Set up a "day one" note: questions to ask (repo access, local setup docs, team norms for PRs, who to pair with)
- [ ] Rest. Finish Thursday. Do nothing technical on the weekend before 1 Feb.

---

## Not on this list, on purpose

LeetCode grind, .NET, React Native, Kafka/Kubernetes beyond concepts, certifications, any second course on a topic already covered. If a rotation needs one of these, you'll learn it at work with support.
