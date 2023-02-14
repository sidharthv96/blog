+++
title = "Resume"
date = "2020-04-09"
+++

To get in touch, drop a mail to [hi@sidharth.dev](mailto:hi@sidharth.dev)

# Professional Experience

{{< experience company="MermaidChart" position="Founding Engineer" start="October '22" end="Present" url="https://www.mermaidchart.com">}}

- Taking Mermaid beyond the live editor to a full fledged collaboration platform.
- Backed by Sid Sijbrandij (Co-Founder and CEO of GitLab) via [Open Core Ventures](https://opencoreventures.com/)

{{< experience company="TurgenSec" position="CTO" start="March '21" end="October '22" url="https://https://web.archive.org/web/20221027171949/https://www.turgensec.com/">}}

[Acquired](https://web.archive.org/web/20221031205854/https://techround.co.uk/news/secretive-gchq-funded-company-turgensec-acquired/)
[(Do not ask who bought us.)](https://web.archive.org/web/20221027171949/https://www.turgensec.com/)

### DataShadow

- Building out an Offensive Privacy platform.

{{< experience company="Oracle" position="Senior Applications Engineer" start="June '18" end="March '21" url="https://www.oracle.com/">}}

{{< experience company="Helios-Webhooks" small="true" start="January '19" end="March '21">}}

{{< collapse summary="Lead developer of the service which facilitates to Integrate Webhooks functionality to any internal product with [CloudEvent](https://cloudevents.io/) spec" open="true" >}}

- **Microservices** (Java & Node.js on Kubernetes), Kafka, Vault, CI/CD (Gitlab, Jenkins & Helm)
- Multiple endpoint-authentication (Basic, HMAC, OAuth2.0, IDCS) support
- At least once delivery, Automatic Retries with exponential back off
- Endpoint blacklisting, Dead letter requeuing and Message expiry

{{< /collapse >}}

{{< experience company="Helios-Extensions" small="true" start="March '20" end="March '21">}}

{{< collapse summary="Allows customers to write custom code to act on system events using Webhooks and **Serverless** Platform (Oracle Fn)" >}}

- Designed the **multi tenancy architecture** which allows managing and running customer functions securely
- Created a **federated Docker registry proxy** service which allows customers to push containers with 0-config while managing access control and tenant data segregation.

{{< /collapse >}}

{{< experience company="Helios-Vision" small="true" start="September '19" end="March '21">}}

{{< collapse summary="Created a Typescript library to provide core functionality required to build a Microservice with Node.js" >}}

- Kafka - Avro schemas | Transparent message encryption with Vault
- HTTP endpoints - Express | Swagger
- Service AuthN/AuthZ - JWT | Vault
- Metrics & Health checks - Prometheus
- Dependency Injection, Easy structured logging, Comprehensive test coverage and test helpers

{{< /collapse >}}

{{< experience company="Element Manager" small="true" start="June '18" end="January '19" url="http://documentation.custhelp.com/euf/assets/devdocs/buiadmin/topicrefs/c_bui_Overview_Element_Manager.html">}}

{{< collapse summary="Product that supports Import/Export of Custom Elements like Reports, Workspaces, etc in Oracle Service Cloud" >}}

- Redesigned the UI to improve UX
- Created a **Generic Framework** to standardize Metadata management for multiple types of objects.
- Developed a [Jenkins Pipeline](https://blogs.oracle.com/cx/this-is-why-customers-love-oracle-cx-service-element-manager-for-b2c) to automate exports and imports for different sites using Element Manager Public API

{{< /collapse >}}

# Open Source

I'm an avid open source advocate and have contributed in a small capacity to multiple projects.

Maintainer of [Mermaid JS](https://github.com/mermaid-js/mermaid) and [Mermaid Live Editor](https://github.com/mermaid-js/mermaid-live-editor).

| Project&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;                                          | Stars&nbsp;&nbsp;&nbsp;&nbsp;                                                                | Description                                          |
| ------------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------- | ---------------------------------------------------- |
| [Mermaid JS](https://github.com/mermaid-js/mermaid/pulls?q=is%3Apr+author%3Asidharthv96+)        | ![GitHub stars](https://img.shields.io/github/stars/mermaid-js/mermaid?style=social&label)   | Markdown inspired diagrams for all                   |
| [Prettier](https://github.com/prettier/prettier/pulls?q=is%3Apr+author%3Asidharthv96+)           | ![GitHub stars](https://img.shields.io/github/stars/prettier/prettier?style=social&label)    | An opinionated code formatter                        |
| [Typescript](https://github.com/microsoft/TypeScript/pulls?q=is%3Apr+author%3Asidharthv96+)      | ![GitHub stars](https://img.shields.io/github/stars/microsoft/TypeScript?style=social&label) | TypeScript is a superset of JavaScript               |
| [Svelte Kit](https://github.com/sveltejs/kit/pulls?q=is%3Apr+author%3Asidharthv96+)              | ![GitHub stars](https://img.shields.io/github/stars/sveltejs/kit?style=social&label)         | Cybernetically enhanced web apps                     |
| [Homebrew \| Brew.sh](https://github.com/Homebrew/brew.sh/pulls?q=is%3Apr+author%3Asidharthv96+) | ![GitHub stars](https://img.shields.io/github/stars/Homebrew/brew.sh?style=social&label)     | The Homebrew homepage                                |
| [Caprover](https://github.com/caprover/caprover/pulls?q=is%3Apr+author%3Asidharthv96)            | ![GitHub stars](https://img.shields.io/github/stars/caprover/caprover?style=social&label)    | Automated Scalable PaaS Package - Heroku on Steroids |

Minor PRs in [Deno](https://github.com/denoland/deno/pulls?q=is%3Apr+author%3Asidharthv96+), [Strapi](https://github.com/strapi/strapi/pulls?q=is%3Apr+author%3Asidharthv96), [Manta](https://github.com/hql287/Manta/pulls?q=is%3Apr+author%3Asidharthv96)

# Tech

- Languages : TypeScript/JavaScript, Java, Python
- Backend : SvelteKit, Express, Spring
- UI : Svelte, Vue, JET
- Testing : Vitest, Jest, K6, JUnit
- Services : Kafka, PostgreSQL, Vault, Swagger, Supabase
- Infra : Docker, Kubernetes, AWS, OCI, Helm, Github Actions, Gitlab CI, Jenkins
- IoT : ESP32, Arduino, RC522 RFID

# Education

[Government Engineering College, Thrissur](http://gectcr.ac.in/) (2014-2018)

- Bachelor of Technology, Computer Science and Engineering

# Projects

#### Mermaid Live Editor - Maintainer

- Overhauled the old editor focusing on Design and UX.
  {{< youtube w7P_9NSRrOs >}}
- Setup a CI/CD Pipeline with Beta deploy.

#### Engineering Spot Allotment - Kerala Government

- Developed system to allot 1000+ students to seats in Government Colleges based on multiple allotment and reservation rules.
- Reduced the runtime from **45+ Min to ~1 Min**

#### CX-Hyperconnect Hackathon

- Managed Pan India event successfully
- Created system with
  - Participant Registration, Team Formations, Idea Wall
  - Multiple Judgement Panels with Different Point systems, Non-Colliding Time slots for Teams, Volunteer Co-ordination Reports
  - Promotional Games to drive engagement

#### Automated-OSINT - [Turgensec UK](https://community.turgensec.com/) (Consultancy)

- Revamped the intelligence gathering tool to handle multiple data sources
- Added company details data scraper

#### Hello KEPA

- Developed application for Kerala Police to sync Official contacts across devices and send notifications

#### Fuelive

- Developed application tracking district level fuel prices in India. 50K Downloads

# Hackathons

## Best Hack, Oracle Service Cloud Hackathon, 2019

**Object Versioning**

Versioning of OSvC Object metadata into Object Storage in OCI (Cloud Native Managed Services) using a Webhooks Adapter MicroService.

## Honorable Mention - Best Productivity, Oracle Service Cloud Hackathon, 2019

**Serverless Jenkins**

Run Jenkins as a Service on demand using the OCI platform. Developer collaboration is done using Slack.
