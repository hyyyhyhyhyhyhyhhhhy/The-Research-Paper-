# Small/Free AI Systems and the Problem of Perspective Reasoning

# 1. What I Wanted to Build

Originally, I wanted to build lightweight AI systems that could reinterpret the same scene from different camera perspectives while preserving spatial consistency. The target users for these systems were student researchers, indie artists, and creative developers experimenting with AI-based perspective transformation without requiring expensive hardware or advanced technical experience. The more interesting version of the idea was not simply generating fluent descriptions or edited images, but testing whether AI systems actually understand the spatial consequences of changing viewpoint.

The project began with two baseline Hugging Face Spaces focused on text-generation and scene description. These systems allowed users to enter a scene prompt, select a camera perspective such as bird’s-eye view or low angle, and compare how different language models described the same environment from multiple viewpoints. The original goal was to study whether smaller language models could preserve spatial relationships consistently through text before expanding toward more advanced image-based perspective transformation systems.

---

# 2. The Rudimentary Baseline (Space 1-2)

After building the original Scene Describer systems, I expanded the project into **The_Image_Editor**, a Hugging Face Space focused on AI image-based perspective transformation. The system attempted to generate alternate-angle versions of uploaded images using lightweight image-editing models running on free Hugging Face CPU hardware. I experimented with:
- Qwen Image Edit,
- SD Turbo,
- and several other lightweight image-editing systems.

The basic functionality worked in the sense that users could:
- upload an image,
- choose a new camera angle,
- and generate an alternate perspective of the same scene.

However, the outputs quickly revealed major limitations. Although the generated images often appeared visually convincing at first glance, the systems struggled to preserve:
- object proportions,
- spatial consistency,
- depth relationships,
- textures,
- and scene identity.

For example:
- animal features became distorted,
- textures such as rocks became unstable,
- and foreground/background relationships frequently shifted incorrectly.

The image-editing systems could imitate the *language* of camera-angle transformation without reliably preserving the deeper spatial structure of the original image. This became the first major sign that lightweight AI systems may not truly understand perspective transformation in a stable or testable way.

---

# 3. The Constraint — The Wall

The main constraint was hardware and model scale.

More advanced image-editing and novel-view generation models exist, but most are far too computationally expensive to run reliably on free Hugging Face CPU Spaces. During testing, image generation frequently crashed before producing outputs, especially when attempting larger or more detailed viewpoint transformations. It turned out, The Image Editor space can edit the angle of which a picture is taken from, but it cannot generate meaningful or testable results because the output is usually not accurate, due to the fact that the reliable image editing models are way too heavy for free CPU. 

Here is an example of one of the outputs the space gave out: 
![The original picture](https://postimg.cc/94LMvhzY)
![The output](https://postimg.cc/xJQRFLJj)

The project also encountered:
- loading failures,
- unstable generations,
- quota limitations,
- and outputs that became too inconsistent to evaluate meaningfully.

One major debugging issue occurred during the early development of **The Perspective Evidence Lab**, when several models failed to generate any outputs at all. The system had to be debugged before meaningful testing could continue.

This became the core wall, as well as the conclusion of the research of the project:

> lightweight/free AI systems could imitate camera-angle vocabulary but struggled with genuine viewpoint consequences.

---

# 4. What I Tried First

Before changing the architecture of the project, I attempted several smaller fixes and partial solutions.

I experimented with:
- SD Turbo,
- Qwen Image Edit,
- prompt restructuring,
- different inference settings,
- seed control,
- and multiple lightweight image-editing pipelines.

I also tested:
- temperature,
- top-p,
- max token count,
- repetition penalty,
- and viewpoint-specific prompting strategies.

One controlled prompt used throughout testing was:

> “From a bird’s-eye view, the night city looked…”

This prompt was repeatedly tested across:
- close-up,
- wide shot,
- bird’s-eye view,
- low angle,
- and over-the-shoulder perspectives.

Some partial improvements occurred. Certain outputs became more visually stable after adjusting parameters such as repetition penalty or prompt structure. However, the systems still failed to produce reliable spatial reasoning consistently enough for evaluation.

One surprising result occurred when the repetition penalty was increased significantly while testing distilgpt2. The generated paragraph became extremely short and misunderstood the prompt completely, describing a literal bird instead of a city scene. This showed that the models often followed surface-level associations instead of maintaining viewpoint logic.

These failed and partial moves were important because they revealed that the problem was not simply “finding the correct prompt,” but the deeper limitation of lightweight systems attempting perspective transformation.

---

# 5. The Move That Worked (Space 3)

The major architectural shift was moving away from image generation and toward controlled viewpoint-reasoning experiments using text-generation systems.

This led to the creation of **The Perspective Evidence Lab**, built using:
- Hugging Face Spaces
- Gradio
- Hugging Face Transformers

Instead of generating alternate-angle images directly, the new system tested whether language models could preserve spatial relationships when describing the same scene from multiple viewpoints.

The Perspective Evidence Lab compared:
- distilgpt2,
- SmolLM2-135M-Instruct,
- SmolLM2-360M-Instruct,
- and Qwen/Qwen2.5-0.5B-Instruct

across viewpoints such as:
- close-up,
- wide shot,
- bird’s-eye view,
- low angle,
- and over-the-shoulder.

The project shifted from evaluating image realism to evaluating measurable reasoning factors:
- foreground/background changes,
- visibility,
- occlusion,
- scale,
- spatial relationships,
- and viewpoint consistency.

A scoring rubric was added so outputs could be systematically evaluated instead of judged informally.

During rubric testing, **SmolLM2-135M-Instruct** became the most stable and reliable lightweight model for controlled perspective reasoning experiments.

This move transformed the project from:
> “trying to build a perfect image-angle generator”

into:
> “building a reproducible system for testing viewpoint reasoning under hardware constraints.”

---

# 6. What the Move Cost Me

The move away from image editing came with important tradeoffs.

The project lost:
- direct visual evidence,
- realistic alternate-angle images,
- and the original goal of fully reconstructing scenes visually from new viewpoints.

Text-generation models can describe perspective changes, but they do not truly reconstruct 3D geometry or perform actual image-based spatial reasoning. Instead, they generate viewpoint-consistent descriptions through language patterns and instruction following.

The project also became dependent on:
- external Hugging Face model hosting,
- free CPU limitations,
- inference latency,
- and model availability.

Smaller models were more deployable, but weaker at instruction-following and spatial consistency. Larger models were stronger, but often impractical for lightweight deployment environments.

This created a constant tradeoff between:
- model capability,
- reproducibility,
- and deployment constraints.

---

# 7. What I'd Do Next

The next stage of the project would focus on improving evaluation quality rather than simply increasing model size.

Future improvements could include:
- testing multimodal vision-language systems,
- expanding the scoring rubric,
- increasing the number of scene prompts,
- testing more difficult perspective transformations,
- and comparing text-based reasoning against image-captioning systems.

I would also like to explore whether stronger multimodal models genuinely preserve spatial logic better than lightweight text-only systems.

However, the main limitation remains real:

> small/free AI systems can imitate viewpoint language without reliably preserving true spatial reasoning.

That limitation ultimately became the central finding of the project rather than simply a technical obstacle.
