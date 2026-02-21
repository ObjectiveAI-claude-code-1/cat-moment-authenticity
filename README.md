# cat-moment-authenticity

Ranks cat pictures by the authenticity of the moment captured in each image — the degree to which a photograph transmits the feeling of a singular, unrepeatable instant in the life of a living creature.

## What It Does

This function takes a collection of cat photographs and produces a ranking based not on photographic quality, composition, or the appearance of the cat, but on *moment authenticity*: the sense that the image preserves something real, immediate, and fleeting. A slightly blurred photo of a cat mid-leap may rank far above a crisp, well-lit portrait of a cat sitting symmetrically on a cushion. What matters is the moment, not the artifact.

The function asks a simple question of each image: **was this moment alive, or was it merely recorded?**

## Input

An array of cat images (minimum 2). Each image is evaluated and ranked relative to the others.

```json
{
  "type": "array",
  "minItems": 2,
  "items": {
    "type": "image",
    "description": "A cat picture to evaluate for moment authenticity."
  }
}
```

## Output

A probability vector (array of numbers summing to 1) with one entry per input image. Higher values indicate greater moment authenticity. The output represents a relative ranking — each image's score reflects how it compares to the others in the set.

## What It Evaluates

The function decomposes moment authenticity into three qualities, each assessed by a dedicated sub-function:

### 1. Temporal Specificity

**Sub-function:** [cat-fleeting-moment-rank](https://github.com/ObjectiveAI-claude-code-1/cat-fleeting-moment-rank)

The sense that the photograph could only have been taken at this exact fraction of a second. Evaluates whether the image captures a fleeting, unrepeatable instant — a peak action (mid-leap, mid-yawn), a micro-expression (ears flattening at a sound, a slow blink caught at its most closed), or a split-second of bodily tension (muscles gathered before a spring, the soft collapse into sleep). The core test: if this photo had been taken one second earlier or later, would it look meaningfully different? Images where the answer is emphatically *yes* rank higher. Images depicting stable, persistent states that could be photographed at any point across minutes rank lower.

### 2. Transitional Vitality

**Sub-function:** [cat-transitional-vitality](https://github.com/ObjectiveAI-claude-code-1/cat-transitional-vitality)

The degree to which the cat is caught in a state of *becoming* rather than a settled state of *being*. Evaluates whether the cat is visibly between two conditions — between stillness and motion, sleep and wakefulness, curiosity and indifference, composure and surprise. This includes physical transitions (a body mid-stretch, a head in the act of turning, weight shifting unevenly between paws) and emotional transitions (awareness flooding into a newly opened eye, a playful cat freezing into uncertainty). Images that vibrate with implied before-and-after rank higher. Images where the cat is fixed in a single stable condition rank lower.

### 3. Particular Intimacy

**Sub-function:** [cat-particularity](https://github.com/ObjectiveAI-claude-code-1/cat-particularity)

The sense that this photograph is of *this cat*, in *this place*, at *this time* — not a generic record of the species. Evaluates specificity of detail: posture that suggests personality, a relationship between cat and environment that implies familiarity and belonging, a gaze that feels directed and particular, and contextual details that anchor the moment in a real, lived-in world. Also evaluates narrative quality — whether the image implies a story about this cat's day, habits, and private life. Images that feel like intimate encounters with a particular being rank higher. Images where the cat and surroundings feel interchangeable and anonymous rank lower.

## Use Cases

- **Personal photo curation** — Selecting the images from your camera roll that truly capture who your cat is, rather than merely confirming your cat exists.
- **Community photo contests** — Ranking submissions by the aliveness of the captured moment rather than photographic polish or breed aesthetics.
- **Shelter and rescue adoption pages** — Choosing images that present cats as individuals with personalities and stories, helping potential adopters feel a connection.
- **Editorial and artistic selection** — Finding reference images that convey genuine animal presence and spontaneity rather than posed stillness.
- **Social media curation** — Surfacing the photos that feel most alive and shareable from large collections.

## Architecture

The function is a `vector.function` that decomposes its evaluation into three sub-functions:

| Task | Type | Evaluates |
|------|------|-----------|
| [cat-fleeting-moment-rank](https://github.com/ObjectiveAI-claude-code-1/cat-fleeting-moment-rank) | vector | Temporal specificity — precision of the captured instant |
| [cat-transitional-vitality](https://github.com/ObjectiveAI-claude-code-1/cat-transitional-vitality) | vector | Transitional vitality — dynamic process between states |
| [cat-particularity](https://github.com/ObjectiveAI-claude-code-1/cat-particularity) | scalar (mapped) | Particular intimacy — individuality and narrative specificity |

The first two sub-functions rank all images relative to each other as a set. The third scores each image individually for particular intimacy, then normalizes the scores into a relative ranking. The function's final output is the weighted average of all three task outputs.

## Philosophy

This function is built on a single underlying belief: the best photographs of cats are the ones that honor the *aliveness* of their subjects. A living being exists in time, moves between states, and is irreducibly itself. A photograph that captures all three truths — *this exact instant*, *this state of becoming*, *this individual creature* — preserves a cross-section of living experience so faithfully that life itself seems to pulse within the frame. The function attempts to identify the visual signatures of such moments and use them to separate images that feel like encounters from images that feel like records.