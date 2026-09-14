---
title: "When the Agent Harness Becomes a Service"
subtitle: "OpenAI’s Agents API and the architecture of governed agentic work"
description: "How endpoint-local and shared agent harnesses differ, why deployment boundaries matter, and a proposal for a Site-deployable Agents API."
publishDate: 2026-09-14
tags:
  - AI
  - Agentic Workspaces
  - Enterprise Architecture
draft: false
---

OpenAI’s Agents API makes an important architectural separation concrete: the harness that coordinates agentic work can be operated as a service, independently of the environment where its tools execute.

For the enterprise, the significance is not simply that another component can move to the cloud. Orchestration can remain close to a particular working environment or become a shared service across approved resources. Its placement and operator can change without changing the organization’s responsibility for the work.

Those decisions should not be collapsed into a simple choice between “local” and “cloud.” An organization can operate its own harness service in a cloud environment. A provider-managed harness can invoke tools on a local endpoint. And either arrangement may use a remotely hosted model.

**The Workspace should govern the complete arrangement—not infer its authority or data boundary from a deployment label.**

## What OpenAI makes available

In its [September 10 announcement](https://openai.com/index/introducing-the-agents-api/), OpenAI introduced the Agents API in public beta, making the Codex harness available as a managed service. The harness supplies the machinery around the model: coordinating context, tool use and the progression of work.

OpenAI’s [architecture documentation](https://developers.openai.com/api/docs/guides/agents-api/architecture) explicitly separates the hosted harness, execution environment and application server. The execution environment may be a remote sandbox, a laptop or a container. When customers provide that environment, they manage its lifecycle and preserved files, while OpenAI continues to operate the harness.

A managed harness is a valuable building block. An enterprise should not have to recreate agent orchestration merely to retain authority over its work. Providers and execution platforms already contribute important controls; the question is how those controls compose into the organization’s approved working arrangement.

## Continuing the Agentic Workspace model

In [From Chatbot to Agentic Endpoint, and Beyond](https://yy8402.github.io/blog/agentic-ai-workspace/), we argued that AI work is not location-neutral. Some requests need only a model. Others need bounded sandbox execution. Still others depend on a persistent, configured environment with installed applications, authenticated state, files, tools and permitted network access.

That is the role of the Agentic Endpoint. The Chat / Command Layer should select the smallest suitable execution context, rather than send every request to an endpoint.

In [Cloudflare OS and Agentic Workspace](https://yy8402.github.io/blog/cloudflare-os-and-agentic-workspace/), we extended the argument to the organizational boundary. Cloudflare OS illustrated an emerging persistent Workspace, not simply a disposable sandbox. Our complementary premise was that the Workspace should govern the complete task profile across approved agents, model routes, capabilities, execution Sites, human-control points and evidence.

In our architecture, a Site is an approved execution and data-locality boundary. A service may serve a Site without residing inside it; authorizing that service does not move its processing into the Site. We also distinguished the Session’s origin Site from the Task’s execution Site. Their separation does not authorize unrestricted movement between them.

Harness placement belongs within that existing framework. It does not replace the Workspace, Session or Site with a new authority. It makes the operator and location of orchestration explicit alongside the other elements of the approved agent profile.

## The harness: endpoint-local or a shared service?

An endpoint-local harness and a shared service organize work differently. The distinction concerns how orchestration relates to the working environment, not whether the machine is physically on premises or in a cloud.

### Endpoint-local orchestration

An endpoint-local harness runs beside the persistent environment its agent operates. It is well suited to work that depends on that environment’s applications, configured tools, authenticated sessions or ongoing state.

Dependence on endpoint state establishes the need for that execution environment, not necessarily for a colocated harness. A remote harness may operate it through a supported executor; an endpoint-local agent is a separate integration choice.

This proximity can make co-work more direct: the user and agent can participate in the same environment, with suitable display and control integration. It also removes the need for a remote orchestration hop for local tool calls, though model calls may still cross a network. Overall performance must be measured, not inferred from locality.

The advantage comes with responsibility. Harness installation, updates, configuration and recovery must be managed across endpoints. Work depends on the availability of the relevant endpoint, whether that is a laptop, server or persistent cloud machine. Access to useful local state can also expose more than a task needs unless permissions and isolation narrow it.

Anthropic’s [discussion of containment across Claude products](https://www.anthropic.com/engineering/how-we-contain-claude) illustrates this tension: local filesystem, shell and network access makes an agent useful, but requires deliberate containment rather than reliance on supervision alone. Locality is not a security boundary by itself.

### Shared harness service

A shared harness service supplies orchestration to multiple separately authorized tasks and execution environments. Unlike an endpoint-local harness, it is not tied to one persistent working environment. Whether it serves resources within one Site or across explicitly authorized Sites is a separate placement and governance decision.

These are common operating patterns rather than mutually exclusive runtime types. An endpoint-local harness can support multiple sessions, while a shared service can support separately scoped sessions and tasks on common infrastructure. Their context, credentials and execution authority require explicit isolation controls; “shared” does not mean unrestricted access between them.

The service can centralize runtime maintenance, scheduling, configuration and recovery. It can preserve orchestration independently of any one user device, although a task using a particular endpoint still depends on that endpoint. It can coordinate approved sandbox or endpoint resources without installing a full orchestration service on every execution target.

But centralization creates its own obligations. Tasks need isolation, scoped credentials and separately controlled context. Capacity must be allocated, failures contained and service recovery planned. A shared service with broad standing access could concentrate more authority than any individual task justifies.

“Shared” must therefore mean shared service infrastructure—not shared conversations, credentials or unrestricted access.

| Decision | Endpoint-local harness | Shared harness service |
| --- | --- | --- |
| Primary fit | Work coupled to a persistent environment | Orchestration across separately authorized tasks and resources |
| Operational benefit | Direct integration with the endpoint’s working state | Centralized harness lifecycle and service operations |
| Main operating burden | Endpoint availability, updates and configuration consistency | Service availability, capacity, isolation and recovery |
| Authority risk to constrain | Excessive access inherited from the endpoint | Excessive authority aggregated by the shared service |

These are architectural trade-offs, not a performance ranking or a claim that either pattern is universally safer.

The two patterns can coexist. A shared harness may invoke tools on an endpoint directly, or delegate bounded work to an endpoint-local agent that determines its own steps. The former requests operations; the latter delegates responsibility within an approved scope. Neither arrangement should expand the authority granted to the task.

This raises a natural possibility: could the managed harness also become a deployable service that organizations operate within an approved Site? We would welcome that option for OpenAI’s Agents API. To understand where it would help, we need to distinguish deployment, operational control and the boundaries crossed during work.

## Deployment and control of a shared harness service

A shared harness service needs an explicit operating boundary: where orchestration and its state reside, who administers the service, and who controls its configuration, access and lifecycle. These operational responsibilities are distinct from the Workspace’s authority to admit tasks and govern their permitted actions. Location and operator are also distinct; neither alone determines the service’s permitted authority. The following are useful combinations, not an exhaustive taxonomy or three offerings announced by OpenAI.

### On-premises, organization-operated

The organization operates the harness service within its own facilities or approved on-premises environment. This can provide more direct control over infrastructure, local service access and orchestration state.

It also places capacity planning, patching, availability and recovery on the organization. This arrangement is relevant when specific processing or operating boundaries require it; external dependencies must still be assessed.

### Cloud-hosted, organization-operated

The organization deploys and operates the harness service in its own approved cloud environment. It can manage the harness configuration, service lifecycle and network placement while using cloud infrastructure.

This can fit a Site whose resources already reside in that environment, but still requires evaluation of provider access, regions, backups and other infrastructure dependencies. Owning the cloud account does not by itself establish who operates the service.

### Provider-managed

The provider operates the harness as a service. OpenAI’s hosted Agents API belongs in this category. In our framework, it can serve an approved Site through supported integrations; it should not be described as organization-operated merely because its tools run on the organization’s infrastructure.

This reduces the customer’s harness-management burden and offers access to provider-maintained agent machinery. The customer must still evaluate processing boundaries, supported configuration and lifecycle controls, retained records and integration responsibilities.

Provider management and physical location are separate attributes. A future provider-operated deployment inside a customer environment would need its own assessment rather than being assumed equivalent to either today’s hosted service or an organization-operated deployment.

## The challenges of orchestration across a service boundary

Separating the harness from execution can simplify agent operations while introducing a boundary into the working loop. Its significance depends on what must cross that boundary and which responsibilities are divided across it. These are architectural challenges to evaluate, not claims that a particular provider lacks the necessary controls.

### Working context can cross even when files stay local

A tool can read an internal document inside a Site and return its contents to a remotely operated harness. The source file remains in place, but information from it becomes part of the agent’s working context outside that environment.

A narrower tool interface can return approved fields or aggregates, but only if those results remain sufficient for the task. Some work depends on detailed intermediate state that cannot simply be removed. Where policy does not permit that context to enter an external service, local execution alone does not resolve the constraint. The placement of orchestration and the model route must both be evaluated.

### Connectivity becomes part of the execution contract

Remote orchestration depends on communication with its tools. Repeated interactions can introduce network round trips, while interruptions can leave the harness uncertain about an operation that has already started or completed.

The integration must establish whether work continues after disconnection, how retries avoid duplicate consequential actions, and how results are reconciled. A cancellation request is not proof that an external action has stopped. These behaviors require verification in the selected workflow; neither remote nor local placement establishes them automatically.

Placing a harness nearer its execution resources may reduce a communication dependency, but does not guarantee lower total latency or disconnected operation. Remote inference and other services may remain necessary.

### Private working environments need more than a connection

An installed application, authenticated browser session or restricted enterprise system may expose more authority than the task requires. Connecting a remote harness to that environment is therefore not just a networking exercise: the integration must define permitted operations, credential handling, reachable resources and human-control points. Public inbound access is not inherently required, but an explicit enforcement boundary is.

A Site-operated service can place orchestration closer to those resources under approved operating controls. An endpoint-local agent may be a better fit where work depends on continuous interaction with one persistent environment. Neither should inherit unrestricted access merely because it runs nearby.

Anthropic’s [sandboxing discussion](https://www.anthropic.com/engineering/claude-code-sandboxing) offers a useful parallel: filesystem boundaries, network controls and credential handling are concrete design choices for both local and cloud execution. Locality does not substitute for containment.

### Operational control and evidence span multiple systems

Managed harness updates can be valuable, but the organization may need to qualify a working configuration and identify which version and tool contracts performed a task. Supported lifecycle controls, administrative access and retained state must fit that requirement.

The harness’s session record and the executor’s operation receipts may also be held separately. Their access rules, retention and evidence must be reconciled; one transcript should not be assumed to establish the complete outcome. An organization-operated service can bring more of these responsibilities under its own administration, but it must then operate and protect them competently.

These challenges do not make a shared harness undesirable. They make its operating boundary consequential. Where policy permits remote context processing and execution interfaces are sufficiently bounded, a provider-managed service can be a strong fit. Where work depends on restricted context, tightly coupled local interactions or operating controls that the selected external service cannot satisfy, placing the shared harness within the approved Site becomes a practical architectural choice.

That Site may be an organization-operated cloud environment or an on-premises deployment. The objective is not locality for its own sake, but bringing orchestration within the boundary required by the work—while evaluating model processing and other dependencies separately.

## A proposal for a Site-deployable Agents API

For these cases, we would welcome a deployable edition of OpenAI’s Agents API that organizations could operate as a shared service within an approved Site, on premises or in their own cloud environment.

The proposal is broader than an on-premises package. The proposed offering would provide a supported way to place orchestration, working context and session state under the Site’s operating requirements, while coordinating authorized execution resources. Through qualified integrations, those resources could include sandboxes, Agentic Endpoints and endpoint-local agents.

Such an offering would need explicit deployment rights, supported interfaces, upgrade and version policies, model routes, operational-access boundaries and recovery responsibilities. A self-deployed harness should not be assumed to reproduce the hosted API’s behavior or compatibility.

This is a deployment proposal, not an announced OpenAI offering or a claim that SautX currently integrates with the Agents API.

Its localization value would depend on the whole arrangement. A Site-operated harness can still call a remote model. Tools, telemetry, backups and support access can create additional paths. If sensitive processing must remain entirely within the Site, inference and every required dependency must satisfy that condition too. Deploying the harness locally does not itself make a suitable local model available.

## One task, one accountable arrangement

Consider a hypothetical task to analyze supplier records and prepare a recommendation. Policy may permit selected aggregates to enter a hosted harness but prohibit raw records from leaving the Site. If the analysis requires those raw records in working context, that hosted arrangement is unsuitable. A Site-operated harness helps only if its model route also satisfies the restriction. Updating the supplier system remains a separately authorized action.

The business purpose can remain the same while the approved arrangement differs. If no available arrangement meets the requirements, the task should wait, fail or seek new authorization—not silently take another route.

Across all of them, the Workspace should retain authority over admission, approved agent configuration, model routes, capabilities, processing placement, data crossings and outputs.

In the proposed architecture, task authority must be checked where capabilities are exercised, and delegated work must remain within that authority. Workspace instructions alone are not an enforcement boundary.

Human authority must survive delegation. Permission to analyze does not imply permission to update supplier records, publish a recommendation or approve a payment. Users need meaningful progress and appropriate opportunities to steer, review or intervene.

Completion must also remain task-defined. A draft may require a saved artifact in an approved location; a system update may require a receipt or verified state. The agent’s final response does not replace the required evidence. That evidence must itself have bounded collection, access and retention.

This is the direction we are pursuing with Agentic Workspace: make the task—not any particular harness or environment—the durable unit of governance. Specific supported arrangements remain subject to engineering, integration and release qualification.

Our first essay asked where agents need a place to work. Our second placed that work inside a governed Workspace. The Agents API makes another part of that architecture explicit: orchestration can become a service without becoming the organization’s authority. Endpoint-local agents and shared harness services can each contribute, provided their placement, operators, model routes and data paths form an approved working arrangement.

**Different agents. Different Sites. One governed Workspace.**

Wherever the harness runs, people remain in authority over the work.
