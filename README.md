### Prompt template

Every generative LLM in this study received exactly the same prompt, shown below (also Figure 2 in the paper). To avoid any risk of the template changing across models, the prompt is **not** built on the fly inside each notebook. Instead, every record pair was pre-formatted into this template once, ahead of time, and saved as a single text field alongside the data. All fine-tuning and inference notebooks read these pre-formatted prompts directly, so the only model-specific step is wrapping the prompt in each model's own chat template.

```text
You are given two patient records. Your task is to determine whether they belong to the same individual. Consider factors such as name similarity, date of birth, and other identifying attributes. Only respond with "Yes" or "No".

Record 1:
- First Name: [Record 1 First Name]
- Middle Name: [Record 1 Middle Name]
- Last Name: [Record 1 Last Name]
- Date of Birth: [Record 1 Date of Birth]
- SSN: [Record 1 SSN]
- Sex: [Record 1 Sex]
- Address: [Record 1 Address]

Record 2:
- First Name: [Record 2 First Name]
- Middle Name: [Record 2 Middle Name]
- Last Name: [Record 2 Last Name]
- Date of Birth: [Record 2 Date of Birth]
- SSN: [Record 2 SSN]
- Sex: [Record 2 Sex]
- Address: [Record 2 Address]
```

Notes:
- Missing identifiers (e.g., SSN or Address) are filled in with the word `Unknown`.
- The system prompt `You are a helpful assistant` is used for all models during both fine-tuning and inference, except DeepSeek-R1, which, following its developers' recommendation, is run without a system prompt.
- During fine-tuning, the ground-truth label (`Yes` or `No`) is supplied as the assistant's response; at inference, the model generates it.
- Because the pre-formatted prompts contain patient identifiers, they are not included in this repository. To reproduce the pipeline on your own data, format each record pair into the template above before running the notebooks.
