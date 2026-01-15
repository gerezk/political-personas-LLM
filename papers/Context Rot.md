2025-12-21 16:29

Tags: [[Context Window]]
# Context Rot: How Increasing Input Tokens Impacts LLM Performance

Large Language Models (LLMs) are typically presumed to process context uniformly—that is, the model should handle the 10,000th token just as reliably as the 100th. However, in practice, this assumption does not hold. We observe that model performance varies significantly as input length changes, even on simple tasks.

![[Context Rot.png]]

Because these models achieve near-perfect scores on widely adopted benchmarks like *Needle in a Haystack (NIAH)*  it’s often assumed that their performance is uniform across long-context tasks.

However, *NIAH is fundamentally a simple retrieval task*, in which a known sentence (the “needle”) is placed in a long document of unrelated text (the “haystack”), and the model is prompted to retrieve it. While scalable, this benchmark typically assesses *direct lexical matching,* which may not be representative of flexible, semantically oriented tasks.

![[Context Rot_needlestack.png]]




# References

https://research.trychroma.com/context-rot