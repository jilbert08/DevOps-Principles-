# DevOps Principles, History, and CI/CD

## 1. Executive summary
DevOps combines cultural practices, engineering methods, and automation to help development and operations teams deliver software safely and continuously. It reduces hand-offs and encourages shared responsibility for building, deploying, operating, and improving a service. DevOps is not simply a toolset or a job title: it is a way of working that joins people, processes, and technology.

## 2. A short history: Waterfall to Agile to DevOps
### Traditional Waterfall
Waterfall is a sequential approach. Teams commonly complete requirements, design, implementation, testing, and release in distinct phases. It can work when requirements are stable, but late testing or long release cycles can make feedback slow and changes expensive. Development and operations may work in separate silos, with software “thrown over the wall” for deployment.

### Agile
Agile emerged as a response to the cost of long feedback cycles and rigid plans. Work is divided into smaller increments, teams collaborate with stakeholders, and priorities can be adjusted using feedback. Agile improves the development loop, but by itself it does not guarantee that code can be built, tested, released, and operated reliably.

### DevOps
DevOps grew from the need to connect development speed with operational stability. Its growth in the late 2000s and early 2010s was influenced by Agile, Lean thinking, continuous delivery, infrastructure automation, cloud computing, and collaboration between development and operations communities. The term is commonly associated with the first DevOpsDays event in 2009. Exact adoption timelines differ by organization; DevOps developed as a movement rather than through one single invention.

### Comparison
| Approach | Typical planning and delivery | Feedback | Team relationship | Common risk |
|---|---|---|---|---|
| Waterfall | Large sequential phases | Often late | Functional hand-offs | Defects or changed needs discovered late |
| Agile | Small iterations/sprints | Frequent stakeholder feedback | Cross-functional product team | Operations/release work may still be a bottleneck |
| DevOps | Continuous, automated delivery where appropriate | Feedback from tests and production | Development, operations, security and product share responsibility | Poorly designed automation can spread mistakes quickly |

These are broad tendencies, not strict rules. Organizations may combine approaches.

## 3. The Three Ways of DevOps
The Three Ways are principles described in *The DevOps Handbook*. They are more important than any specific tool.

### First Way — Flow
Optimize the entire value stream from an idea or code change to a customer receiving value. Make work visible, reduce batch sizes, automate repeatable steps, remove queues and hand-offs, and build quality into the process.
**Example:** Every pull request triggers an automated build and test suite, so problems are discovered before merging.

### Second Way — Feedback
Create fast, clear feedback loops from every stage, including production, back to the people who can act on it. Use tests, logs, metrics, traces, alerts, customer feedback, and incident reviews to detect and correct problems.
**Example:** A deployment increases error rates; monitoring alerts the team, which rolls back and fixes the cause.

### Third Way — Continual Learning and Experimentation
Build a learning culture where teams share knowledge, run safe experiments, practice recovery, and improve the system after incidents without focusing on blame. Document lessons and spread them across teams.
**Example:** After an outage, a blameless review identifies a missing health check and the team adds it to all relevant services.

The Three Ways reinforce each other: flow creates more opportunities for feedback; feedback guides learning; learning improves the flow.

## 4. CI, Continuous Delivery, and Continuous Deployment
- **Continuous Integration (CI):** Developers merge small changes frequently. Automated builds and tests check each change and reveal integration problems early.
- **Continuous Delivery:** Changes are built, tested, and kept in a releasable state. Production release may require a human approval.
- **Continuous Deployment:** Every change that passes the required automated checks is automatically deployed to production. This requires strong testing, observability, and rollback or recovery practices.

CI/CD is not a promise that every change should go live immediately. Teams should choose controls based on risk, regulation, and service needs.

## 5. Typical CI/CD pipeline lifecycle
1. **Plan:** Define a user need, acceptance criteria, and work item.
2. **Code:** Implement a small change in version control; use peer review and branch protection.
3. **Build:** Compile/package the application and create versioned artifacts.
4. **Test:** Run unit, integration, API, end-to-end, security, and quality checks as appropriate.
5. **Package:** Store artifacts or container images in a registry; scan and sign where supported.
6. **Deploy to test/staging:** Deploy consistently and run smoke or acceptance tests.
7. **Approval / release gate (optional):** Apply human approval, change controls, or policy checks where needed.
8. **Deploy to production:** Use strategies such as rolling, blue-green, or canary deployment where appropriate.
9. **Observe:** Collect logs, metrics, traces, and user signals; alert on actionable service-level objectives.
10. **Learn and improve:** Roll back or mitigate if necessary, review outcomes, and feed lessons into the backlog.

### Example tool mapping
| Stage | Possible tools | What they do |
|---|---|---|
| Source control and review | Git, GitHub/GitLab | Track changes and review code |
| CI orchestration | GitHub Actions, Jenkins | Run workflow jobs |
| Build and test | Maven, Gradle, pytest, JUnit | Build software and validate behavior |
| Security checks | Dependabot, CodeQL, Trivy, SAST/DAST tools | Find vulnerable dependencies, code patterns, or images |
| Configuration and automation | Ansible | Configure systems and automate operational tasks |
| Containers | Docker | Build and run container images |
| Orchestration | Kubernetes | Schedule and manage containerized workloads |
| Infrastructure as Code | Terraform | Define and provision infrastructure declaratively |
| Observability | Prometheus, Grafana, OpenTelemetry | Collect/visualize metrics and traces; support diagnosis |
| Artifact storage | Container/image or package registry | Store versioned deliverables |

Tools overlap and the exact choice depends on the platform, budget, team skills, compliance needs, and existing systems.

## 6. Benefits
- Shorter and more predictable delivery cycles
- Earlier detection of defects and security issues
- Repeatable deployments and less manual work
- Shared ownership and fewer “throw it over the wall” hand-offs
- Better visibility into service health
- Faster recovery through monitoring, rollback, and incident learning
- More time for improvement by automating repetitive tasks

## 7. Challenges and good practices
**Challenges:** legacy systems, fragmented ownership, brittle tests, excessive permissions, secrets leakage, alert fatigue, tool sprawl, and automating a bad process.

**Good practices:**
- Start with one small service or workflow and measure results.
- Keep pipelines version-controlled and reproducible.
- Protect secrets; use least privilege and short-lived credentials when possible.
- Make tests meaningful and keep them maintainable.
- Add security throughout the lifecycle (“shift left”), not only at release time.
- Use staged rollouts and tested rollback/recovery procedures.
- Define service-level indicators/objectives and alert on user-impacting symptoms.
- Review incidents without blame and turn findings into tracked actions.

## 8. Suggested success metrics
Use a balanced set rather than optimizing only for deployment speed:
- Deployment frequency
- Lead time for changes
- Change failure rate
- Time to restore service
- Build/test duration and failure rate
- Availability, latency, error rate, and saturation
- Security findings and time to remediate
- Customer outcomes and developer experience

Metrics should guide learning, not be used to punish teams.

## 9. Conclusion
DevOps connects development, operations, and related functions around delivering and operating reliable software. Agile encourages small increments; CI/CD automates checks and delivery; observability creates feedback; and continual learning turns experience into improvement. The best toolchain is the one that supports the team’s goals with appropriate security and operational controls.

## References
1. Atlassian, “How do Agile and DevOps interrelate?” https://www.atlassian.com/agile/devops
2. Microsoft Learn, “What is Agile development?” https://learn.microsoft.com/en-us/devops/plan/what-is-agile-development
3. GitHub Docs, “Understanding GitHub Actions.” https://docs.github.com/en/actions/get-started/understanding-github-actions
4. Jenkins documentation. https://www.jenkins.io/doc/
5. Ansible documentation. https://docs.ansible.com/
6. Docker documentation. https://docs.docker.com/
7. Kubernetes documentation. https://kubernetes.io/docs/home/
8. Terraform documentation. https://developer.hashicorp.com/terraform/docs
9. Prometheus documentation. https://prometheus.io/docs/introduction/overview/
10. Grafana documentation. https://grafana.com/docs/
11. Kim, G., Humble, J., Debois, P., Willis, J. and Forsgren, N. *The DevOps Handbook*, 2nd edition, IT Revolution, 2021. https://www.oreilly.com/library/view/the-devops-handbook/9781098182281/

