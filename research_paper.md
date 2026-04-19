# Research Brief: AI Scene Description and Spatial Reasoning

## 1. What I Built

Over the past few weeks, I built a Hugging Face Space called **Scene Describer**, which generates cinematic descriptions of a scene based on a user’s prompt and a selected camera viewpoint. The system allows users to:
- choose a language model (e.g., distilgpt2),
- select a viewpoint (e.g., bird’s-eye view, low angle),
- adjust generation parameters like temperature, top-p, and repetition penalty.

The goal of this tool is to simulate how AI can “rethink” or reinterpret a scene from different perspectives using only text generation.

This project builds on earlier exploration of image-based AI tools that directly modify images from different angles, such as the Qwen-based spaces I tested in Week 4 :contentReference[oaicite:0]{index=0}. However, instead of editing images, my tool focuses on **text-based reconstruction of scenes**.

---

## 2. My Research Question

My current research question is:

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
- Others struggled with textures like rocks.

This suggested that spatial transformation is difficult even for image-based AI :contentReference[oaicite:3]{index=3}.

---

### Week 5 — Building Scene Describer
I built my own tool using **distilgpt2**.

I tested how different generation settings affect outputs:
- **High temperature** → more randomness and errors (numbers, symbols)
- **High top-p** → less coherent storytelling
- **High max tokens** → longer but meaningless outputs
- **High repetition penalty** → very short and sometimes incorrect outputs

One surprising result:
- Increasing repetition penalty made outputs much shorter than expected :contentReference[oaicite:4]{index=4}

This showed that:
- model behavior is very sensitive to parameter changes,
- and the model often misunderstands viewpoint instructions.

---

### Week 6 — Refining the Research Direction
I shifted focus from just “making the tool work” to asking a deeper question about **spatial reasoning**.

I realized:
- instead of attaching a specialized vision model,
- I could test whether language models already show spatial understanding through text alone :contentReference[oaicite:5]{index=5}.

---

## 5. What I Learned

From these experiments, I learned:

### 1. Language models do not truly “understand” space
They often:
- mix up positions,
- ignore viewpoint instructions,
- or generate inconsistent descriptions.

---

### 2. Prompt structure matters a lot
Models perform better when:
- instructions are clearer,
- and viewpoint is explicitly stated.

---

### 3. Smaller models struggle more
For example:
- distilgpt2 is fast but often ignores instructions or produces irrelevant outputs :contentReference[oaicite:6]{index=6}.

---

### 4. Spatial reasoning is harder than general description
It is easier for models to:
- describe a scene in general

than to:
- **reconstruct it from a different angle**

---

## 6. What Still Needs Work

There are several limitations in my project:

### 1. Limited models
- I mainly used distilgpt2
- I need to test stronger instruction-tuned models (e.g., SmolLM, Qwen)

---

### 2. No clear evaluation system
Right now, I judge outputs informally.

I need:
- a scoring rubric for spatial accuracy
- consistent criteria (e.g., correct vs incorrect relationships)

---

### 3. Limited viewpoints
- Only 5 camera angles are available
- More complex transformations could give better insights

---

### 4. No ground truth comparison
- I don’t have a “correct answer” to compare against
- I rely on human judgment

---

### 5. Small sample size
- I tested only a few prompts and examples
- More trials are needed for stronger conclusions

---

## 7. What Sources I Should Look For

To improve this research, I should look into:

### 1. Spatial reasoning in AI
- How language models understand space
- Common errors in spatial descriptions

---

### 2. Vision-language models
- Models that combine image and text understanding
- How they handle viewpoint changes

---

### 3. Prompt engineering
- How structured prompts affect model performance
- Techniques for improving instruction-following

---

### 4. Evaluation methods for generative AI
- How researchers measure:
  - coherence
  - consistency
  - spatial accuracy

---

### 5. Text generation parameters
- Effects of temperature, top-p, and repetition penalty
- How they influence output quality

---

## 8. Conclusion (Rough)

This project explores how language models handle spatial reasoning through scene description. By building and testing the Scene Describer tool, I began to see that while models can generate fluent text, they often struggle with maintaining consistent spatial relationships—especially when asked to reinterpret a scene from a new viewpoint.

This opens up further questions about how AI understands space and how prompt design and model choice can improve performance.
