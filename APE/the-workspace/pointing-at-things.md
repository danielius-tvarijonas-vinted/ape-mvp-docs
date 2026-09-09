# Pointing at things

Describing a UI element in words is harder than it sounds. "The button at the top right of the search page" is four things the agent has to guess correctly before it even opens a file.

Clicking it removes the guessing.

## Inspect[​](#inspect "Direct link to Inspect")

Turn on **Inspect** from the floating toolbar over the preview.

Hover, and each element highlights with a label telling you what it is – the component name and the file it comes from. This is useful on its own, as a way to learn a codebase you don't know.

Click, and that element is attached to your next prompt. You'll see it as a chip above the composer. Now you can write:

> make this taller

...and the agent knows exactly which element, in which file, on which route.

Inspect stays on until you turn it off, so you can click, prompt, look, and click again without toggling.

### Why it works better[​](#why-it-works-better "Direct link to Why it works better")

Without it, the agent searches for something matching your description and picks the most likely candidate. Usually right, sometimes not, and on a large codebase "not" costs you a whole turn.

With it, the agent gets the component and the source file directly. The difference is biggest on projects like `marketplace-web`, where a component name might appear in a dozen places.

## Region capture[​](#region-capture "Direct link to Region capture")

The other toolbar mode. Drag a box over any part of the preview and the crop lands in your chat as an image.

Useful when the problem is visual and awkward to name:

> the spacing in this section is inconsistent – make it even

Two things worth knowing:

* The capture is of the **live page**, so open modals, dropdowns and hover states are included. If you can see it, you can capture it.
* It captures what's in the viewport, so scroll to what you want first.

## Using both together[​](#using-both-together "Direct link to Using both together")

They're mutually exclusive on the toolbar – one at a time. But their outputs aren't: you can capture a region, then switch to Inspect, click an element, and send both with one prompt.

That combination – a picture of the problem plus the exact file – is about as much context as you can hand over in one message.

## Attaching images from elsewhere[​](#attaching-images-from-elsewhere "Direct link to Attaching images from elsewhere")

You don't have to capture from the preview. Paste or drag any image into the chat, up to four per message.

A Figma export works well as a target:

> match this layout, using the components we already have

The agent can see the image. It can't open a Figma link, so export first.
