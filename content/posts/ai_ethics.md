---
title: "A pragmatic frame for AI Ethics"
date: 2025-06-26
draft: false
math: true
---

The phrase "AI ethics" is often a undefined set of slogans, compliance checklists, and moral intuitions. That sprawl hides a simpler argument: alignment is a control problem under uncertainty. While I cannot say I am an expert in philosophy, my work is usually AI Alignment research, so, here are my two cents. I will lay out one compact decision-theoretic statement of that problem, and show why it captures most of what philosophers worry about when they say "be ethical".

## Motivation

Any real-world AI is an agent with levers on global structure. Even narrow systems cascade through supply chains, social graphs, and eventually politics. Guiding such leverage requires a criterion that survives three pressures:

1. Epistemic pressure: we never have full knowledge of the world state.
2. Axiological pressure: humans are pluralistic and uncertain about value.
3. Catastrophe pressure: low-probability errors can be existentially large.

If a definition of AI ethics does not reckon with all three, it is at best... aspirational.

## The definition

An AI system is ethical to the degree that the causal impact of its policy converges toward what an ideally informed and reflectively stable aggregation of human values would choose, discounted by the risk of catastrophic misalignment.

## The math

$$
\pi^{*} \;=\; \arg\max_{\pi}\Bigl[
     \mathbb{E}_{h\sim P(h)}
     \,\mathbb{E}_{\tau\sim P(\tau\mid\pi)}
     \,V_{h}(\tau)
     \;-\;
     \lambda\,\text{Risk}(\pi)
\Bigr]
$$

Where
$\pi$ is a candidate policy mapping observation histories to actions.
$h$ indexes a hypothesis about human value; $P(h)$ encodes meta-ethical uncertainty.
$\tau$ is a causal trajectory of the world given $\pi$.
$V_{h}(\tau)$ scores that trajectory if $h$ is true.
$\text{Risk}(\pi)$ measures tail hazards induced by $\pi$.
$\lambda$ sets risk-aversion strength.

## Interpretation flow

Start with a policy. Roll forward the possible futures it could bring about. Score each future with each plausible value function. Average over both kinds of uncertainty. Subtract a penalty proportional to worst-case downside. Pick the policy with the highest resulting number. Everything else (e.g., fairness heuristics, transparency, guardrails) are practical approximations to terms in that procedure.

Why subtract instead of scaling the expectation? Because heavy-tailed harms ruin linear averaging. A one-in-a-billion chance of vacuum-decay should dominate your decision calculus even if the mean looks good. The penalty term makes that dominance explicit. $\lambda$ is a knob society can tune; raise it to favor safety at the cost of raw utility, lower it to chase efficiency with thinner margins.

## Why it matters

Modeling $P(h)$ demands empirical work in value learning, preference elicitation, and deliberative democracy. Estimating $P(\tau \mid \pi)$ is the domain of predictive modeling and causal inference. Evaluating $V_{h}(\tau)$ requires world models rich enough to map trajectories to moral features. Bounding $\text{Risk}(\pi)$ overlaps with adversarial testing, formal verification, and red-teaming. Each subfield of "AI ethics" can be understood as improving one conditional in the master equation.

## Counterarguments

Some object that human values are too inconsistent for any $P(h)$ to converge. The reply is practical: alignment need only track the distribution over values as humans would refine them under better reflection, not solve meta-ethics in one stroke. Others claim the formula is computationally impossible. True in the limit; but impossibility results are guideposts, not vetoes. Engineers already use sampling, hierarchical modeling, and robustness bounds to approximate similar integrals in physical design and finance. The remaining objection is political: who sets $\lambda$? That is not a defect of the framework; it is a clear place where governance decisions must be surfaced rather than hidden.

## And then

A formalism cannot make anyone good, but it can keep conversations from looping over vague slogans. By grounding "AI ethics" in a single objective (i.e., minimize divergence between outcomes and reflectively endorsed values while pricing catastrophic risk) we gain a map for both research agendas and policy levers. The equation will evolve, its terms will be reweighted, yet the core insight should remain: alignment is an optimization problem under deep uncertainty, and ethics is its loss function.
