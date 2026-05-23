# Small/Free AI Systems and the Problem of Perspective Reasoning

## 1. What I Wanted to Build

Originally, I wanted to build an AI image-editing system capable of generating the same scene from different camera angles. The target users for this project were student researchers, indie artists, and creative developers experimenting with AI-based perspective transformation without requiring expensive hardware or advanced technical experience. The more interesting version of the idea was not simply “changing the angle of an image,” but testing whether AI systems actually understand the spatial consequences of changing perspective.

The original concept eventually became **The_Image_Editor**, a Hugging Face Space that allowed users to upload an image and generate a new version of the same scene from another viewpoint. Users could select prompts such as bird’s-eye view, low angle, side view, or over-the-shoulder while attempting to preserve the original scene identity and object placement. The deeper research question behind the project became:

> “How well do different AI systems preserve spatial relationships when reinterpreting a scene from another perspective?”

---

# 2. The Rudimentary Baseline (Space 2)

The first major system I built was **The_Image_Editor**. The Space used lightweight image-editing models running on free Hugging Face CPU hardware. I experimented with models including:
- Qwen Image Edit
- SD Turbo
- several smaller image-editing systems

The basic system worked in the sense that it could:
- accept an uploaded image,
- interpret camera-angle prompts,
- and generate alternate-angle outputs.

However, the results were not reliable enough to become meaningful evidence for viewpoint reasoning. Although the generated images often looked visually convincing at first glance, the systems frequently failed to preserve:
- spatial consistency,
- object proportions,
- depth relationships,
- textures,
- and scene identity.

For example:
- animal features became distorted,
- textures such as rocks became chaotic,
- foreground/background relationships became inconsistent,
- and the model sometimes invented completely new geometry.

The systems could imitate the *language* of perspective transformation without reliably preserving the actual spatial structure of the scene.

---

# 3. The Constraint — The Wall

The main constraint was hardware and model scale.

More advanced image-editing and novel-view generation models exist, but most are far too computationally expensive to run reliably on free Hugging Face CPU Spaces. During testing, image generation frequently crashed before producing outputs, especially when attempting larger or more detailed viewpoint transformations.

The project also encountered:
- loading failures,
- unstable generations,
- quota limitations,
- and outputs that became too inconsistent to evaluate meaningfully.

One major debugging issue occurred during the early development of **The Perspective Evidence Lab**, when several models failed to generate any outputs at all. The system had to be debugged before meaningful testing could continue.

This became the core wall of the project:

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
