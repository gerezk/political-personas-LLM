2025-12-22 16:03

Tags:
# Prompt Engineering

## Anthropic Prompt Engineering

#### Prompt Improver

The prompt improver enhances your prompts in 4 steps:

1. **Example identification**: Locates and extracts examples from your prompt template
2. **Initial draft**: Creates a structured template with clear sections and XML tags
3. **Chain of thought refinement**: Adds and refines detailed reasoning instructions
4. **Example enhancement**: Updates examples to demonstrate the new reasoning process
#### Prompt templates

> [!importante] 
> You should always use prompt templates and variables when you expect any part of your prompt to be repeated in another call to Claude

#### Be clear and direct

- **Give Claude contextual information:** Just like you might be able to better perform on a task if you knew more context, Claude will perform better if it has more contextual information. Some examples of contextual information:
    - What the task results will be used for
    - What audience the output is meant for
    - What workflow the task is a part of, and where this task belongs in that workflow
    - The end goal of the task, or what a successful task completion looks like
- **Be specific about what you want Claude to do:** For example, if you want Claude to output only code and nothing else, say so.
- **Provide instructions as sequential steps:** Use numbered lists or bullet points to better ensure that Claude carries out the task the exact way you want it to.

#### Use examples

- **Relevant**: Your examples mirror your actual use case.
- **Diverse**: Your examples cover edge cases and potential challenges, and vary enough that Claude doesn't inadvertently pick up on unintended patterns.
- **Clear**: Your examples are wrapped in `<example>` tags (if multiple, nested within `<examples>` tags) for structure.

#### CoT

The chain of thought techniques below are **ordered from least to most complex**.

- Include "Think step-by-step" in your prompt.
	Lacks guidance on _how_ to think

- **Guided prompt**: Outline specific steps for Claude to follow in its thinking process
	Lacks structuring to make it easy to strip out and separate the answer from the thinking.

```
Think before you write the email. First, think through what messaging might appeal to this donor given their donation history and which campaigns they've supported in the past. Then, think through what aspects of the Care for Kids program would appeal to them, given their history. Finally, write the personalized donor email using your analysis.
```

- **Structured prompt**: Use XML tags like `<thinking>` and `<answer>` to separate reasoning from the final answer.

```
Think before you write the email in <thinking> tags. First, think through what messaging might appeal to this donor given their donation history and which campaigns they've supported in the past. Then, think through what aspects of the Care for Kids program would appeal to them, given their history. Finally, write the personalized donor email in <email> tags, using your analysis.
```

#### Use XML tags

`<instructions>`, `<example>`, and `<formatting>`

#### Giving Claude a role

you can dramatically improve its performance by using the `system` parameter to give it a role. This technique, known as role prompting, is the most powerful way to use system prompts with Claude.

```
system="You are a seasoned data scientist at a Fortune 500 company.",
```

#### Chain complex prompts

Or multi-step tasks like research synthesis, document analysis, or iterative content creation. When a task involves multiple transformations, citations, or instructions, chaining prevents Claude from dropping or mishandling steps.

#### Long context tips

**Put longform data at the top**: Place your long documents and inputs (~20K+ tokens) near the top of your prompt, above your query, instructions, and examples.

Structure document content and metadata with XML tags

**Ground responses in quotes**: For long document tasks, ask Claude to quote relevant parts of the documents first before carrying out its task. This helps Claude cut through the "noise" of the rest of the document's contents.

## Google

### Define clear goals and objectives

| Strategy                                           | Example of prompt                                                                                                                |
| -------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------- |
| Use **action verbs** to specify the desired action | "Write a bulleted list summarizing the main findings of the attached research paper."                                            |
| **Define** the desired output length and format    | "Write a 500-word essay discussing the impact of climate change on coastal communities."                                         |
| **Specifies the target audience**                  | "Write a product description for a new line of organic skincare products, aimed at young adults concerned about sustainability." |

### Provide context and background information:

| Strategy                                 | Example of prompt                                                                                                                        |
| ---------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------- |
| *Include relevant facts* and data        | "As global temperatures have risen 1 degree Celsius since the pre-industrial era, discuss the potential consequences of sea level rise." |
| *Refer to specific sources* or documents | "Based on the attached financial report, it analyzes the company's profitability over the last five years."                              |
| **Define key terms** and concepts        | "Explain the concept of quantum computing in simple terms, suitable for a non-technical audience."                                       |

### Use prompt few-shot:

| Strategy                                         | Example of prompt                                                                                                                                                                                                                                                                                                      |
| ------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Give some examples of desired input-output pairs | Input: "Cat" Output: "A small, hairy mammal with a mustache." Input: "Dog" Result: "A domesticated dog known for its loyalty." Prompt: "Elephant"                                                                                                                                                                      |
| Demonstrate the desired style or tone            | Example 1 (humorous): "The politician's speech was so boring that it could have cured insomnia." Example 2 (formal): "The dignitary provided an address that was both informative and engaging." Prompt: "Write a sentence to describe the comedian's cabaret program."                                                |
| Show desired level of detail                     | Example 1 (short): "The film is about a boy who befriends an alien." Example 2 (detailed): "The science fiction film follows the story of Elliot, a lonely boy who discovers and forms a unique bond with an extraterrestrial stranded on Earth." Prompt: "Summarize the plot of the novel you just finished reading." |

### Be precise when possible


| Strategy                                     | Example of prompt                                                                                                                                                             |
| -------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Use precise language and **avoid ambiguity** | Instead of: "Write something about climate change," use: "Write a persuasive essay advocating for stricter regulations on carbon dioxide emissions."                          |
| **Quantify requests when possible**          | Instead of: "Write a long poem," use: "Write a 14-line sonnet on the themes of love and loss."                                                                                |
| Break complex tasks into **smaller steps.**  | Instead of "Create a marketing plan," use: "1. Identify the target audience. 2. Develop the most important marketing messages. 3. Choose the appropriate marketing channels." |

### Iteration refinement:

| Strategy                                    | Action                                                                  |
| ------------------------------------------- | ----------------------------------------------------------------------- |
| Try different phrases and keywords          | Rephrase the prompt using synonyms or alternative sentence structures.  |
| Adjusts the level of detail and specificity | Add or remove information to refine the output.                         |
| Prompt head of different length             | Experiment with shorter and longer prompts to find the optimal balance. |



# References

https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/overview
