# Pretext.js – A new approach to text layout on the web

## 1. What is Pretext.js?

Pretext is a lightweight TypeScript library that calculates text dimensions, line breaks and positioning **without needing to access the DOM**.

- Traditionally, developers rely on browser layout measurements to work out how much space text takes up, which can trigger expensive browser **reflows**.
- Pretext avoids that by using **Canvas text measurements** and **mathematical calculations**.

> **The main idea:** calculate text layout without asking the browser to render and measure HTML elements.

## 2. How does it work?

Pretext uses two main functions.

### Step 1 – `prepare()`: measure the text

- Uses the Canvas API (`measureText()`).
- Measures individual text segments and their widths.
- Handles Unicode, word boundaries and different languages.
- Caches the measurements for reuse.

### Step 2 – `layout()`: calculate the layout

- Takes the prepared text and the container widt
- Uses mathematical calculations to determine line breaks.
- Calculates the number of lines and total height.
- Doesn't need DOM measurements or browser reflows.

### Simple code example

```ts
import { prepare, layout } from '@chenglou/prete

// Prepare and measure the text once
const prepared = prepare('Hello, this is Pretext!', '16px Inter');

// Calculate the layout for a given width (300px) and line height (24px)
const result = layout(prepared, 300, 24);

console.log(result.height);
console.log(result.lineCount);
```

The important distinction is that `prepare()` does the initial measurement, while layout() can be called repeatedly with different container widths.

## 3. What problems can it solve?

| Use case | How Pretext helps |
|---|---|
| **Virtual scrolling** | Calculate the height of thousands of text-heavy list items without rendering and measuring every element. |
| **AI chat interfaces** | Calculate dynamic message heights as AI responses stream in, reducing layout shifts and jumping chat bubbles.|
| **Masonry layouts** | Calculate card heights before rendering, allowing more efficient positioning of content.|
| **Creative typography and animations** | Make text dynamically flow around shapes and moving objects, enabling more experimental interfaces. |

## 4. Does it introduce a new DOM?

**No, and this is an important distinction.** Pretext does not introduce a new DOM, replace the browser DOM, or replace CSS.

Instead, it provides an alternative way to calculate text layout.

| Traditional approach | Pretext approach |
|---|---|
| Create HTML elements | Prepare text |
| Ask the browser for dimensions | Measure using Canvas
| Trigger layout / reflow | Calculate using mathematics |
| Read `getBoundingClientRect()` | Call `layout()`
| Potentially expensive | Very lightweight |

The actual DOM is still used to render the interface. Pretext simply allows developers to calculate the dimensions and positioning of text before rendering it.

## 5. Why is it interesting?

The exciting part isn't just performance.
It potentially opens the door to new ways of building web interfaces that were previously difficult or expensive because of browser layout limitations.

- More responsive, text-heavy applications
- More sophisticated animations
- Better virtualised interfaces
- More dynamic typography
- Less dependence on DOM measurements

It's particularly interesting for modern applications with large amounts of dynamic content.

## 6. Limitations and considerations

Pretext isn't a replacement for the browser's entire layout engine.
- It focuses on text measurement and layout, not complete HTML/CSS rendering.
- Developers still need to render the resulting content.
- Complex CSS layouts remain the browser's responsibility.
- Font loading, spacing and rendering differences need consideration.
- It should be introduced where text measurement is actually a performance bottleneck.

---

### Closing statement

> Pretext doesn't replace the browser's rendering engine. It challenges the assumption that we need the DOM to calculate text dimensions. By separating text measurement from rendering, it gives developers more control over performance and opens up possibilities for more dynamic and creative web interfaces.


---

## Useful references

- Official docs (https://pretextjs.dev/)
