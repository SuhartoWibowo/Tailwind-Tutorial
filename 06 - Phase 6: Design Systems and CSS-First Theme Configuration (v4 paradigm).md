### Phase 6: Design Systems and CSS-First Theme Configuration (v4 paradigm)

In previous versions of Tailwind, customizing your colors, fonts, and breakpoints was done in a JavaScript configuration file called `tailwind.config.js`. 

In the modern **Tailwind CSS v4** engine, this configuration is fully **CSS-first**. You configure your entire design system directly inside your global CSS file using native CSS variables and the new **`@theme`** directive.

We will break Phase 6 into three core lessons:
*   **Lesson 6.1: The CSS-First Theme Config (`@theme`)**
*   **Lesson 6.2: Customizing Design Tokens (Colors, Fonts, Spacing)**
*   **Lesson 6.3: Mastering Dark Mode (Manual & System Toggling)**

---

### Lesson 6.1: The CSS-First Theme Config (`@theme`)

Instead of writing complex nested JavaScript objects, Tailwind v4 detects special CSS custom properties (variables) defined inside a `@theme` block in your stylesheet.

#### How Custom Variables Map to Utilities
When you define a variable inside `@theme`, Tailwind automatically parses the prefix and compiles the corresponding utility classes.

```css
@import "tailwindcss";

@theme {
  /* This automatically creates the `bg-brand-primary` and `text-brand-primary` utilities! */
  --color-brand-primary: #ff5500;
  
  /* This automatically creates the `font-display` utility class! */
  --font-display: "Clash Display", sans-serif;
}
```

#### Overriding vs. Extending
*   **Extending (Default):** Any variable you add inside `@theme` will be *added* to Tailwind's default design library. For example, adding `--color-brand` keeps all standard colors (`bg-red-500`, `bg-blue-300`) and simply adds `bg-brand` to your toolkit.
*   **Resetting to Blank:** If you want to disable the default theme entirely and build a custom system from absolute scratch, you set the global namespace to initial:
    ```css
    @theme {
      --*: initial; /* Clears all default Tailwind tokens */
      --spacing: 4px;
    }
    ```

---

### Lesson 6.2: Customizing Design Tokens

Let's look at the syntax conventions for different types of custom variables.

#### 1. Custom Colors (`--color-*`)
You can define single colors or shade scales:
```css
@theme {
  /* Single brand color */
  --color-neon-blue: #00f0ff;

  /* Color scale */
  --color-brand-50: #f0f7ff;
  --color-brand-500: #0070f3;
  --color-brand-900: #002d62;
}
```
*Utilities generated:* `bg-neon-blue`, `text-brand-500`, `border-brand-900` etc.

#### 2. Custom Typography (`--font-*`)
```css
@theme {
  --font-display: "Satoshi", "Helvetica", sans-serif;
  --font-serif: "Merriweather", serif;
}
```
*Utilities generated:* `font-display`, `font-serif`.

#### 3. Custom Screen Breakpoints (`--breakpoint-*`)
```css
@theme {
  --breakpoint-xs: 480px;
  --breakpoint-3xl: 1920px;
}
```
*Responsive prefixes generated:* `xs:grid-cols-1`, `3xl:flex-row`.

---

### Lesson 6.3: Mastering Dark Mode

By default, Tailwind v4 automatically matches the operating system's system settings (`prefers-color-scheme`). If a user has Dark Mode active on their phone/computer, `dark:` utility styles will render.

However, if you want to support a **manual theme toggle** (e.g., a "Sun/Moon" button in your navbar that lets the user switch themes explicitly), you can define a custom variant:

#### Step 1: Add a Custom Variant to your CSS
Add the following line to your global CSS file to tell Tailwind to look for a `.dark` class on the parent wrapper (usually the `<html>` or `<body>` element):

```css
@import "tailwindcss";

/* Define a manual class-based dark mode trigger */
@custom-variant dark (&:where(.dark, .dark *));
```

#### Step 2: Use CSS Variables in HTML
Now, when you add the `.dark` class to your `<html>` element, any `dark:` modifier classes on your page will automatically apply:

```html
<!-- Light background by default, black background when the parent has the `.dark` class -->
<body class="bg-white text-black dark:bg-black dark:text-white">
  <h1>Visual Title</h1>
</body>
```

---

### Practice Exercise 6.1

You can practice this in **[play.tailwindcss.com](https://play.tailwindcss.com/)**! 
1. Look at the top of the playground window. You will see three tabs: **HTML**, **CSS**, and **Config**.
2. Click on the **CSS** tab. Notice it says `@import "tailwindcss";`.
3. Erase whatever is there and paste the following theme config:

```css
@import "tailwindcss";

@custom-variant dark (&:where(.dark, .dark *));

@theme {
  --color-brand-green: #10b981;
  --color-brand-charcoal: #1e293b;
  --font-heading: "Trebuchet MS", sans-serif;
}
```

4. Now switch back to the **HTML** tab and paste the following element structure:

```html
<!-- Try adding "dark" to the class below to test the theme switch -->
<div class="min-h-screen flex items-center justify-center bg-stone-100 text-stone-900 transition-colors duration-300 dark:bg-stone-950 dark:text-stone-100">
  
  <div class="max-w-sm p-6 bg-white border border-stone-200 rounded-2xl shadow-sm transition-colors duration-300 dark:bg-brand-charcoal dark:border-stone-800">
    <h2 class="font-heading text-2xl font-bold text-brand-green">
      Design System Configured
    </h2>
    <p class="text-stone-500 text-sm mt-2 dark:text-stone-400">
      This card is using custom branding properties defined purely inside the CSS theme directive tab.
    </p>
  </div>

</div>
```

#### Your Tasks:
1. **Toggle Manual Dark Mode:** Look at the outer wrapper `div` in the HTML tab (`<div class="min-h-screen...`). Add the class **`dark`** to the very beginning of its classes list. Watch how the card background instantly switches to your custom charcoal color (`bg-brand-charcoal`).
2. **Experiment with New Colors:** Go back to the CSS tab. Change `--color-brand-green` to a different hex color (e.g., vibrant orange `#ff5500` or royal blue `#1e40af`). Switch back to the HTML tab and notice how the header text automatically updates to reflect your modified configuration.

Let me know how the CSS-first flow feels! Once you are ready, we will transition to **Phase 7: Component Reusability & Developer Workflow**.

