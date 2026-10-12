---
title: "When the Agent Takes on an Ongoing Role"
subtitle: "Muse, dots, and governed work across enterprise Endpoints and Sites"
description: "Persistent agents need suitable working environments. How Agentic Workspace connects approved Endpoints, Site boundaries, private work, human participation and completion evidence."
publishDate: 2026-10-12
tags:
  - AI
  - Agentic Workspaces
  - Enterprise Architecture
draft: false
---

Muse and dots make an important idea tangible: an agent can become a continuing participant in our work. We can give it something to look after, return as circumstances change, and expect progress between conversations.

The opportunity extends beyond a longer conversation. An agent can help track unfinished work, recognize a new constraint and bring a decision back when human judgment is needed. That relationship can make projects easier to sustain.

Enterprise work adds another dimension. Different people and tasks need different applications, data, tools and authority. Some work belongs in a development environment; other work depends on a protected dataset or a particular enterprise application. A continuing relationship with an agent must be able to participate in these working arrangements.

Our Agentic Workspace vision addresses that need: approved agents and people working through suitable Endpoints and services across explicit Site boundaries, with sufficient capabilities, appropriate authority and accountable outcomes.

## Persistent agents and their working environments

Meta describes [Muse](https://about.fb.com/news/2026/09/introducing-muse-personal-ai-agent/) as pursuing goals and continuing work after the user closes the app. Its dedicated cloud VM supplies a browser and a place to act. Meta also describes a separate Sentinel, protected credential storage and controls over connected services. [Muse for Small Business](https://about.fb.com/news/2026/09/introducing-muse-small-business/) extends that experience through business integrations and custom connectors.

OpenAI's [dots](https://learn.chatgpt.com/docs/dots) similarly takes on ongoing responsibilities. It combines its cloud computer with supported work on a connected personal computer and delegation to ChatGPT Work or Codex. For coding work, it can use [configured Codex cloud environments](https://learn.chatgpt.com/docs/dots/tasks-and-memory), with repositories and setup appropriate to the task. Those [environments](https://learn.chatgpt.com/docs/environments/cloud-environments) preserve separate task state and include documented options for Enterprise customization.

These capabilities deserve recognition. Continuing agency, environment choice and permission controls are already taking concrete product forms.

In [From Chatbot to Agentic Endpoint, and Beyond](https://yy8402.github.io/blog/agentic-ai-workspace/), we explored why some AI work depends on a durable, configured environment. We called that environment an **Agentic Endpoint**, and its main agent operator a **Primary Agent**. The agent operates under delegated authority, using permitted tools and applications, maintaining working state and reporting results.

Our [Cloudflare OS essay](https://yy8402.github.io/blog/cloudflare-os-and-agentic-workspace/) brought organizational context, persistent artifacts and governed capabilities into the picture. The [Agents API essay](https://yy8402.github.io/blog/agents-api-and-enterprise-workspace/) examined how harness operation can be separated from tool execution.

An ongoing responsibility rarely stays within one kind of work. A project owner keeping a customer implementation on track may need to review progress today, investigate an application failure tomorrow, and validate a fix against protected resources later. The project context connects these activities, but their software, data and authority requirements differ.

The responsibility can remain continuous while the working arrangement changes from task to task. Muse and dots already illustrate parts of this through connected applications, local access and delegated work. Our Agentic Workspace perspective makes the choice of execution environment and its organizational boundaries explicit within the complete work.

We organize the enterprise working arrangement around three connected architectural ideas:

- **Different work needs different Agentic Endpoints.** Provide configured environments with the applications, tools, state and capabilities appropriate to the work.
- **Sites make the operating boundary explicit.** Establish where those environments operate, who runs them, and which information crossings are permitted.
- **The Workspace governs the complete work.** Connect authorization, private work, shared outputs, human participation and completion evidence across the approved arrangement.

Together, these ideas explain how people and agents can carry an ongoing responsibility forward through different working environments.

## Different work needs different Agentic Endpoints

Preparing the project owner's status update may need only approved information and a model service. Investigating an integration failure may require a repository, development tools and persistent application state. Validating the fix may require an environment with access to protected test resources.

Where work depends on a configured environment, the organization should be able to provide an appropriate Agentic Endpoint. The same person may use different approved Endpoints across these tasks, while other participants use environments suited to their own responsibilities. Our vision lets the enterprise define these configurations for its users, teams and classes of work.

- **Application development:** development tools, a selected repository and test dependencies, subject to permitted code changes and development access.
- **Protected-data analysis:** approved analysis tools and compute near selected data, subject to processing and output boundaries.
- **Production diagnosis:** diagnostic tools and scoped system access, subject to operational authority and change controls.
- **Specialist application work:** the required application, runtime and working state, subject to application availability and resource eligibility.

An Endpoint's configuration can include selected software versions, compute, files, mounts, permitted routes and supported human interaction. Its approved agent profile also identifies the agent or executor, model route and capabilities used for the work.

Users should be able to express their needs and select among eligible arrangements. Administrators determine which configurations are available and the conditions under which they may be used. Customer-specific runtime images, managed Endpoints and external Endpoints can contribute where supported; exact options depend on integration, runtime, Site, deployment and release.

Configuration and permission remain separate. An analysis tool supplies a capability; task authority determines which dataset it may use and which results may leave. An installed application does not authorize every resource it can reach.

Continuity also needs a precise meaning. A useful working environment can persist across tasks even when its compute is replaceable. In our managed-runtime design, a private Session can retain its working files while dedicated compute is stopped or replaced. Each Task records its concrete execution placement, which remains fixed during execution. Different approved environments can be used across the person's work without implying that a running task silently moves between them.

Some requests need only reasoning through an approved model. Others need temporary computation in a sandbox. An Agentic Endpoint is appropriate when the work depends on a particular configured environment and its state.

## Sites make the operating boundary explicit

Identifying a suitable environment also raises the question of where it may operate and under whose responsibility. A **Site** makes that part of the arrangement explicit: it is an approved execution and data-locality boundary with local operating responsibility. It may contain multiple Endpoints, runtime services and selected resources, on premises, in an organization's cloud or in an approved hosted environment.

The purpose becomes concrete in a protected test environment. Its operator manages the available runtimes, storage, resource connections and local controls. An approved Endpoint can operate near the applications and data required for testing. The task specifies which operations and crossings are permitted.

A Site is therefore more than a location label. It identifies the operating arrangement in which execution participates. Development and production, or an enterprise and a separately operated customer environment, may justify distinct Sites. Several users may work through one Site; one user may use different approved Sites for different work.

In the SautX architecture, Admin retains durable identity, policy and authorization authority. The Resource Edge and Site validate scoped authority and materialize supported execution locally. Being present in a Site does not grant access to every resource within it.

Harness operation and model processing must be considered separately. A hosted harness can invoke tools inside a protected Site and receive their results outside it. A locally operated harness can still send context to a remotely hosted model. Prompts, tool results, retained state and technical evidence are all potential information paths.

An on-premises Endpoint therefore establishes only part of the locality arrangement. If raw data must remain within a Site, every component that processes that data must satisfy the requirement. Placement makes the boundary explicit; permitted processing and crossings determine whether the arrangement fits the work.

OpenAI's [enterprise local-access guidance](https://learn.chatgpt.com/docs/enterprise/cloud-local-access) makes a related distinction between cloud coordination, local execution requirements and separate cloud execution controls. Our Site perspective builds the organization's operating boundary into the complete approved task arrangement.

## The Workspace governs the complete work

Endpoint configuration and Site placement establish important parts of the working arrangement. The Workspace connects their use to the people, authority, information and outcomes involved in the task.

Agentic Workspace describes our vision for governed organizational work. In the product architecture, a **Workspace** also has a specific role: it supplies the boundary for membership, shared files, publication and lifecycle. A user's **Session** holds private interaction and working state.

That distinction matters when an agent remembers context and several people participate in a project. Continuity should preserve useful work while respecting the audience for each piece of information.

A user can investigate in a private Session. Findings and artifacts become shared through explicit, governed publication. Another participant receives the approved report needed for the next task, while the original dialog and private working files retain their own access boundary. Workspace membership does not automatically expose other users' private Sessions.

Responsibility remains with the people and organization directing the work. Standing instructions may authorize routine agent activity within an agreed scope; changed resources or consequential actions may require another decision. Memory helps interpret those instructions, but does not itself grant permission to share or act.

The Workspace's value has three connected parts.

**Complete task empowerment** means providing capabilities sufficient for the defined work. The user should be able to reach the necessary applications, resources and execution without rebuilding a working environment for every request.

**Minimum necessary authority** means bounding those capabilities by the task. Useful access can be made available without turning a narrow assignment into broad standing authority.

**End-to-end accountability** means connecting intent, authorization, material actions and outcome evidence. A document task may require the saved artifact; a test task needs the appropriate results; a system update may require an operation receipt or verified state. The agent's final response alone does not establish completion.

Human participation is part of this value. For supported Endpoint sessions, progress and a live display can let the user inspect the actual working environment and provide guidance. Where policy and integration permit, the user can temporarily take control to complete a sensitive step directly, then return control so work continues. Availability varies by Endpoint, provider, runtime, Site, policy and release.

Evidence remains governed too. Completion checks do not require every private conversation or working file to become visible to ordinary administrators. Collection, access and retention should match the task's requirements.

As agency spans people, applications and environments, these functions become necessary. Organizations may implement them through one platform or several cooperating systems. Our value proposition is a coherent working arrangement that makes more work feasible while keeping its authority and outcomes explicit.

## An integration test under a concrete constraint

These choices come together when the project owner needs to validate the integration. Suppose that work requires raw customer records that must remain within an approved test Site and must not enter an external model context. This is an illustrative policy constraint, not a customer case.

A developer first investigates the code in a development Endpoint using approved test fixtures. The environment supplies the repository and toolchain without access to the protected customer records.

Validation then proceeds as a separate authorized task in the test Site. If it needs an agent to inspect raw records, the harness and model route must be approved to process them within the required boundary. If no eligible arrangement exists, that form of the task cannot proceed. An alternative may be deterministic testing that produces permitted summaries, provided the test design and output policy support it.

This is where environment choice has practical value. One general-purpose agent computer need not accumulate every application's state, customer dataset and operational credential. The organization can make the appropriate configuration available within the boundary required by the work.

The tester works in a private Session with access to the selected resources. A supported live environment can let the tester inspect an unexpected result, complete a required human step and steer the investigation. Successful execution must produce the agreed test evidence, with access governed by the same working arrangement.

A report containing permitted findings can then be made available through the approved publication path. The project owner can use that report to request a customer-update draft. The drafting task receives the shareable findings it needs; it does not require the tester's private Session or the raw records.

One person may use several Endpoints across these tasks, and several people may contribute to the same responsibility. Each task has a defined participant, execution arrangement and outcome. A compatible persistent agent may assist with follow-up within its assigned scope.

Handoffs also require clear ownership of consequential actions. If an operation's outcome is uncertain, its state must be reconciled before another participant repeats it. Changing access, pausing a task and retiring an environment are separate lifecycle decisions. Retained organizational outputs and private Session content continue under their respective policies.

## The organizational home for continuing agency

Muse and dots make the ongoing agent relationship easier to understand and use. Their environments, integrations and controls are important contributions to the emerging way of working.

Our Agentic Workspace perspective focuses on how those capabilities compose with the organization's own agents, applications, resources and operating boundaries. Configurable environments and approvals are shared concerns; our emphasis is the complete arrangement across approved Endpoints and Sites, including private work, permitted sharing, human participation and evidence.

Participation by a particular agent still requires compatible integration. Specific SautX capabilities should be evaluated against the [current-fit qualifications](https://sautx.com/technology/current-fit/) for the relevant workflow and release.

The goal is for people and approved agents to carry work forward through suitable environments while the organization retains clear authority and ownership of its outcomes.

Complete task empowerment. Minimum necessary authority. End-to-end accountability.

Different agents. Different Sites. One governed Workspace.
