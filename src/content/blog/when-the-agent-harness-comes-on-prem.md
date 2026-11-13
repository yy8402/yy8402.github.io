---
title: "When the Agent Harness Comes On-Prem"
subtitle: "What self-hosted Claude Managed Agents changes—and what the enterprise still has to govern"
description: "Self-hosting changes where the agent loop runs. Agentic Workspace asks how enterprises govern participation, authority, and continuity when the harness or agent changes."
publishDate: 2026-11-13
tags:
  - AI
  - Agentic Workspaces
  - Enterprise Architecture
draft: false
---

## Executive Summary

The self-hosted option for Claude Managed Agents lets enterprises run the agent harness and retain session history in their own cloud or on premises. It changes who operates the agent loop, not where inference necessarily runs or what the agent is authorized to do.

Our vision for Agentic Workspace is to keep those decisions tied to the work: what information may cross a Site boundary, who may observe, steer, or approve an action, and what evidence can carry forward when the agent changes. The goal is to let people and agents continue the work without inheriting access they no longer need.

---

On November 12, 2026, Anthropic [announced a private beta for self-hosted Claude Managed Agents](https://claude.com/fr/resources/articles/self-hosted-claude-managed-agents). It moves more than the sandbox. Previously, an enterprise could run tools on its own infrastructure while Anthropic still operated the **harness**—the loop that calls the model and directs tool use. The new option lets the enterprise operate that loop and retain session history in its own cloud or on premises. [Inference remains a separate choice](https://platform.claude.com/docs/en/managed-agents/self-hosted-data-and-access): prompts and tool results can still reach the configured model provider.

The self-hosted option for Claude Managed Agents is a concrete example of a deployment pattern we proposed for OpenAI’s Agents API in [*When the Agent Harness Becomes a Service*](https://yy8402.github.io/blog/agents-api-and-enterprise-workspace/): an organization could operate a shared harness within an approved **Site**, an operating boundary for execution and data locality. Where tools run, who operates the agent loop, and where inference happens are separate decisions. **The enterprise still has to approve a supported combination for the task—and decide what the agent may do with it.**

## From a place to work to authority over the work

In [*From Chatbot to Agentic Endpoint, and Beyond*](https://yy8402.github.io/blog/agentic-ai-workspace/), we started with what the work requires. Some requests need only a model. Others need a temporary sandbox. Still others depend on a durable environment with particular applications, files, access, and state. We called that environment an **Agentic Endpoint**. The first essay anticipated a fleet of managed Endpoints because different people and tasks would need different environments.

In [*Cloudflare OS and the Agentic Workspace Taking Shape*](https://yy8402.github.io/blog/cloudflare-os-and-agentic-workspace/), we argued that governance has to follow the work into those environments. Permission to talk to an agent or connect an application does not tell us whether the agent may read a particular record, send its contents elsewhere, or change it.

Our essay [*When the Agent Takes on an Ongoing Role*](https://yy8402.github.io/blog/muse-dots-and-agentic-workspace/) showed why those decisions need to follow the task, not just the person or agent. The same person might investigate a bug in a development Endpoint, then validate a fix in a different Site where protected test data resides. A shared harness can run within a Site, but its presence there does not grant access to the Site’s resources. What the agent can do depends on what the enterprise authorizes for that task.

## One supplier task, two decisions

Return to the supplier example from [the Agents API essay](https://yy8402.github.io/blog/agents-api-and-enterprise-workspace/). A procurement analyst wants to compare supplier performance and prepare a recommendation. The source records are inside an approved Site. In this hypothetical case, policy permits selected aggregates to be sent to an external model, but not raw records or identifiable excerpts.

The first decision is **how the analysis may run**. A Site-operated harness could invoke a narrowly scoped operation that computes the metrics where the records reside. Only results approved for that model destination would leave the Site; aggregation alone does not make a result safe to send. The external model could compare those metrics under non-identifying labels. The analyst would review the comparison and resolve the labels inside the Site before making a recommendation about a named supplier.

Giving the agent unrestricted file access and asking it not to share what it reads is not the same control. If a tool returns raw records into model context, hosting the harness locally does not stop the model route from carrying them elsewhere. If no approved arrangement can do the analysis as requested, the task has to change or wait.

Suppose the analyst now wants to change a supplier’s status in the system of record. The second decision is **whether that particular change may be made**. Permission to analyze records does not confer permission to change them. An agent’s own approval flow may allow it to run a command; that does not by itself authorize the business action the command would perform.

The agent can propose the update. The person authorized to approve it should be able to see which supplier record would change, what the new status would be, and which account would make the change. The system that applies the update should enforce that scope. The agent does not need broad write access just because one specific update may be warranted.

If the request times out without a receipt, the agent should not assume the update failed and repeat it. The destination may already have applied it. The next step is to check the actual state under appropriate authority. If the outcome cannot be verified, it should remain visibly unresolved. A record that the agent attempted an operation is not evidence that the intended change took effect.

## A Workspace that gives agents more room to work

Claude Managed Agents already provides ways to [follow a session, redirect or interrupt work](https://platform.claude.com/docs/en/managed-agents/events-and-streaming), and [respond to tool confirmation requests](https://platform.claude.com/docs/en/managed-agents/permission-policies). The enterprise question is who may use each of those controls, what information each person may see, and whether the same rules can apply when the work uses a different agent. That is the role we see for Agentic Workspace.

**Enterprise governance is incomplete if it governs what the agent can do but not who can see or intervene in the work.** Session access can expose sensitive context, and an intervention can change the course of a task. But if the people responsible for the work can only submit a request and wait for a result, they cannot see when to step in or make an informed decision when asked to approve a change. Governed session access and interaction are essential to a usable Workspace, not just to its access policy.

In the supplier example, the analyst should be able to follow the comparison and steer the work within their role. A reviewer should be able to inspect the recommendation and the evidence they’re entitled to see without gaining control of the session. An authorized approver should be able to approve or decline the exact proposed update without needing the full conversation or broad write access. Each person gets enough visibility and control to do their part without inheriting someone else’s access.

The working session need not be the handoff. The next participant should be able to receive the approved recommendation and see whether the proposed update was verified or remains unresolved. They should not inherit the analyst’s private session, raw records, or permissions simply because they are continuing the work. The Endpoint can remain available for future work while the authority granted for this task expires. That is **continuity of work without continuity of privilege**.

The same applies if a different agent takes on the follow-up. The approved recommendation, verified outcomes, and record of what remains unresolved can form the handoff. The next agent should receive only the context and fresh authority it needs for the next task, without carrying over the original conversation, credentials, or approvals.

This is how our vision extends the fleet of managed Endpoints we described in the first essay. People should be able to start with the work they need done and draw on the right environment, harness, and model route without accumulating broad standing access. Changing that arrangement should not mean starting over with a different model of authority. What should carry across is who authorized the task, what the agent was allowed to do, and what evidence establishes the outcome.

Anthropic’s release gives enterprises another way to arrange the work. Our vision for Agentic Workspace is to use that flexibility to give agents more room to work and people a meaningful way to participate, without giving either broader access or authority than the task requires.

**The harness runs the agent. The enterprise governs the work.**
