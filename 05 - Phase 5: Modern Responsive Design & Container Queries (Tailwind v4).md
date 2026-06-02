### Phase 5: Modern Responsive Design & Container Queries (Tailwind v4)

In this phase, you will learn how to make your layouts adapt gracefully to any screen size. We will cover the standard **mobile-first media query** system (based on the screen viewport) and **modern container queries** (where components adjust their design based on the size of their immediate parent element).

We will break Phase 5 into two essential lessons:
*   **Lesson 5.1: Viewport Responsive Design (Mobile-First)**
*   **Lesson 5.2: Container Queries in Tailwind v4**

---

### Lesson 5.1: Viewport Responsive Design (Mobile-First)

Tailwind utilizes five default responsive breakpoints based on the width of the browser viewport:
*   **`sm:`** $\rightarrow$ 640px and up (tablets/large phones)
*   **`md:`** $\rightarrow$ 768px and up (small laptops/tablets)
*   **`lg:`** $\rightarrow$ 1024px and up (desktops)
*   **`xl:`** $\rightarrow$ 1280px and up (large desktop screens)
*   **`2xl:`** $\rightarrow$ 1536px and up (ultra-wide monitors)

#### 1. The Mobile-First Philosophy
In Tailwind, **every utility class without a prefix applies to mobile screens first.** Breakpoints are minimum-width overrides. 

For example, if you write `class="w-full md:w-1/2"`, the element will occupy 100% of the screen width on mobile, and then scale down to 50% width *only* when the screen size reaches 768px (`md`) or larger.

##### The "Mobile-First" Rule of Thumb:
Always design your mobile screen layout first, and then add prefix overrides (like `md:`, `lg:`) to scale elements up or reposition them for larger viewports.

**Example Code:**
```html
<!-- Mobile: Stacks vertically (flex-col), 16px padding (p-4), small text -->
<!-- Tablet & Up: Horizontal row (md:flex-row), 32px padding (md:p-8), larger text -->
<div class="flex flex-col p-4 md:flex-row md:p-8">
  <h2 class="text-sm md:text-lg">Responsive Heading</h2>
</div>
```

---

### Lesson 5.2: Container Queries (Tailwind v4)

Traditionally, media queries look at the size of the **browser viewport**. But what if you are building a reusable "Product Card" component? 
*   If you place that card in a wide main dashboard, it should display in a spacious horizontal layout.
*   If you place that exact same card in a narrow sidebar, it must display vertically.

Because viewports don't change when you move elements inside sidebars, viewport media queries (`md:`) fail here. 

In Tailwind v4, **Container Queries** are built directly into the core engine. They let you style elements based on the width of their **parent element** instead of the whole screen.

#### 1. How to Use Container Queries
1.  **Mark the parent container** with the **`@container`** class.
2.  **Style the child elements** using **`@` prefixed** responsive variants:
    *   `@sm:` $\rightarrow$ apply styles when the parent is 640px or wider.
    *   `@md:` $\rightarrow$ apply styles when the parent is 768px or wider.
    *   `@lg:` $\rightarrow$ apply styles when the parent is 1024px or wider.
    *   **Max-Width variants:** You can also use `@max-md:` or `@max-sm:` to apply styles *only below* a certain container size.

**Example Code:**
```html
<!-- 1. Mark the outer card container -->
<div class="@container bg-slate-800 p-4">
  
  <!-- 2. The layout stacks vertically on mobile/small containers -->
  <!-- But switches to a side-by-side row if the parent container hits 768px wide -->
  <div class="flex flex-col @md:flex-row gap-4">
    <div class="size-20 bg-indigo-500"></div>
    <div>Description</div>
  </div>
  
</div>
```

---

### Practice Exercise 5.1 & 5.2

Let's build a dual-purpose layout combining **Viewport queries** (to lay out sidebars and grids) and **Container queries** (to allow individual cards to adapt automatically depending on where they land).

Open **[play.tailwindcss.com](https://play.tailwindcss.com/)** and paste this starting layout:

```html
<div class="bg-slate-950 p-6 min-h-screen text-white">
  
  <!-- Outer Page Layout: Viewport responsive grid -->
  <!-- Mobile: 1 column | Desktop (lg): 3 columns (Sidebar on left, main content on right) -->
  <div class="grid grid-cols-1 lg:grid-cols-3 gap-6">
    
    <!-- Left Column (Narrow Sidebar) -->
    <div class="bg-slate-900 p-4 rounded-2xl border border-slate-800 space-y-4">
      <h3 class="text-sm font-semibold text-slate-400">Sidebar (Narrow)</h3>
      
      <!-- Reusable Widget 1 -->
      <div class="bg-slate-800 p-4 rounded-xl">
        <div class="flex flex-col gap-3">
          <div class="h-24 bg-indigo-500 rounded-lg"></div>
          <div>
            <h4 class="font-bold">Active Servers</h4>
            <p class="text-slate-400 text-xs mt-1">Status check is complete.</p>
          </div>
        </div>
      </div>
      
    </div>

    <!-- Right Column (Wide Workspace) -->
    <div class="lg:col-span-2 bg-slate-900 p-4 rounded-2xl border border-slate-800 space-y-4">
      <h3 class="text-sm font-semibold text-slate-400">Main Content (Wide)</h3>
      
      <!-- Reusable Widget 2 (Exact duplicate) -->
      <div class="bg-slate-800 p-4 rounded-xl">
        <div class="flex flex-col gap-3">
          <div class="h-24 bg-indigo-500 rounded-lg"></div>
          <div>
            <h4 class="font-bold">Active Servers</h4>
            <p class="text-slate-400 text-xs mt-1">Status check is complete.</p>
          </div>
        </div>
      </div>
      
    </div>

  </div>
  
</div>
```

#### Your Tasks:
1. **Apply the Container Query:**
   * Look at both **Widget 1** and **Widget 2**. They are identical. On the wrapping element of both widgets (`<div class="bg-slate-800 p-4...`) add the class **`@container`**.
2. **Make the Widgets Adapt to Parent Widths:**
   * Inside the widgets, locate the inner layout wrapper (`<div class="flex flex-col gap-3">`).
   * We want these widgets to stack vertically by default (`flex-col`), but if the widget gets placed in a wide space (such as the Main Content area), it should split horizontally.
   * Change that inner wrapper to: **`flex flex-col @md:flex-row @md:items-center`**.
   * Size the blue image box: on the image placeholder (`<div class="h-24 bg-indigo-500 rounded-lg">`), change it to: **`h-24 @md:h-20 @md:w-32`**.

Once you apply these classes in the playground, look at the preview. Notice how **Widget 2** automatically converts to a side-by-side row, while **Widget 1** stays stacked in a neat vertical column!

---

### Phase 5 Milestone Project: Responsive Layout System

You have successfully completed Phase 5! Let's build a clean, production-grade responsive environment.

**Your Goal:** Build a **Responsive Article Hub Grid** in Tailwind Play.

**Requirements:**
*   A responsive outer layout: displays 1 column on mobile devices and scales to a multi-column card layout on desktops.
*   Construct a reusable card component that uses **Container Queries**.
*   When placed in wide columns, the card should layout horizontally (Image on left, text on right).
*   When placed in narrow columns (or on smaller devices), the card should layout vertically (Image on top, text on bottom).
*   All spacings and font sizes must scale cleanly using viewport modifiers (e.g. smaller text on mobile screens, larger text on desktops).

Save your work, play with the browser scaling, and paste your HTML here when you are ready to transition to **Phase 6: Design Systems and CSS-First Theme Configuration (v4 paradigm)**!

