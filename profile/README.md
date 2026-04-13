### Welcome

:suspect: My name is Victor, and this is my professional portfolio that contains different repositories to showcase my skills to the interested.

In the following of this README, you will find my soft & hard skills that will give you an oversight of what I am capable of when working in a professional environment.

> French school taugh me to avoid being wrong at all cost. My professional experience with Ukrainians teammates told me otherwise. Now I like being wrong and to own it, it motivates me learning and improve.

### :handshake: Soft skills

<details>
    <summary>Who are you dealing with ?</summary>
    
- I'm a **very** collaborative teammate, I work with people every day with passion and smile on my face, _especially when we are firefighting in production_. I'm highly communicative (verbally and in writing), if there is a tension, I'm going to talk to you about it, even if you would rather avoid it :feelsgood:.
- Working with other people is **essential** for me. Sitting alone in a corner would slowly kill me. Developping software alone is **slow**, **lacks** of knowledge **sharing**, **not challenging**, and frankly... **sad**.
- I am a proactive engineer, I will raise concerns, share ideas, and will assume any responsability you want me to take. I've led teams accross the world (mostly Ukraine, Portugal, India and some from the United-States), and we always managed to deliver applications that built trust and credibility :fire:.
- I'm **not** an **over**-engineer. I know time is a **very valuable** resource, and I will always evaluate the tradeoffs and think before building or validating any part of a software. I am never going to spend multiple days on insignificant task, just for the fun of it. I am not a cat chasing butterflies.
- I pay attention to detail. You'll probably wonder how I spotted something in your PR that you missed.
- I love input from others, I dislike building something alone: I know I could be missing something obvious to someone else. (Now we have AI, and itr surely helped me to give me an oversight during the building iterations of this portfolio)
- I love solving problems. That's what engineering is about. Repetitive tasks with no reasoning aren't my thing. I naturally lean toward the hardest problems first.
> :arrow_right_hook: In some scenarios where priority is onto the most boring task, I've been told that it can be considered as a weakness. And I agree, that's why I am still doing these boring tasks when needed.
- Do you want to onboard me on a tech I don't know yet ? No problem. Give me _`<timescale according to complexity of the subject goes here>`_ of experiment and I will have strong basics. I've done this many times before, even in here with my Homelab (check hard skills section).
- My main goal will always be client satification :100:
- There is a high chance that I send GIF memes to my coworkers, I find this very effective to communicate emotions :trollface:.

</details>

### :computer: Hard skills

#### :bulb: Idea

To showcase infrastructure and platform engineering skills with real, working examples rather than hello worlds, I built a personal Kubernetes homelab deployed on a VPS.

The goal: a self-hosted, always-on platform where I can deploy, test, and iterate on anything — provisioned with OpenTofu, managed with GitOps.

##### :package: Repositories

- [Homelab](https://github.com/VictorMalodPortfolio/Homelab): OVH VPS provisioning, k3s cluster, Helm charts, and ArgoCD GitOps configuration — the full platform, end to end
- [DockerTooling](https://github.com/VictorMalodPortfolio/DockerTooling): Dockerfile for an isolated, reproducible development environment with all necessary tooling pre-installed

```mermaid
graph TD
    dev["💻 Developer"]

    subgraph local["Local Machine"]
        tooling["DockerTooling container\nkubectl · helm · tofu · sops"]
        age["age key"]
        kubeconfig["kubeconfig"]
    end

    subgraph github["GitHub"]
        homelab_repo["Homelab repo"]
        docker_repo["DockerTooling repo"]
        ghcr_tooling["GHCR\nk8s-tooling"]
        ghcr_reposerver["GHCR\nargocd-repo-server"]
    end

    subgraph ovh["OVH"]
        dns["DNS\nvictor-malod.ovh"]
        s3["Object Storage\nTofu state"]

        subgraph vps["VPS · Ubuntu 24.04 · k3s"]
            argocd["ArgoCD\nApp of Apps"]
            helm_secrets["helm-secrets\n+ SOPS + age"]
            cert_manager["cert-manager"]
            webhook["OVH webhook"]
            traefik["Traefik\ningress"]
            authelia["Authelia\nOIDC + ForwardAuth"]
            ovh_secret["Secret: ovh-credentials"]
            tls_secret["Secret: wildcard TLS"]
        end
    end

    subgraph le["Let's Encrypt"]
        acme["ACME v2"]
    end

    dev -->|push| homelab_repo
    dev -->|push| docker_repo
    docker_repo -->|CI builds| ghcr_tooling
    homelab_repo -->|CI builds| ghcr_reposerver
    homelab_repo -->|GitOps sync| argocd
    argocd -->|decrypts secrets| helm_secrets
    argocd -->|deploys| cert_manager
    argocd -->|deploys| webhook
    argocd -->|deploys| traefik
    argocd -->|deploys| authelia
    argocd -->|deploys| ovh_secret
    tooling -->|tofu apply| vps
    tooling -->|tofu apply| dns
    tooling -->|state| s3
    age -->|decrypt secrets| tooling
    kubeconfig -->|cluster access| tooling
    webhook -->|reads| ovh_secret
    webhook -->|creates TXT record| dns
    acme -->|verifies TXT| dns
    acme -->|issues cert| cert_manager
    cert_manager -->|stores| tls_secret
    traefik -->|serves TLS| tls_secret
    authelia -->|OIDC SSO| argocd
    traefik -->|ForwardAuth| authelia
```

#### :toolbox: Tools

In order to keep track of the stuff I've played around with, I've built this list of programming languages, frameworks, IaC, monitoring, security and quality tools. That I've liked to use during my DevSecOps iterations.  

<details>
    <summary>:scroll: The programing languages that I've liked using</summary>

- C# 
- Go 
- Java
- Python
- C
- GSC

</details>

<details>
    <summary>:classical_building: The frameworks I have worked with</summary>

- .NET (including Framework & Core): 
  - Aspire 
  - ASP.NET
  - Entity Framework
  - xUnit 
  - Blazor
- Azure: 
  - .NET SDK (including emulators)
  - App Service
  - Functions (previously WebJobs)
  - LogicApps
- Open Telemetry
- Go:
  - Testify
  - Benthos (now Redpanda-Connect)
- Black Ops 3 Mod Tools
<!-- AWS: -->
<!-- OVH: -->

</details>

<details>
    <summary>:building_construction: IaC tools I've used</summary>

- OpenTofu / Terraform
- Helm
- ARM Template
<!-- ansible -->
<!-- Bicep -->

</details>

<details>
    <summary>:whale: Containerization & Registries</summary>

- Kubernetes (k3s)
- Docker
- GitHub Container Registry (GHCR)
- Azure Container Apps
- Azure Container Instance (yikes)
- Azure Container Registries
- JFrog Artifactory

</details>

<details>
    <summary>:arrows_counterclockwise: CI/CD</summary>

- Azure DevOps pipelines (& release)
- GitHub actions

</details>

<details>
    <summary>:closed_lock_with_key: Quality & Security</summary>

- SonarQube
- Trivy
- BlackDuck
- Sops

</details>

<details>
    <summary>:bar_chart: Monitoring & Observability</summary>

- OpenTelemetry (in .NET Aspire & Azure AppInsights)
- Grafana 
- Grafana OTel Stack (Tempo / Loki / Prometheus)
- Dynatrace
- Jaeger
- Log4Net
- Azure AppInsights's .NET TelemetryClient

</details>

<img src="https://komarev.com/ghpvc/?username=VictorMalodPortfolio&label=Profile%20views&color=03d4ff&style=flat" alt="VictorMalodPortfolio" />

