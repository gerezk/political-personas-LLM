2025-12-21 13:52

Tags:
# Context Window

## Anthropic: context windows

> [!spiegata-semplice] The "context window" 
> **The entirety of the amount of text a language model can look back on and reference** when generating new text plus the new text it generates

![[context-window.svg]]

> [!note] For chat interfaces context windows can also be set up on *a rolling "first in, first out" system*

When using [extended thinking](https://platform.claude.com/docs/en/build-with-claude/extended-thinking), all input and output tokens, including the tokens used for thinking, count toward the context window limit, with a few nuances in multi-turn situations.

![[context-window-thinking.svg]]

### Effective context engineering for AI agents

The **engineering** problem at hand is optimizing the utility of those tokens against the inherent constraints of LLMs in order to consistently achieve a desired outcome. 
 
Effectively wrangling LLMs often requires _thinking in context_ — in other words: considering the holistic state available to the LLM at any given time and what potential behaviors that state might yield.

- Prompt engineering refers to methods for writing and organizing LLM instructions for optimal outcomes
- **Context engineering** refers to the set of strategies for curating and maintaining the optimal set of tokens (information) during LLM inference, including all the other information that may land there outside of the prompts.

> [!importante]
> An agent running in a loop generates more and more data that _could_ be relevant for the next turn of inference, and this information must be cyclically refined.

![[prompt_eng_vs_context_eng.png]]

- - -
#### *Context Rot*
[[Context Rot]]

as the number of tokens in the context window increases, the model’s ability to accurately recall information from that context decreases.

- - -

This attention scarcity stems from architectural constraints of LLMs. LLMs are based on the [transformer architecture](https://arxiv.org/abs/1706.03762), which enables every token to [attend to every other token](https://huggingface.co/blog/Esmail-AGumaan/attention-is-all-you-need) across the entire context. This results in n² pairwise relationships for n tokens.

As its context length increases, a model's ability to capture these pairwise relationships gets stretched thin, creating a natural tension between context size and attention focus. *Additionally, models develop their attention patterns from training data distributions where shorter sequences are typically more common than longer ones*. This means models have less experience with, and fewer specialized parameters for, context-wide dependencies.

> [!curiosita]
> Techniques like [position encoding interpolation](https://arxiv.org/pdf/2306.15595) allow models to handle longer sequences by adapting them to the originally trained smaller context, though with some degradation in token position understanding

- - -

#### Write good sys prompts

Given that LLMs are constrained by a finite attention budget, _good_ context engineering means finding the _smallest_ _possible_ set of high-signal tokens that maximize the likelihood of some desired outcome

1. **System prompts** should be extremely clear and use simple, direct language that presents ideas at the _right altitude_ for the agent.

![[Context_calibration.png]]

2. We recommend organizing prompts into distinct sections (like `<background_information>`, `<instructions>`, `## Tool guidance`, `## Output description`, etc) and using techniques like XML tagging or Markdown headers to delineate these sections

3. Providing examples, otherwise known as few-shot prompting, is a well known best practice. curate a set of diverse, canonical examples that effectively portray the expected behavior of the agent.

#### Agents: context pollution constraints

To enable agents to work effectively across extended time horizons, we've developed a few techniques that address these context pollution constraints directly: compaction, structured note-taking, and multi-agent architectures.

##### Compaction

Compaction is the practice of taking a conversation nearing the context window limit, ***summarizing*** its contents, and reinitiating a new context window with the summary

##### Structured note taking

Structured note-taking, or agentic memory, is a technique where the agent regularly writes notes persisted to memory outside of the context window. These notes get pulled back into the context window at later times.

*persistent memory with minimal overhead*

> [!esempio]
> [Claude playing Pokémon](https://www.twitch.tv/claudeplayspokemon) demonstrates how memory transforms agent capabilities in non-coding domains. The agent maintains precise tallies across thousands of game steps—tracking objectives like "for the last 1,234 steps I've been training my Pokémon in Route 1, Pikachu has gained 8 levels toward the target of 10."
> 
> Without any prompting about memory structure, it develops maps of explored regions, remembers which key achievements it has unlocked, and maintains strategic notes of combat strategies that help it learn which attacks work best against different opponents.

*After context resets, the agent reads its own notes* and continues multi-hour training sequences or dungeon explorations. *This coherence across summarization* steps enables long-horizon strategies that would be impossible when keeping all the information in the LLM’s context window alone.

##### Multi-agent architectures

Rather than one agent attempting to maintain state across an entire project, specialized sub-agents can handle focused tasks with clean context windows

The main agent coordinates with a high-level plan while subagents perform deep technical work or use tools to find relevant information. Each subagent might explore extensively, using tens of thousands of tokens or more, but returns only a condensed, distilled summary of its work (often 1,000-2,000 tokens).

(substantial improvement over single-agent systems on complex research tasks)

##### Conclusion

The choice between these approaches depends on task characteristics. For example:

- Compaction maintains conversational flow for tasks requiring extensive back-and-forth;
- Note-taking excels for iterative development with clear milestones;
- Multi-agent architectures handle complex research and analysis where parallel exploration pays dividends.

Even as models continue to improve, the challenge of maintaining coherence across extended interactions will remain central to building more effective agents.






# References

https://platform.claude.com/docs/en/build-with-claude/context-windows

https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents