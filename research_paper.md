# Research Brief: AI Scene Description and Spatial Reasoning

## 1. What I Built

I built a Hugging Face Space called **Scene Describer**, a tool that generates cinematic descriptions of a scene from different camera viewpoints based on a text prompt. Users can select a language model (e.g., distilgpt2), choose a viewpoint (such as bird’s-eye view or low angle), and adjust generation settings like temperature and top-p. The purpose of this tool is to test how well language models can reinterpret a scene and maintain spatial relationships when the perspective changes.
---

## 2. My Research Question

**“How well do different language models preserve spatial relationships when generating descriptions of visual scenes?”** :contentReference[oaicite:1]{index=1}

More specifically, I am interested in:
- whether models maintain correct spatial relationships (left/right, above/below, distance),
- whether they can adapt these relationships when the viewpoint changes,
- and how well they follow structured prompts that include camera angles.

---

## 3. Why This Matters to Me

I became interested in this topic when I explored AI tools that can change the angle of an image. I noticed that even strong models sometimes struggle with:
- object proportions,
- textures,
- and depth perception.

For example, when I tested image-based tools, I saw issues like distorted animal features and inconsistent textures :contentReference[oaicite:2]{index=2}. This made me wonder:

> If AI struggles visually with spatial transformations, does it also struggle when describing them in text?

This question matters to me because it connects to a bigger idea:
- If AI can understand spatial relationships well, it could eventually connect text and image reasoning more effectively.
- It also shows the limits of current AI systems beyond just generating fluent language.

---

## 4. What I Tried

### Week 4 — Comparing Image-Based Tools
I tested multiple Hugging Face spaces that change the angle of images. I used:
- a bee on a flower
- a goat on a mountain

I asked both tools to rotate the scene by 90 degrees.

**Findings:**
- Some models preserved structure but distorted details (e.g., bee legs, goat fur).
- Others struggled with textures like rocks :contentReference[oaicite:3]{index=3}.

---

### Week 5 — Building Scene Describer
I built my own tool using **distilgpt2**.

I tested how different generation settings affect outputs:
- **High temperature** → more randomness and errors (numbers, symbols)
- **High top-p** → less coherent but fluent outputs
- **High max tokens** → longer but meaningless outputs
- **High repetition penalty** → very short and sometimes incorrect outputs

One surprising result:
- Increasing repetition penalty made outputs much shorter than expected :contentReference[oaicite:4]{index=4}.

---

### Week 6 — Refining the Research Direction
I shifted focus from just building the tool to exploring **spatial reasoning**.

I realized that instead of attaching a specialized vision model, I could test whether language models already demonstrate spatial understanding through text generation alone :contentReference[oaicite:5]{index=5}.

---

## 5. Concrete Evidence from Testing

- **Model comparison:**  
  Using the same prompt (*“From a bird’s-eye view, the night city looked…”*), different parameter settings in **distilgpt2** produced very different behaviors. High temperature led to increasingly random and incoherent outputs (including numbers and symbols), while high top-p kept sentences fluent but made the content drift off-topic. (e.g., describing a person’s story instead of the city) 

- **One output that surprised me:**  
  When the repetition penalty was set to its maximum, the model generated a very short paragraph (20–30 words instead of ~60–70) and misunderstood the prompt by describing a literal bird instead of a city scene.

- **One prompt grid:**  
  I used a controlled testing setup where I kept the base prompt constant and changed one variable at a time (temperature, top-p, max tokens, repetition penalty). This allowed me to isolate how each parameter affected output quality and spatial description.

- **One journal observation:**  
  In earlier testing with image-based AI tools, I observed that models often distorted spatial details (e.g., bee legs, goat fur, rock textures) when changing viewpoints, showing that spatial transformation is a common challenge across both image and text systems.

- **One limitation:**  
  A major limitation is that **distilgpt2 does not reliably follow structured viewpoint instructions**, meaning errors may come from weak instruction-following rather than true spatial reasoning ability.

---

## 6. What I Learned

From these experiments, I learned:

- Language models often struggle with maintaining consistent spatial relationships.
- Prompt structure plays a major role in improving output quality.
- Smaller models like distilgpt2 are fast but less reliable in following instructions. 
- Spatial reasoning is significantly more difficult than general scene description.

---

## 7. What Still Needs Work

- Testing more advanced instruction-tuned models (e.g., SmolLM, Qwen)
- Developing a clear scoring rubric for spatial accuracy
- Expanding the range of viewpoints
- Increasing sample size for more reliable conclusions
- Creating a method to evaluate correctness more objectively

---

## 8. What Sources I Should Look For

To improve this research, I should explore:

- Spatial reasoning in language models  
- Vision-language models (image + text systems)  
- Prompt engineering techniques  
- Evaluation methods for generative AI  
- Effects of generation parameters (temperature, top-p, etc.)

---

## 9. Conclusion (Rough)

This project explores how language models handle spatial reasoning through scene description. By building and testing the Scene Describer tool, I found that while models can generate fluent text, they often struggle to maintain consistent spatial relationships—especially when asked to reinterpret a scene from a new viewpoint. This suggests that spatial reasoning remains a key limitation in current AI systems and highlights the importance of prompt design and model selection in improving performance. 
