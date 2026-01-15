2025-12-22 16:03

Tags:
# Persona prompting

Persona prompting is a prompt engineering technique where you assign a specific role or persona to a Large Language Model (LLM) to influence how it responds. The goal in assigning the model a specific persona, such as a ‘math expert,’ or ‘supportive mentor,’ is to guide its tone, style, or reasoning approach to better align with the task at hand.

#### [_Better Zero-Shot Reasoning with Role-Play Prompting_](https://arxiv.org/abs/2308.07702)

Instead of using a simple prompt like “pretend you’re a mathematician,” they used a **two-stage role immersion approach** that includes a **Role-Setting Prompt** and a **Role-Feedback Prompt**.

- **Role-Setting Prompt:** A user-designed prompt that assigns the persona.
- **Role-Feedback Prompt:** The model’s response to the Role-Setting Prompt. It’s meant to serve as the model’s acknowledgement to the role it has been assigned. The goal is that this prompt will further anchor the model in the provided role






# References

https://medium.com/@dan_43009/role-prompting-does-adding-personas-to-your-prompts-really-make-a-difference-ad223b5f1998