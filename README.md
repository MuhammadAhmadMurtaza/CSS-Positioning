<div align="center">

# 🎨 CSS Fundamentals: Positioning & Card Design

**Two hands-on experiments: how elements are placed on a page, and how to build a real UI component**

</div>

---

## 📖 About This Repository

This repository contains mini-projects I built while learning CSS. Each folder holds a single `index.html` file, so every concept is easy to see, edit, and experiment with.

No frameworks, no build tools. Just HTML and CSS.

---

## 📑 Table of Contents

1. [Project Structure](#-project-structure)
2. [Experiment 1: CSS `position`](#-experiment-1-css-position)
3. [Experiment 2: Card Component Design](#-experiment-2-card-component-design)
4. [How to Run](#-how-to-run)
5. [Key Takeaways](#-key-takeaways)
6. [Roadmap](#-roadmap)

---

## 📂 Project Structure

```
css-fundamentals/
│
├── 07-css-position/
│   └── index.html
│
├── 08-card-design/
│   └── index.html
│
└── README.md
```

> 💡 Rename the folders to match your own layout. Each `index.html` is fully standalone.

---

## 📍 Experiment 1: CSS `position`

📁 `07-css-position/index.html`

### 🎯 Goal
Understand how the `position` property controls where an element sits on the page, and how a **positioned parent** becomes the reference point for `absolute` children.

### 🔑 The Five Position Values

<table>
  <tr>
    <th>Value</th>
    <th>Behavior</th>
    <th>Reference point</th>
    <th>Leaves normal flow?</th>
  </tr>
  <tr>
    <td><code>static</code></td>
    <td>The default. <code>top</code>, <code>left</code>, etc. have no effect.</td>
    <td>n/a</td>
    <td align="center">No</td>
  </tr>
  <tr>
    <td><code>relative</code></td>
    <td>Shifts the element from where it would normally sit. Its original space is kept.</td>
    <td>Its own normal position</td>
    <td align="center">No</td>
  </tr>
  <tr>
    <td><code>absolute</code></td>
    <td>Placed exactly using <code>top</code>, <code>left</code>, <code>right</code>, <code>bottom</code>. Other elements ignore it.</td>
    <td>Nearest <b>positioned</b> ancestor</td>
    <td align="center"><b>Yes</b></td>
  </tr>
  <tr>
    <td><code>fixed</code></td>
    <td>Stays in the same spot on screen while scrolling.</td>
    <td>The viewport</td>
    <td align="center"><b>Yes</b></td>
  </tr>
  <tr>
    <td><code>sticky</code></td>
    <td>Scrolls normally, then sticks once it reaches a set offset.</td>
    <td>Nearest scrolling ancestor</td>
    <td align="center">No</td>
  </tr>
</table>

### 🧪 Code Highlight

The page has four stacked boxes inside a `.parent` container:

```html
<div class="parent">
  <div class="box box1"></div>
  <div class="box box2"></div>
  <div class="box box3"></div>
  <div class="box box4"></div>
</div>
```

```css
.parent {
  padding: 43px;
  margin: 34px;
  border: 2px solid purple;
  position: relative;   /* makes .parent the anchor for absolute children */
}

.box1 {
  background-color: aqua;
  position: absolute;
  top: 0px;
  left: 3px;
}
```

### 🧠 What Happens Here

<table>
  <tr>
    <td>1️⃣</td>
    <td><code>.box1</code> is <code>absolute</code>, so it is <b>removed from the normal flow</b>. The other boxes behave as if it does not exist, so <code>.box2</code> moves up into its old place and the two overlap.</td>
  </tr>
  <tr>
    <td>2️⃣</td>
    <td>Because <code>.parent</code> has <code>position: relative</code>, <code>top: 0</code> and <code>left: 3px</code> are measured from the <b>parent's edge</b>, not from the page.</td>
  </tr>
  <tr>
    <td>3️⃣</td>
    <td>Positioned elements paint on top of non-positioned ones, so <code>.box1</code> appears above <code>.box2</code> even though it comes earlier in the HTML.</td>
  </tr>
  <tr>
    <td>4️⃣</td>
    <td>Since <code>.box1</code> no longer takes up space, the parent is shorter by one box's height.</td>
  </tr>
</table>

### ⚠️ Special Case: Other Ways to Create an Anchor

Besides `position`, these properties can also make an element the reference point for its `absolute` (and `fixed`) descendants:

<table>
  <tr>
    <th>Property</th>
    <th>Example</th>
  </tr>
  <tr>
    <td><code>transform</code></td>
    <td><code>transform: translate(0);</code></td>
  </tr>
  <tr>
    <td><code>filter</code></td>
    <td><code>filter: invert(0);</code></td>
  </tr>
  <tr>
    <td><code>perspective</code></td>
    <td><code>perspective: 0em;</code></td>
  </tr>
</table>

### 🔬 Try It Yourself

<details>
<summary><b>Click to expand the experiment steps</b></summary>

<br>

1. **See the anchor in action:** remove `position: relative` from `.parent`. `.box1` now jumps to the top-left of the whole page.
2. **Try `relative`:** on `.box2`, uncomment `position: relative; top: 34px; left: 56px;`. The box shifts, but the gap it leaves behind stays.
3. **Try `fixed`:** on `.box3`, uncomment `position: fixed; bottom: 0px; left: 8vw;`. Scroll the page and watch it stay pinned to the viewport.
4. **Try `sticky`:** on `.box1`, replace `absolute` with the commented `position: sticky; top: 0px;` block. It scrolls with the page, then sticks at the top.
5. **Test the exception:** remove `position: relative` from `.parent` and add `transform: translate(0);`. The absolute box anchors to the parent again.

</details>

### 📚 Cheat Sheet

| Goal | Use |
|---|---|
| Nudge an element slightly from its normal spot | `relative` |
| Place something exactly inside a container (badge, close button) | `absolute` inside a `relative` parent |
| Floating button or chat widget that always stays visible | `fixed` |
| Header or table heading that sticks while scrolling | `sticky` |

---

## 🃏 Experiment 2: Card Component Design

📁 `08-card-design/index.html`

### 🎯 Goal
Combine layout, spacing, borders, shadows, and hover states to build a clean, modern **card UI component**.

### 🧱 Card Structure

```html
<div class="card">
  <img src="..." alt="Lake in the mountains">

  <div class="tags">
    <span>Nature</span>
    <span>Lake</span>
  </div>

  <h2>Lago di Braies</h2>
  <p>Lorem ipsum dolor sit amet...</p>
  <button>Read More</button>
</div>
```

### 🔑 Concepts Covered

<table>
  <tr>
    <th>Concept</th>
    <th>Where it's used</th>
    <th>Why it matters</th>
  </tr>
  <tr>
    <td>Universal reset</td>
    <td><code>* { margin: 0; padding: 0; box-sizing: border-box; }</code></td>
    <td>Removes browser defaults and makes sizing predictable.</td>
  </tr>
  <tr>
    <td>Flexbox centering</td>
    <td><code>body { display: flex; justify-content: center; align-items: center; }</code></td>
    <td>Centers the card horizontally and vertically.</td>
  </tr>
  <tr>
    <td><code>min-height: 100vh</code></td>
    <td><code>body</code></td>
    <td>Gives the body the full screen height so vertical centering works.</td>
  </tr>
  <tr>
    <td><code>border-radius</code></td>
    <td>Card, image, tags, button</td>
    <td>Rounded corners for a soft, modern feel.</td>
  </tr>
  <tr>
    <td><code>box-shadow</code> with <code>rgba()</code></td>
    <td><code>.card</code></td>
    <td>A semi-transparent shadow lifts the card off the background.</td>
  </tr>
  <tr>
    <td>Responsive image</td>
    <td><code>.card img { width: 100%; }</code></td>
    <td>The image always fills the card's width.</td>
  </tr>
  <tr>
    <td>Pill-shaped tags</td>
    <td><code>.tags span</code></td>
    <td>Border, rounded edges, and horizontal padding create a "chip" look.</td>
  </tr>
  <tr>
    <td>Centering a block button</td>
    <td><code>display: block; margin: auto;</code></td>
    <td>A block element with auto side margins centers itself.</td>
  </tr>
  <tr>
    <td><code>:hover</code> state</td>
    <td><code>.card button:hover</code></td>
    <td>Interactive feedback with a darker background.</td>
  </tr>
  <tr>
    <td><code>line-height</code></td>
    <td><code>.card p</code></td>
    <td><code>1.5</code> makes paragraphs easier to read.</td>
  </tr>
</table>

### 🧪 Code Highlight

```css
body {
  background-color: #e8e8e8;
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
}

.card {
  width: 350px;
  background: white;
  border-radius: 15px;
  padding: 10px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
}

.card button {
  display: block;
  margin: auto;
  padding: 10px 20px;
  border: none;
  border-radius: 20px;
  background-color: #d8ecff;
  color: #0077ff;
  font-weight: bold;
  cursor: pointer;
}

.card button:hover {
  background-color: #c5e2ff;
}
```

### 🎨 Color Palette

<table>
  <tr>
    <th>Use</th>
    <th>Value</th>
  </tr>
  <tr>
    <td>Page background</td>
    <td><code>#e8e8e8</code></td>
  </tr>
  <tr>
    <td>Card background</td>
    <td><code>white</code></td>
  </tr>
  <tr>
    <td>Tag border</td>
    <td><code>#bdbdbd</code></td>
  </tr>
  <tr>
    <td>Button background</td>
    <td><code>#d8ecff</code></td>
  </tr>
  <tr>
    <td>Button hover</td>
    <td><code>#c5e2ff</code></td>
  </tr>
  <tr>
    <td>Button text</td>
    <td><code>#0077ff</code></td>
  </tr>
</table>

### 🐛 Common Pitfall: Unbalanced Tags

If the opening `<div class="tags">` is missing but its closing `</div>` is still there, that extra `</div>` closes the **card** early. The heading, paragraph, and button then fall outside the white card. Always check that every opening tag has a matching closing tag.

### 🔬 Try It Yourself

<details>
<summary><b>Click to expand the experiment steps</b></summary>

<br>

1. Change `width: 350px` on `.card` and see how the image and text adapt.
2. Remove `box-sizing: border-box` from the reset and notice how element sizes change.
3. Adjust the `box-shadow` blur and opacity to get a flatter or deeper look.
4. Change `border-radius` on `.tags span` from `20px` to `4px` to turn pills into rounded rectangles.
5. Add `transition: background-color 0.3s;` to the button for a smooth hover effect.
6. Remove `min-height: 100vh` from `body` and watch the card lose its vertical centering.

</details>

---

## 🚀 How to Run

No installation needed.

```bash
# 1. Clone the repository
git clone https://github.com/<your-username>/<your-repo-name>.git

# 2. Move into the project
cd <your-repo-name>

# 3. Open any experiment in your browser
open 07-css-position/index.html      # macOS
start 07-css-position/index.html     # Windows
xdg-open 07-css-position/index.html  # Linux
```

💡 **Tip:** Use the VS Code **Live Server** extension to see changes instantly as you edit.

---

## 🎓 Key Takeaways

<table>
  <tr>
    <td>✅</td>
    <td><code>absolute</code> positions an element relative to its nearest <b>positioned</b> ancestor. Set <code>position: relative</code> on the parent to control the anchor.</td>
  </tr>
  <tr>
    <td>✅</td>
    <td>An <code>absolute</code> or <code>fixed</code> element leaves the normal flow, so other elements move up to fill its space.</td>
  </tr>
  <tr>
    <td>✅</td>
    <td><code>fixed</code> pins to the viewport, while <code>sticky</code> switches between normal and fixed behavior as you scroll.</td>
  </tr>
  <tr>
    <td>✅</td>
    <td>Flexbox on the <code>body</code> is a quick way to center a component on the screen.</td>
  </tr>
  <tr>
    <td>✅</td>
    <td>Small details like soft shadows, rounded corners, and hover states make a component feel polished.</td>
  </tr>
  <tr>
    <td>✅</td>
    <td>Balanced HTML tags matter: one missing opening tag can break a whole layout.</td>
  </tr>
</table>

---

## 🗺️ Roadmap

- [x] `display` property
- [x] Viewport units and box model
- [x] CSS specificity
- [x] `overflow`
- [x] Lists and `list-style`
- [x] `box-shadow` and `text-shadow`
- [x] Positioning (`relative`, `absolute`, `fixed`, `sticky`)
- [x] First card component
- [ ] Flexbox in depth
- [ ] CSS Grid
- [ ] Media queries and responsive design
- [ ] Transitions and animations

---

<div align="center">

### ⭐ If you found this helpful, consider giving the repo a star!

Made with ❤️ while learning CSS

</div>
