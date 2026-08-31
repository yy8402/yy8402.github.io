---
title: "Cloudflare OS and the Agentic Workspace Taking Shape"
subtitle: "Why data sovereignty, governed execution, and open agent choice belong at the foundation of enterprise AI"
description: "Cloudflare OS, ChatGPT, and Codex point toward an emerging Agentic Workspace—and a governance boundary that must extend through execution."
publishDate: 2026-08-31
tags:
  - AI
  - Agentic Workspaces
  - Enterprise Security
  - Data Sovereignty
draft: false
---

Cloudflare's release of [Cloudflare OS](https://blog.cloudflare.com/cloudflare-os/) is an important event for enterprise AI. We immediately recognized in it many of the principles that had also shaped our own work on Agentic Workspace.

It moves the conversation beyond models and chatbots toward a more consequential question: what kind of environment do agents need in order to participate safely in real organizational work? By open-sourcing a new version shaped by what it learned from the platform used inside Cloudflare, the company has made the emerging idea of an agentic workspace far more visible.

Cloudflare OS brings agents, organizational context, generated applications and enterprise systems into one environment. Employees can ask agents to create "Gadgets," connect them to approved resources and share what they build. Gatekeepers mediate access to systems of record, while credentials remain outside the agent and generated code. Agents and Gadgets begin with no access to external resources and receive narrowly scoped capabilities as needed. It is a thoughtful expression of a principle we share: security should not merely restrict what agents can do; it should create the conditions under which people can safely allow agents to do useful work.

In May, I published [*From Chatbot to Agentic Endpoint, and Beyond*](/blog/agentic-ai-workspace/). That essay grew from our work on a different part of the problem, but articulated the same underlying change we can now see more clearly: real AI work would not remain inside a conversation.

OpenAI's subsequent move to bring ChatGPT and Codex into a [common desktop experience](https://learn.chatgpt.com/docs/features) reinforces the same direction: conversation, knowledge work and specialized agency are converging into a common workspace.

Cloudflare OS now makes the same larger movement visible at the organizational level. Seen through our architectural framework, it is an emerging cloud-native **Agent-Native Workspace**: agents are not additions to a conventional productivity suite, but first-class participants that receive organizational context, request governed capabilities, create applications and produce persistent, shareable work.

These developments are not identical products or architectures. To us, they nevertheless point toward the same larger direction:

> The AI interface is becoming a workspace, and the workspace itself is becoming agentic.

## In brief

Cloudflare OS makes the emerging Agentic Workspace tangible: agents can work with organizational context, create persistent applications and reach enterprise systems through governed capabilities. We believe the enterprise form of this Workspace needs three foundations: data sovereignty across the complete chain of work, governed execution in approved Sites and Agentic Endpoints, and open support for approved agents under one authoritative policy and evidence boundary.

## The enterprise boundary is becoming the Workspace

The importance of Cloudflare OS is not simply that it gives every employee an agent, but that it gives the agent a place within the organization: shared context, persistent work, generated applications and controlled paths to enterprise systems. Work created by an agent can become part of the organization rather than disappearing at the end of a conversation.

Cloudflare OS is agent-native at the Workspace layer. Its browser provides the Chat / Command Layer, persistent Workspace state provides continuity, Dynamic Workers execute generated applications, and Gatekeepers provide governed enterprise capabilities. Many systems beneath that Workspace remain traditional applications; APIs, Model Context Protocol (MCP) servers and Gatekeepers make them agent-friendly while allowing their integration details and credentials to recede from the ordinary user experience.

That abstraction makes the Workspace simpler for the user, but more consequential for the enterprise. As the Workspace absorbs integration and execution complexity, it also becomes the place where access, data movement, policy and accountability must be governed.

For an individual, the immediate question may be whether the agent can complete a task. For an enterprise, that is only the beginning.

The organization must also know who authorized the work, which agent performed it, where it executed, what information it accessed, which model received that information, which credentials and networks were available, what changed and what evidence remains.

The change becomes more consequential when an agent can take action. It can read and modify files, run commands, operate applications, query internal systems, create persistent artifacts and trigger downstream processes. As the agent gains agency, the security boundary expands from the conversation to the complete chain of work:

```text
Human intent
  → request and inputs
  → Workspace admission
  → authorized Task
      ├── agent or executor
      ├── model route and capabilities
      ├── execution Site
      └── required evidence
  → authorized actions
  → artifacts, state changes and evidence
```

Every transition can move data or authority.

A document retrieved from an internal system may enter an agent's context. Part of that context may be sent to a model provider. Generated code may transform the document and save a new copy. A tool may update another system. Operational logs may retain the request or result. A shared artifact may reveal information derived from a source the recipient is not permitted to access.

Enterprise security therefore cannot stop at the prompt, the model or the connector. It must govern the complete lifecycle of work.

This is why we see the Workspace as something more foundational than a common interface for AI tools. It is the enterprise boundary connecting human identity, agent authority, organizational data, models, applications, execution and accountability.

## Sovereignty must follow the work

Whether a Workspace is agent-friendly or agent-native describes how work is organized. It does not determine where that work runs or who operates the execution environment. Cloudflare OS is open source, and its documented deployment path runs in the organization's own Cloudflare account. The project describes v2 as an [early-access release](https://github.com/cloudflare/cloudflare-os?tab=readme-ov-file#warning-early-access). It can also run on the open-source `workerd` runtime, although [production self-hosting documentation and tooling are still forthcoming](https://github.com/cloudflare/cloudflare-os?tab=readme-ov-file#deploy-to-your-own-server-using-workerd). That creates a credible path beyond the managed platform, but does not by itself answer where models run, how evidence is retained, who operates every dependency or which legal authority can reach them.

Cloudflare also provides substantial [data-localization controls for Workers](https://developers.cloudflare.com/data-localization/how-to/workers/). Regional Services can restrict where requests are processed and Worker code executes. Cloudflare's documentation also notes that code and secrets are deployed globally, outgoing subrequests are not covered by the same regionalization, and other triggers can follow different paths. These are not defects in the service. They illustrate why residency, localized processing and sovereignty are related but different requirements.

A provider region may satisfy the required boundary for some organizations, but not for others whose boundaries are defined by a country, legal entity, sovereign operator, private network, facility or regulated enclave. Files may be stored in the right location while their contents travel to a model elsewhere; temporary copies, credentials, logs and artifacts may follow other paths. Sovereignty must therefore cover the whole chain: data, execution, model processing, capabilities and evidence, as well as who operates each environment.

Agentic Workspace makes that execution boundary governable. We call it a **Site**: an approved data-locality and execution boundary that may be associated with a cloud region, private VPC, customer data center, sovereign environment or restricted network. In our architectural terms, a Cloudflare OS deployment could be treated as one managed Site where enterprise policy accepts Cloudflare-operated infrastructure and its applicable regional controls; it does not have to be the only kind.

A central enterprise **Authority** decides who may perform the work, which agent and model may be used, where the task may execute and what evidence must remain. A user expresses intent through a request and its inputs, but that request is not itself executable authority. The Workspace admits it as a **Task** only after binding the approved agent or deterministic executor, model route, capabilities, execution Site and required evidence. The agent's actions—such as modifying files, running commands or operating enterprise systems—must remain within that Task's authorization.

The Session's origin Site and the Task's execution Site may be the same, but they do not have to be. The origin Site can retain the conversation and source data while another authorized Site supplies the required model route, Execution Sandbox, Managed Agentic Endpoint, private-network access or regulated environment. Anything moving between the two must be explicit, authorized and bound to the Task.

For locality-constrained work, policy may require Session data, task execution, AI routing and evidence storage to resolve within the same Site. If any required placement or route is unavailable, the work should wait, fail or require new authorization—not silently relocate.

> **Where the agent works is part of what the agent is allowed to do.**

## From sandbox to Agentic Endpoint

Cloudflare OS is a persistent workspace built around isolated, platform-managed execution. Its agent can write and run code in an isolated runtime, while generated Gadgets run in Dynamic Workers with durable state. For the work that fits this model, no explicit endpoint needs to appear.

In the framework of our earlier article, Cloudflare OS's isolated runtime resembles a **command-layer sandbox**: bounded execution supplied by the platform when the task needs it. Cloudflare OS itself is a persistent workspace, not a disposable sandbox. Agentic Workspace retains the bounded-execution pattern but gives the sandbox an explicit Site placement, so its execution and data-custody boundary can follow enterprise policy.

Not every task needs even that much execution. Drafting, summarization, explanation and planning may go directly to an approved model service. Other tasks need temporary computation but not a durable environment; a **Site-bound Execution Sandbox** can analyze files, transform data, test generated code or run an isolated operation. It is temporary, task-scoped and disposable.

But some work cannot be separated from a particular persistent environment. It may depend on an installed desktop application, an authenticated browser session, a private repository, a configured development toolchain, specialized hardware, a large local dataset, a restricted network or state that must continue across tasks.

This is the role of the concept introduced in our earlier article: the **Agentic Endpoint**.

An Agentic Endpoint is a durable, configured environment in which a Primary Agent can operate the files, applications, tools, authenticated application state, permitted networks and persistent state required for a class of work. When that environment is enrolled, secured, governed and auditable for enterprise use, it becomes a **Managed Agentic Endpoint**.

A Site may provide temporary Execution Sandboxes, persistent Agentic Endpoints or both. They are not interchangeable. The Workspace should select the smallest authorized execution context appropriate for the task:

```text
Human / User
    ↓
Chat / Command Layer
    ↓
Authorized task profile
    ├── Direct model service
    ├── Site-bound Execution Sandbox
    └── Managed Agentic Endpoint
          └── Primary Agent
```

Use a model when reasoning is enough. Use a sandbox when bounded execution is enough. Use an Agentic Endpoint when the work depends on a particular persistent environment.

Seen through this framework, the ChatGPT desktop application can function as an **Agent App** and Chat / Command Layer, while Codex can act as a Primary Agent for technical work.

The user's computer becomes an Agentic Endpoint only when an approved agent is authorized to operate its local files, repositories, terminal, browser or applications. If the work runs in a temporary cloud environment, the computer remains the command surface and the remote environment is an Execution Sandbox. If it runs in a persistent, configured remote environment, that environment may itself be an Agentic Endpoint.

One experience can remain coherent even as execution moves among models, sandboxes and endpoints.

## Co-work at the Agentic Endpoint

Long-running agentic work cannot remain a one-way delegation followed by a final answer. The situation may change, the agent may form a wrong assumption, or the work may reach a point that requires human judgment. The user needs enough visibility to understand its direction and enough agency to guide, correct or stop it. Co-work does not mean supervising every step; it means preserving the user's ability to participate when participation matters.

Codex has already taken an important first step in this direction. Its [long-running work](https://learn.chatgpt.com/docs/long-running-work) experience exposes progress as it works and allows the user to steer an active request with further guidance. The useful account is not private reasoning or every low-level technical event, but the steps, concrete outcomes and changes in direction that help the user remain oriented and respond.

We believe the Agentic Endpoint should extend this co-work from the conversation into the environment where the work actually happens. In Agentic Workspace, a **Session** connects the dialog and progress with the Endpoint's applications, files and persistent state.

The live display lets the user see the actual browser, desktop application or other graphical environment instead of relying only on the agent's description. When the work reaches a boundary involving sign-in, confidential input or human confirmation, the agent can ask for assistance and the user can take temporary control of the same environment. The user completes the sensitive step directly rather than placing the secret in the dialog or model input. Live control and display recording remain governed surfaces, so their access, capture and retention policies still apply. The user then returns control, and the agent continues from the resulting state.

Progress explains the work. The live display reveals the environment. Temporary control lets the user cross a sensitive boundary directly. Together, they make the Agentic Endpoint a place where the agent can act without pushing the user out of the work.

## The Session becomes the record of work

Agentic Workspace makes accountability a responsibility of the Workspace rather than a promise from the agent. A final response may say that a file was created, an application was updated or a workflow was completed, but the agent's statement does not establish that the outcome exists.

The **Session** is designed to connect the policy-relevant record: the user's request, the agent profile and model route, structured progress, origin and execution Sites, the selected execution placement and any Endpoint involved, governed operations, assistance and control handoffs, resulting files and state changes, validation, and the final response. The dialog remains part of the record, but it is no longer asked to stand in for the work itself.

Each kind of work can define what evidence completion requires. A document task may require the resulting file and its recorded change. A software task may also require successful tests. An enterprise workflow may require an operation receipt or verified state from the system of record. The agent proposes completion; the Workspace checks that the required evidence exists before it records success.

Live display and recording can show how an interaction unfolded. They complement, but do not replace, evidence of the outcome. The Workspace therefore connects what the user intended, what the agent and user actually did, and what result now exists.

That evidence remains subject to the same Site, retention and access boundaries as the work. The user should receive the result rather than a wall of technical logs. Protected evidence should be available only to appropriately authorized operators or investigators, without making ordinary administration a way to inspect every private conversation or working file.

This structure does not make a deployment automatically compliant or sovereign. Those remain organizational outcomes involving technology, configuration, operating policy, contracts and certification. It gives Agentic Workspace the means to express, enforce and demonstrate the evidence requirements on which those outcomes depend.

## One governed Workspace, many approved agents

Cloudflare OS makes a strong and coherent choice: it centers the experience on a deeply integrated, [multi-purpose agent](https://github.com/cloudflare/cloudflare-os), while allowing the organization to choose among models and [customize](https://github.com/cloudflare/cloudflare-os-starter/blob/main/docs/customization.md) its instructions, context, skills, Gatekeepers, integrations and interface. Agentic Workspace shares the goal of a coherent experience, but places the durable enterprise boundary one layer lower: around the Workspace rather than any single agent.

The distinction matters because model choice is not agent choice. Changing a model changes the inference engine. Changing an agent can change how work is planned and executed, which tools are used, when approval is requested and how people collaborate with it. Codex, Claude Code and other specialized agents are not interchangeable wrappers around models; each can develop capabilities and workflows that become important to particular users, teams and kinds of work.

The recent post from Shopify CEO [Tobi Lütke](https://x.com/tobi/status/2092259436538495186) offers a sharper glimpse of this enterprise reality. He said he was considering banning Claude Code at Shopify until it read `AGENTS.md` and `.agents/skills`, arguing that relying only on `CLAUDE.md` can create “split brain” problems when teammates use different tools.

The particulars concern coding agents, but the enterprise issue is broader. Different agents may suit different users, tasks, execution environments or regulatory boundaries. If their governing instructions live in agent-specific files, those copies can diverge and agents working on the same repository may operate under different rules. An enterprise cannot make its governing context dependent on whichever agent happens to be running.

The Workspace should therefore hold the authoritative context, policies and record of work, then provide each approved agent with the form it needs. The agent can retain its distinctive capabilities and user experience while operating through a common enterprise contract for identity, data access, model policy, reachable systems, execution Site, approvals, retention and evidence.

That contract must govern the complete agent integration—not only its executable. An agent's effective behavior also depends on its version and update source, model route, system and project instructions, configuration files, skills, plugins, MCP servers, hooks, runtime settings, permissions and credentials. A change to any of them may change what the agent can observe, where information can travel or which actions it can perform.

In our architecture, each task is admitted against an explicit profile: the agent or deterministic executor, model route, permitted capabilities and execution placement. A coding workflow may use one profile, knowledge work another, and a regulated process a more restricted one. The organization can use different agents where they add value while keeping each working arrangement predictable and governable.

Our current implementation begins with Codex as a deeply integrated Primary Agent. That is a statement about implementation today, not a claim that one agent should define the Workspace. If another agent is integrated, its complete profile—not merely its executable—must be evaluated and governed.

The goal is not to collect the most agents. It is to keep the organization's work—its context, files, permissions, history, approvals, artifacts and evidence—inside one governed Workspace across the different agent-backed workflows the organization has deliberately established.

Today, users often take their work to an agent. We envision approved agents coming to the governed work.

## The Workspace ahead

Cloudflare OS has made an important future tangible: enterprise AI will become a coherent place where agents, people, organizational context and applications come together to do real work. We share that vision.

We believe the enterprise Workspace must carry its governance boundary all the way through that work. It should span cloud-native execution, customer- or Site-operated sovereign environments, and Managed Agentic Endpoints; keep data, model routes, credentials, artifacts and evidence within the required boundary; and support approved agents through deliberate, governed profiles rather than separate security islands.

Inside that boundary, the user does not disappear when the agent begins to act. The Session connects progress and steering with live display, temporary control and the resulting evidence. The agent can perform the work, but it is neither the only observer of that work nor the sole judge that it is complete.

The enterprise should not have to choose between capable agents and sovereign control, or between agent autonomy and human authority. It needs one Workspace that holds them together.

> **Different agents. Different Sites. One governed Workspace.**

Data stays governed. Work stays accountable. People remain in authority.

That is the Agentic Workspace we are building.
