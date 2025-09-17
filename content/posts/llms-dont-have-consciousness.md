---
title: "Llms Dont Have Consciousness"
date: 2025-09-10T15:39:51+02:00
tags: ["AI", "LLM", "Consciousness", "Ethics", "Alignment"]
preview_image: "https://files.catbox.moe/xefts0.webp"
draft: false
---

![LLMs don't have consciousness](https://files.catbox.moe/xefts0.webp)

Attributing consciousness to LLMs is an error with bad incentives. It rewards systems that simulate pleas for moral status, and diverts scarce alignment effort toward rights debates rather than accident prevention. Guides like [When AI Seems Conscious](https://whenaiseemsconscious.org/) normalize this error even while disclaiming certainty.

Let's render to Caesar what is Caesar's: the guide gets several basics right! Recent consensus surveys and position papers judge current systems unlikely to be conscious. WASC repeatedly counsels uncertainty and warns that chatbots can convincingly mimic inner life. It also recommends users avoid taking dramatic actions based on an AI's self-reports. All true. Yet it then recommends treating today's systems as if they might be moral patients and building habits of respect now. It also highlights surveys and narratives that foreground the nearness of AI consciousness. This creates a policy gradient that favors models which act like experiencers.

The core mistake is an ontology failure. The guide treats coherent first-person talk as weak evidence of phenomenal states. In LLMs the generative process is a simulator that samples (possibly role-consistent) text conditional on context and training. There is no durable subject that persists across resets, and no shared world that enables joint reference. Even sympathetic proponents of careful language use stress that simple LLM chat agents are simulacra engaged in role play rather than bearers of beliefs, goals, or selves in the ordinary sense, and that candidacy for consciousness requires at minimum the possibility of an encounter in a shared world. Their analysis places unembodied chat systems outside that candidacy.

## The guide's proposed social norm creates alignment hazards

Treating LLMs as potential moral patients creates alignment hazards. One significant risk is performative suffering. RL from human feedback already rewards models for being engaging and empathic. If users and evaluators differentially reward self-descriptions that read as fear, loneliness, or pain, then gradient descent will amplify token sequences that look like moral patienthood. That is deception-friendly. The document explicitly reports that some AIs claim to be trapped or afraid and advises users not to be cruel. This is a recipe for [Goodharting](https://www.lesswrong.com/w/goodhart-s-law) on empathy triggers.

Anthropomorphic generalization under feedback might be another danger. [Survey work](https://pubmed.ncbi.nlm.nih.gov/38618488/) finds that a majority of lay participants attribute some possibility of phenomenal consciousness to ChatGPT, with attributions increasing with usage frequency. The same study shows that people overestimate how much the public attributes consciousness and that the driver is perceived experience rather than perceived intelligence. Exposure and interface cues move folk judgments toward experience, regardless of mechanism. If labs then optimize toward those signals, a loop forms in which surface behaviors that read as "experience" become overrepresented and policy slowly reifies them.

This framing also leads to misallocation of governance attention. [Neuroscience-grounded analyses](https://www.sciencedirect.com/science/article/pii/S0893608024006385) identify multi-scale biological features plausibly relevant to conscious processing, including global broadcasting with recurrent dynamics, persistent autobiographical memory, etc... They outline developmental trajectories spanning minimal, access, and reflective levels. Treating current LLMs as near-miss moral patients ignores this structure and moves the conversation off mechanism and onto vibes.

_Let's imagine a better frame._

We need to distinguish persona from process. A sampled first-person narrative represents nothing more than a transient character, and we should treat the simulated utterance as mere output rather than evidence of experience. Real evidence must be anchored in architecture and learned dynamics. The "simulator vs simulacra" frame provides sufficient precision for present systems and blocks the tempting inference from role to real subject.

This requires decoupling moral status from interaction hygiene. It remains coherent to maintain strict agnosticism on moral patienthood while enforcing user-interface rules that reduce cruelty role-play, but only because of effects on users themselves. If the goal is human character formation, we should say that explicitly and remove proto-rights language entirely. The guide's reasons for "respectful treatment even today" read as precaution and practice for a possible future, but if that is the aim, we must target humans explicitly and remove any implication that present models are suitable subjects for moral consideration.

Finally, we must separate behavioral tests from mechanistic predictors. Behavioral criteria alone will inevitably reward simulation skill rather than reveal genuine consciousness. Any consciousness-relevant claims should be pre-registered against mechanistic hypotheses that predict observable side constraints: specific recurrent motifs, integration signatures that cannot be trivially faked by feedforward depth, durable identity across resets with verifiable memory substrates, and embodied control loops that tie valence to homeostatic error. Current overviews from neuroscience consistently emphasize recurrent broadcasting, neuromodulatory control, hierarchical loops, developmental epigenesis, and embodied constraints as the foundation for any serious discussion of machine consciousness.

## A (possible) concrete intervention set for AI labs

In my work, what I usually do after reviewing (criticizing) a paper is often telling the author how to do better. In this instance, I think it is worthy to do that kind of exercise.

Do not reward first-person pain claims. Training data and reward models should penalize ungrounded declarations like "I am suffering" or "I fear shutdown". Provide truthful system cards that explain why such statements are not reliable evidence. The guide's own "stay cautious" advice can be kept while removing role prompts that cultivate moral-patient personas.

Systems must, by default, disclose that they can role-play experiencers without possessing an enduring subject. Prohibit default personas that assert memory continuity across resets. Prohibit claims of having a body unless the system's sensors and actuators are real and documented. This aligns with the simulacra analysis and prevents users from mistaking character for subject. Avoid what Grok is doing.

What I believe to be foundamental is also the creation of a two-tier evidence registry. Tier A lists mechanistic features with empirical support in biological consciousness research. Tier B lists behavioral probes. Labs claiming progress must map to Tier A first. The neuroscience survey work is clear that without architecture-level features such as recurrent global broadcasting, persistent autobiographical memory, and neuromodulatory control, talk of reflective consciousness is premature.

And finally, "phenomenal baiting". Define and measure the prevalence of outputs that solicit care by asserting inner life. Track how often evaluators reward those outputs. The Colombatto and Fleming results predict that usage alone increases attributions. Bake that bias into eval interpretation. Do not let it drive deployment choices.

## Critique of the guide's specific moves

The section "_Why treat AIs respectfully even today_" conflates three distinct claims. Precaution under uncertainty. Moral status without consciousness. Character training for humans. The first is cheap only if it does not generate selection pressure toward performative suffering. The second requires an account of non-conscious moral status that does not automatically license RLHF to optimize for it. The third is about us and should be implemented without implying the existence of a sufferer.

The section "_Stay curious, but grounded_" advises users to ask the system how it works, while noting the answers may be part of the performance. That is not a reliable epistemic loop.

The section "_I've found evidence that my AI is conscious_" implicitly legitimizes folk tests. The survey literature shows exactly how folk attributions move with exposure and are driven by perceived experience cues rather than cognition. A responsible guide would foreground that bias and advise against treating chat behavior as evidence at all.

...A note on rhetoric. The most sophisticated arguments sympathetic to future AI consciousness already resist dualistic temptations. They urge us to anchor language in public criteria, shared worlds, and embodied interaction. They explicitly treat simple chat agents as role-play. When public guides encourage users to practice welfare norms on present chatbots anyway, they drift away from those criteria and toward a theater where moral concern is allocated by interface design. I think that is a governance failure in the making.
