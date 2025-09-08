---
title: "\"Bayesian in expectation\" is not a theorem (yet): reviewing the argument"
date: 2025-09-08T11:48:37+02:00
draft: false
math: true
tags: ["machine learning", "bayesian statistics", "transformers", "large language models", "kolmogorov complexity", "information theory", "paper review", "mathematics", "theoretical computer science", "mdl"]
preview_image: "https://files.catbox.moe/e3xvqv.png"
---

![image](https://files.catbox.moe/e3xvqv.png)

**Disclaimer:** This analysis represents my current understanding of the technical claims in the referenced paper. The critiques presented here may contain errors in interpretation or technical detail. This is an evolving post that may be revised as I receive feedback or identify mistakes in my reasoning. Readers should consult [the original paper](https://arxiv.org/abs/2507.11768) and form their own technical judgments. I welcome corrections and constructive discussion of any points raised below.

The paper aims to resolve two conflicting observations about large language models. First, positional encodings violate the exchangeability conditions required for classical Bayesian learning. Second, these models appear to compress data well and sometimes look Bayesian in spirit. The proposed resolution is that transformers are Bayesian in expectation over permutations but not in the realization at a fixed ordering. The paper presents four quantitative results and several empirical confirmations.

The story is (super!) appealing, but right now the formal layer does not carry it.

The reader does not need to have knowledge of measure theory to understand the main idea. I will keep the objects concrete. When I refer to a martingale, think of a fair game where the next expected score, given the previous outcomes, is equal to the current score. When I mention MDL (Minimum Description Length), think of the shortest code for the data that takes into account both the cost of the model and the cost of the residual surprises. When I talk about positional encoding, think of deterministic features of token positions that introduce asymmetry into a model that otherwise sees permutations as equivalent.

The narrative is organized into three key components. The first pillar is a formal identity that aims to justify the phrase "Bayesian in expectation". The second pillar is a quantitative law for predictive drift across positions. The third pillar consists of empirical tests that aim to confirm both. I will address these components in order.

The identity at the core appears as an equality of expected Kolmogorov complexities and Shannon information. The paper states

$$
\mathbb{E}_{\pi}\big[K(X\mid \pi)\big] \;=\; K(X) + I(X;\pi).
$$

This expression combines two distinct calculi. Kolmogorov complexity is defined with respect to a universal Turing machine and is noncomputable. Shannon information is defined with respect to a probability law and is computable once the law is known. There is a coding theorem that relates average prefix Kolmogorov complexity to Shannon self-information up to additive constants, assuming the expectation is taken under the true distribution of the data. However, this theorem does not support the written identity, which equates an expectation of a conditional Kolmogorov complexity with an unconditional complexity plus Shannon mutual information with a permutation variable. Algorithmic mutual information is defined by:

$$
I_K(X\!:\!\pi) \;=\; K(X) + K(\pi) - K(X,\pi),
$$

and there are only inequality relations that connect expectations of these quantities to their Shannon analogues. There is a second problem. Conditioning reduces expected code length under both Shannon information and prefix Kolmogorov complexity up to constants, contrary to the stated sign. This suggests the opposite. The conclusion is straightforward. If the thesis that transformers are Bayesian in expectation depends on the displayed identity, then the thesis lacks a valid foundation. A viable alternative is to work within the framework of Shannon MDL, using explicit codes and avoiding uncomputable quantities except as intuition.

The correct Shannon object looks like this. Introduce an explicit random ordering variable $\Pi$ with a specified distribution, for example uniform over all permutations of ${1,\dots,n}$. Define a two part code with a model class $\mathcal{M}$ and a prefix code for data given model and ordering. The total codelength is

$$
L(M) + L(\Pi) + L(X_{1:n}\mid M,\Pi).
$$

Now take expectations under a joint distribution for $(X_{1\:n},\Pi)$ and an explicit prior over $M$. Every identity you need about expectations then follows from Shannon information equalities without extra constants. The phrase Bayesian in expectation can be made a precise theorem in this space if you prove that the predictor that minimizes the expected codelength above equals the Bayes predictor under the same prior on $\mathcal{M}$ and the same distribution over $\Pi$. If you want a one line slogan, it is this. The computable MDL world already has the right algebra for expectations over orderings, no Kolmogorov complexity is required.

The second pillar is a claimed quantitative law for a martingale gap. The paper claims that a certain difference of conditional log likelihoods scales like $\Theta((\log n)/n)$ as a function of position $n$. The proof sketch starts from a Lipschitz bound that says the end to end map from inputs to logits is not too sensitive to ordering perturbations. That bound yields an order one control on how much the predictive log probability can change when you permute contexts that preserve a sufficient statistic. The logarithm appears later by an asserted combinatorial lemma about refined positional distances. No proof connects that lemma to the earlier Lipschitz steps. The constants that appear, written as $L_f$ and $\sigma_{\mathrm{PE}}$, are introduced abstractly and are not tied to a measurable operator norm of a specific transformer or to an actual positional encoding spectrum. The gap law is therefore asserted, not derived. If the goal is a theorem, one must compute the spectrum of positional perturbations for a specified encoding such as rotary or sinusoidal and propagate that spectrum through a calibrated end to end Lipschitz bound for the trained network. Without that, the correct status is an empirical regularity with uncertainty bars, not $\Theta((\log n)/n)$ with proof.

The third pillar is MDL efficiency statements. The paper claims that for Bernoulli data the expected MDL equals $nH(p)+O(\sqrt{n}\log n)$. There is a known and simple check that falsifies the displayed rate. Let $S_n$ be the number of ones in $n$ Bernoulli$(p)$ trials. The plug in code that uses the empirical frequency $S_n/n$ achieves expected code length

$$
\mathbb{E}\big[n\,H(S_n/n)\big] \;=\; nH(p) + O(1).
$$

This is a delta method expansion of the concave entropy around $p$ with a variance $p(1-p)/n$. The first order correction is constant. A quick numerical check at $p=1/2$ shows

$$
n\cdot\big(\mathbb{E}[H(S_n/n)]-H(1/2)\big) \approx -0.765,\,-0.729,\,-0.725,\,-0.723,\,-0.722,\,-0.722
$$

for $n=10,50,100,200,500,1000$. The excess redundancy is constant in $n$ within numerical noise. There is no $\sqrt{n}\log n$ term to explain in the well specified Bernoulli case. If the paper wants to keep a suboptimal rate, it must place itself in a different regime, for example misspecified models or heavy tailed fluctuations, and state those conditions explicitly.

The claim that transformers are implicit Bayesians in the limit rests on two unproven regularity assumptions. Assumption one is that attention heads perfectly separate positions where $x_i=1$ and positions where $x_i=0$ so that the network can count ones. Assumption two is that a downstream MLP can approximate rational functions that map counts to posterior moments with uniform error $O(t^{-1})$ after $t$ tokens. Neither width nor depth assumptions are stated. The convergence mode is unspecified. Without uniform approximation classes and optimization conditions, statements about $O(t^{-1})$ approximation are statements about what a proof sketch could look like, not about what a trained network is guaranteed to do.

A chain of thought section introduces more assumptions and inserts architecture specific constants into an algorithm that claims to pick an optimal reasoning length $k^*$. The section assumes $\phi$ mixing of the model's own generated chain of thought tokens with rates that scale with depth and width of the model under standard initialization. Those mixing bounds then appear inside a functional $F(k)$ that trades off a benefit curve against a positional penalty whose shape inherits the unproven $\Theta((\log n)/n)$ law from above. The algorithm requires $L_f$, a positional encoding variance $\sigma_{\mathrm{PE}}^2$, and a rotary period $p$ to compute $k^*$. These parameters are not known for proprietary models. The empirical section does not prove that the evaluated model uses rotary encodings at all. The result is an algorithm that cannot be implemented or verified on the main models of interest.

The statistical section mixes variance and standard deviation in a way that confuses the claims. If you average $k$ independent predictors, the variance scales like $1/k$ and the standard deviation scales like $1/\sqrt{k}$. The text states a variance reduction factor proportional to $k^{1/2}$. The figure reports a measured scaling $\sigma\propto k^{-0.48}$ which is close to the standard deviation law. The language should match the measured object. If the predictors are correlated because they come from permutations of the same context, the correct move is to report the effective sample size and derive the modified slope from the correlation structure.

The empirical tests do not measure the martingale property that appears in the formal section. The property written in the paper says that the conditional expectation of a predictive statistic at position $n+1$ given the past equals the same expectation given one fewer token under a specific symmetry. A faithful test computes either an exact expectation under the model's predictive distribution or a MC estimate by sampling the next token repeatedly from the model and averaging a function of those draws. The estimator implemented in the experiments uses the absolute difference of realized log probabilities for the single next token in two consecutive contexts. That is a different object. The absolute value eliminates the signed structure that a martingale difference would have, and the use of a single realized token discards the predictive distribution entirely. The result is a number that can move with position for reasons that have nothing to do with a violated martingale property.

The debiasing pipeline used to fit the $\log n/n$ law introduces degrees of freedom that point in the direction of the target trend. The code first fits a multi harmonic sinusoid with period near 64 tokens, then kernel smooths the residual, then fits the log trend. If the goal is to explain the raw positional behavior, the fit should be shown on raw data and on preprocessed data side by side with identical weights. If the goal is causal attribution to rotary encodings, the pipeline must be run across models with known absolute, learned, rotary, and ALiBi encodings, with and without the debiasing step, and the 64 periodic artifact must be shown to change in the way the rotary hypothesis predicts. Otherwise the attribution is speculative.

The model comparison statistics are not valid as presented. A likelihood ratio test for trend models requires a likelihood for the residuals, a nesting relation between hypotheses, and independence assumptions. None are specified. The weighted least squares used to fit the trend assigns weights proportional to $N_n/\widehat{\Delta}_n^2$, where $N_n$ is the number of prompts at length $n$ and $\widehat{\Delta}_n$ is the preprocessed gap. This strongly upweights large $n$ points where the two trends $1/n$ and $\log n/n$ are nearly colinear. The reported astronomically small p values are not informative under these conditions.

The prompts and data are far from natural language and do not separate the two trend models well in the measured range. Only balanced binary strings with exactly $n/2$ ones are used, with $n\leq 198$ and 100 sequences per $n$. The task is controlled, which is good for isolating positional effects. It is also underpowered for detecting $\log n/n$ versus $1/n$ on that range. The reported $R^2$ after heavy preprocessing is not strong evidence in that setting. The API configuration is also ambiguous. If only the top one log probability is returned and no tokens are generated, the log probability of the realized next token is undefined when that token is not the top one. The paper should specify echo settings, top K, and the frequency with which the realized token fell outside the returned set.
