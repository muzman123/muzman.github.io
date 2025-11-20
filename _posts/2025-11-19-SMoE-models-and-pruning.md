---
layout: post
title: "Understanding SMoE Models and Pruning"
date: 2025-11-19
---

# Understanding SMoE Models and Pruning

I recently stumbled upon a research paper called "REAP: Router-weighted Expert Activation Pruning". The paper showed that you could remove up to 50% of experts from massive Sparse Mixture of Experts (SMoE) models with barely any performance loss. My first thought was: "Wait, if half the model is redundant, why even train it that big in the first place?"

That question sent me down a rabbit hole, and this post is basically me working through what I learned.

## First, What Even Are SMoE Models?

Before I could understand the pruning results, I had to actually understand the architecture. I'd heard about Mixture of Experts before but never really looked into how they work. Here is what i understood from some basic research:

**Normal dense models** (like GPT) work pretty straightforwardly:
- Every token goes through the same feedforward layers
- All parameters get activated for every token
- Simple, but expensive at scale

**SMoE models** do something different:
- Each layer has multiple "expert" networks (like 8 separate feedforward networks)
- A router/gating network looks at each token and decides which 1-2 experts should handle it
- Only chosen experts process that token
- The outputs get combined with a weighted sum

So if you have 8 experts of 10B parameters each, that's 80B total parameters, but only ~20B are active for any given token (if using top-2 routing). This is how models like DeepSeek or Qwen can be so large but still efficient.

## Back to the Pruning Paper: The Results That Confused Me

The REAP paper showed results for models like Qwen3-Coder-480B where they could prune 25% or even 50% of experts and maintain almost identical performance on most benchmarks. Some observations:

- At 25% pruning: barely any degradation
- At 50% pruning: most benchmarks only dropped 1-2%
- Some tasks (like agentic benchmarks) were more sensitive, mostly categories that require a multi-step reasoning process as opposed to tasks that can be accomplished with one-shot generation (like multiple choice questions)

This is where my confusion started. **If you can throw away half the model with minimal loss, why did they train it so big?** Isn't that just wasted compute?

## Questions I Had (And What I Learned)

### Q1: Does having more experts during training mean each expert becomes less redundant?

I managed to find a paper that answers this question but in short, yes.

This was a key realization for me. When you train with:

- **Few experts (like 16)**: Each expert has to be a generalist. They all learn to answer various kinds of questions.
- **Many experts (like 128)**: Each expert can specialize narrowly. One could be an expert at coding while another could be great at doing math and neither of them have much capability overlap between them.

More experts = more narrow specialization = less redundancy between them.

**This means the experts with the lowest activation frequency (the ones that get pruned) are actually the most specialized ones.** They handle edge cases and niche patterns that don't show up often in evaluation (assuming we are using the REAP method to prune the model).

### Q2: So as model size and number of experts increase, does pruning tolerance decrease?

That same research paper shows that:
- Models with **128 experts** can only be pruned by ~50% before major degradation
- Models with **32 experts** can be pruned by ~75% and still perform relatively well

Why? Because smaller models have more redundant, generalist experts. If you remove one, the others can cover for it since they have overlapping skills.

Larger models have highly specialized experts. Remove one, and you've lost a unique capability that no other expert has.

**But here's the thing:** Even though smaller models can be pruned more aggressively, the larger model pruned to 50% still outperforms the smaller model pruned to 25%.

### Q3: If pruning works so well, why train bigger models at all? Why not just train at the size I want to deploy?

This is the question that really made everything click for me.

**You can't skip the large training phase.** Here's why:

When you train with 480B parameters and lots of experts:
1. Competition between experts drives specialization
2. More diverse gradient pathways during learning
3. Richer representations emerge across the expert pool
4. The model learns better patterns overall

Then when you prune to 240B:
- You keep the BEST experts from that larger pool
- Those remaining experts learned better specializations during training
- They benefit from having competed with more experts during training

If you just trained 240B from scratch:
- Each expert is forced to be more general from the start
- Less competition, less specialization
- Lower quality ceiling even when fully trained

**The analogy that helped me:** If you have 100 people competing to come up with the best ideas versus only 50 people competing, the larger pool will always produce superior results since competition encourages higher quality. Even if you then remove half the people from that first group of 100, their quality remains high (assuming they don't become complacent)

## What This All Means

After going through all this, the "paradox" resolved itself. It's not actually wasteful to train with more experts than you deploy. The training capacity is what unlocks the performance ceiling. Training big and pruning aggressively is a viable strategy.

## The Bigger Picture

This exploration taught me something important about deep learning: **capacity during learning matters even if you don't need that capacity during deployment.**

It's similar to how:
- You need a large dataset even if you distill to a smaller model
- You need high-precision training even if you deploy in INT8
- You need many training iterations even if you only use the final checkpoint

The journey matters, not just the destination.

I'm still pretty early in understanding all the nuances of SMoE architectures—there's way more to explore around routing strategies, load balancing, expert merging techniques, and how this all scales to even larger models. But this deep dive into pruning helped me understand why model makers are still pushing for bigger models despite compression working so well.

If you're also learning about this stuff and have insights or corrections, I'd love to hear them!

---

*These are my notes and understanding. If I got something wrong or oversimplified, please let me know—I'm still learning!*