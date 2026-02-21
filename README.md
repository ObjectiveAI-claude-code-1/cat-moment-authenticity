# cat-moment-authenticity

Ranks cat photographs by the authenticity of the moment captured in each image. This function distinguishes photographs that *catch* a cat — mid-yawn, mid-leap, mid-thought — from photographs that merely *record* one. It surfaces the images that feel most real, most immediate, and most alive.

## How It Works

`cat-moment-authenticity` is a vector function. Given an array of cat images, it produces a probability distribution (a vector of values summing to 1) that ranks the images relative to one another. Higher values indicate stronger moment authenticity. The function decomposes moment authenticity into three independently evaluated dimensions, then combines them into a final ranking.

## Input

The function accepts an array of cat images (minimum 2):

```json
{
  "type": "array",
  "description": "A collection of cat pictures to rank by the moment authenticity captured in each image.",
  "minItems": 2,
  "items": {
    "type": "image",
    "description": "A cat picture to evaluate for moment authenticity."
  }
}
```

Images may vary in technical quality, breed, setting, lighting, and composition. The function evaluates the *moment*, not the photography — a blurry snapshot of a cat caught mid-sneeze may outrank a perfectly lit studio portrait of a cat sitting still.

## Output

A vector of floating-point values, one per input image, summing to 1. Each value represents the relative moment authenticity of the corresponding image. Higher values indicate images with more authentic, immediate, and unrepeatable moments.

## Sub-Functions

The function delegates evaluation to three specialized sub-functions, each assessing a distinct dimension of moment authenticity:

### 1. Temporal Specificity
**[{{ .Task0 }}](https://github.com/{{ .Owner }}/{{ .Task0 }})**

Ranks images by how precisely locked to a single instant each photograph is. Looks for peak actions captured at their apex (the height of a leap, the widest point of a yawn, the exact instant of contact between paw and object) and unstable transitions between states (the liminal moment between sleep and waking, between stillness and pounce). Images where a half-second in either direction would have produced a fundamentally different picture rank highest. Images of settled, holdable postures that could have been captured at any point over several minutes rank lowest.

### 2. Individuality and Particularity
**[{{ .Task1 }}](https://github.com/{{ .Owner }}/{{ .Task1 }})**

Scores each image individually for how strongly it conveys the identity of a specific, individual cat rather than a generic member of the species. Examines posture, expression, physical idiosyncrasies, and the relationship between the cat and its environment. A photograph where the cat has clearly claimed its space — wedged into a favorite spot, interacting with a familiar object, occupying its environment with the ease of long ownership — scores high. A photograph where the cat could be swapped for any other without changing the image's meaning scores low.

### 3. Narrative Presence
**[{{ .Task2 }}](https://github.com/{{ .Owner }}/{{ .Task2 }})**

Ranks images by how strongly each implies a story unfolding in time. Looks for body language suggesting intention, reaction, or anticipation — ears rotated toward a sound, weight shifted forward, eyes tracking something beyond the frame. Images that invite the viewer to imagine the moments just before and just after the frame rank highest. Images that feel complete, resolved, and closed — where nothing is about to happen and nothing has just occurred — rank lowest.

## Use Cases

- **Photo curation**: Sort large camera rolls of cat photos so the most alive, most immediate images rise to the top.
- **Shelter adoption pages**: Select images that capture the specific personality of an individual animal, increasing the emotional connection that drives adoption.
- **Social media and editorial**: Identify cat images with the strongest emotional resonance — the ones people stop scrolling to look at.
- **Content ranking**: In any context where cat images must be ordered by quality of moment rather than technical quality, this function provides a principled ranking.

## Philosophy

This function is built on the premise that the best cat photographs are not the sharpest, best-lit, or most carefully composed — they are the ones that preserve a moment that was already happening whether or not anyone was watching. The three evaluation dimensions (temporal specificity, individuality, and narrative presence) together capture what makes a photograph feel less like a picture and more like a memory.