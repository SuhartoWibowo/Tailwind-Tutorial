### Phase 3: Layouts, Flexbox, and CSS Grid

With visual styling mastered, we now move into **Page Layouts**. This is where we learn how to structure page content, distribute space, align items, and build modern grids. 

We will break Phase 3 into three key lessons:
*   **Lesson 3.1: Flexbox Layouts** (One-dimensional layouts: alignments, wrapping, and gaps)
*   **Lesson 3.2: CSS Grid Layouts** (Two-dimensional layouts: columns, spans, and grids)
*   **Lesson 3.3: Positioning & Layering** (Relative, absolute, fixed, and coordinate systems)

Let's begin with **Lesson 3.1: Flexbox Layouts**.

---

### Lesson 3.1: Flexbox Layouts

Flexbox is a one-dimensional layout system, meaning it helps you arrange elements in either a **row** (horizontally) or a **column** (vertically). 

To turn on Flexbox, you apply the **`flex`** class to the parent container.

#### 1. Direction (`flex-row` vs. `flex-col`)
By default, applying `flex` arranges children horizontally.
*   **`flex-row`** (Default): Elements are aligned side-by-side.
*   **`flex-col`**: Elements are stacked on top of each other. This is incredibly common for sidebars, mobile menus, and forms.

#### 2. Alignment & Distribution
Flexbox makes aligning items simple:
*   **`items-*` (Cross Axis / Align Items):** Controls the vertical alignment of items in a row.
    *   `items-center` $\rightarrow$ Centers items vertically (highly recommended for navbars and list items).
    *   `items-start` / `items-end` $\rightarrow$ Aligns items to the top or bottom.
*   **`justify-*` (Main Axis / Justify Content):** Controls horizontal spacing.
    *   `justify-center` $\rightarrow$ Aligns elements to the center.
    *   `justify-between` $\rightarrow$ Pushes elements to opposite edges (e.g., Logo on the left, Menu on the right).
    *   `justify-end` $\rightarrow$ Aligns everything to the right edge.

#### 3. Modern Gaps (`gap-*`)
Instead of adding margins (`mr-4`) to every individual child in a flex row, you can define spacing on the parent wrapper using **`gap-*`**:
*   `gap-4` $\rightarrow$ Adds $16\text{px}$ of equal space between all flex children (both horizontally and vertically if wrapped).
*   `gap-x-4` / `gap-y-2` $\rightarrow$ Allows you to set different horizontal and vertical gaps independently.

#### 4. Flex Grow & Shrink (`grow` vs. `shrink-0`)
Sometimes, in a horizontal layout, you want one element to fill all the remaining space while keeping others fixed:
*   **`grow`**: Forces an element to expand and occupy any leftover space.
*   **`shrink-0`**: Prevents an element (such as an avatar image or an icon) from shrinking or squishing when other content next to it is too long.

---

### Practice Exercise 3.1

Let's design a clean **Media Navigation / User Row** using Flexbox alignment. Open **[play.tailwindcss.com](https://play.tailwindcss.com/)** and paste the following HTML:

```html
<div class="bg-slate-100 p-12 min-h-screen flex items-center justify-center">
  
  <!-- Main Nav Bar Card Container -->
  <div class="bg-white p-4 rounded-xl w-[450px] shadow-sm">
    
    <!-- User Info Wrapper -->
    <div>
      
      <!-- Avatar -->
      <div class="size-12 rounded-full bg-indigo-500 text-white flex items-center justify-center font-bold">
        AM
      </div>
      
      <!-- Text Area -->
      <div>
        <h4 class="text-slate-900 font-semibold text-sm">Alex Morgan</h4>
        <p class="text-slate-500 text-xs">active 5m ago</p>
      </div>
      
      <!-- Action Button -->
      <button class="bg-slate-100 hover:bg-slate-200 text-slate-700 text-xs px-3 py-1.5 rounded-lg font-medium">
        Message
      </button>
      
    </div>

  </div>
  
</div>
```

#### Your Tasks:
1. **Flex the Main Row:** Currently, the avatar, text, and button stack vertically. Add classes on the **User Info Wrapper** `div` to make it a horizontal row, align all items to the center vertically, and push the "Message" button to the far right. *Hint: Use `flex`, `items-center`, and `justify-between`.*
2. **Handle the Avatar and Text:** The avatar and the text are right next to each other because they are in the flex flow. Instead of using custom margins, wrap *only* the avatar and the text area `div` in an inner wrapper, turn on `flex`, align them to the center, and add a gap of 3 units (`gap-3`).
3. **Protect the Avatar:** To ensure the avatar is never squeezed if the user's name is exceptionally long, add **`shrink-0`** to the avatar `div`.

Once you have completed these steps, your layout elements should organize themselves cleanly across the card. Paste your updated HTML or let me know when you are ready for **Lesson 3.2: CSS Grid Layouts**!

### Lesson 3.2: CSS Grid Layouts

While Flexbox works beautifully for single rows or single columns, **CSS Grid** is designed for two-dimensional layouts—meaning you want to control both columns and rows at the same time. 

Grid is ideal for building dashboard layouts, photo galleries, card grids, or full-page layouts.

To turn on Grid, apply the **`grid`** class to the parent container.

---

#### 1. Defining Columns (`grid-cols-*`)
By default, a grid has only one column. To split your layout into multiple equal columns, you tell the parent container how many columns to create:
*   `grid-cols-2` $\rightarrow$ Splits the container into 2 equal columns.
*   `grid-cols-3` $\rightarrow$ Splits it into 3 columns.
*   `grid-cols-4` to `grid-cols-12` $\rightarrow$ Up to 12 columns.

Any child element placed inside this parent will automatically fall into the next available cell.

---

#### 2. Spanning Columns & Rows (`col-span-*` & `row-span-*`)
Sometimes you don't want all items to be the exact same size. You can tell a specific child element to stretch across multiple grid tracks:
*   **`col-span-2`**: Forces a single item to span across 2 columns.
*   **`col-span-full`**: Forces an item to stretch across the entire width of the grid, regardless of how many columns are defined.
*   **`row-span-2`**: Forces an item to span vertically across 2 rows.

---

#### 3. Setting Grid Spacing (`gap-*`)
Just like Flexbox, spacing out grid cells is handled entirely on the parent container using the **`gap-*`** scale:
*   `gap-6` $\rightarrow$ Separates all cards by $24\text{px}$ (both horizontally and vertically).
*   `gap-x-8` / `gap-y-4` $\rightarrow$ Sets independent horizontal and vertical gap widths.

---

### Flexbox vs. CSS Grid: Quick Guideline
*   Use **Flexbox** (`flex`) when you want to align a small row of elements, like a button next to an input, a navigation bar, or list items.
*   Use **CSS Grid** (`grid`) when you are laying out structured containers, card directories, dashboard metrics, or a page’s macro layout.

---

### Practice Exercise 3.2

Let's build a functional **Dashboard Metrics Grid**. Open **[play.tailwindcss.com](https://play.tailwindcss.com/)** and replace your code with the following template:

```html
<div class="bg-slate-900 p-12 min-h-screen flex items-center justify-center text-white">
  
  <!-- Grid Parent Container -->
  <div>
    
    <!-- Card 1: Total Users -->
    <div class="bg-slate-800 p-6 rounded-xl border border-slate-700">
      <p class="text-sm text-slate-400 font-medium">Total Users</p>
      <p class="text-3xl font-black mt-2">12,482</p>
    </div>

    <!-- Card 2: Active Subscriptions -->
    <div class="bg-slate-800 p-6 rounded-xl border border-slate-700">
      <p class="text-sm text-slate-400 font-medium">Active Subs</p>
      <p class="text-3xl font-black mt-2">1,843</p>
    </div>

    <!-- Card 3: Monthly Revenue -->
    <div class="bg-slate-800 p-6 rounded-xl border border-slate-700">
      <p class="text-sm text-slate-400 font-medium">Monthly Revenue</p>
      <p class="text-3xl font-black mt-2">$42,850</p>
    </div>

    <!-- Card 4: Wide Analytics/Promo Widget -->
    <div class="bg-indigo-600 p-6 rounded-xl">
      <p class="text-sm text-indigo-200 font-medium font-bold">Analytics Note</p>
      <p class="text-sm text-white/80 mt-2">Traffic is up 12% this week compared to last month. Keep optimizing your image configurations for better performance.</p>
    </div>

  </div>
  
</div>
```

#### Your Tasks:
1. **Initialize the Grid:** On the outer **Grid Parent Container** `div`, turn on the CSS grid and tell it to display **3 columns**. *Hint: Use `grid` and `grid-cols-3`.*
2. **Add Spacing:** Space out all the cards in the grid by $24\text{px}$. *Hint: Use `gap-6` on the parent.*
3. **Span the Wide Widget:** The last card (the Indigo card) looks crushed inside a single 3-column cell. Make it span across **two columns** so that it matches the visual weight of the rest of the dashboard. *Hint: Use `col-span-2` on the Card 4 container.*

Once you run this in the playground, you will see how cleanly CSS Grid organizes distinct containers. Paste your updated HTML or ask any questions, and we will move to **Lesson 3.3: Positioning & Layering**!

### Lesson 3.3: Positioning & Layering

To finish Phase 3, we will cover **CSS Positioning**. 

By default, elements on a webpage flow in order, one after the other. However, you often need to override this behavior—such as placing a "New" badge on the top corner of a card, pinning a navigation bar to the top of the viewport, or overlapping elements.

---

#### 1. Positioning Contexts
*   **`relative`**: Keeps the element in the normal document flow but turns it into a **boundary parent**. Any child element with `absolute` positioning will anchor itself to this container instead of the whole screen.
*   **`absolute`**: Removes the element entirely from the document flow. You can place it anywhere inside its nearest `relative` parent using coordinate classes.
*   **`fixed`**: Pins an element relative to the entire browser window (viewport). Even if the user scrolls, a fixed element stays in the exact same spot (often used for headers, sidebars, or modal backgrounds).
*   **`sticky`**: Acts like a normal element until you scroll past it, at which point it "sticks" to the edge of the screen (commonly used for table headers or persistent sub-navigation menus).

---

#### 2. Coordinate Utilities
Once you apply `absolute`, `fixed`, or `sticky`, you must tell Tailwind where to place the element using directions and spacing values:
*   **Direct Placement:** `top-0`, `bottom-4`, `left-6`, `right-2`.
*   **All Directions at Once:** **`inset-0`** is a useful shortcut that sets top, bottom, left, and right to `0` at the same time. This is perfect for full-screen dim overlays or wrapping an image fully.

---

#### 3. Z-Index Layering (`z-*`)
When elements overlap, you need to control which one sits on top. Tailwind uses a standard z-index scale:
*   `z-0` (default)
*   `z-10`, `z-20`, `z-30`, `z-40`, `z-50` (higher numbers stack on top of lower numbers)
*   `z-auto`

---

### Practice Exercise 3.3

Let's build a **Product Card with an Overlaid "Popular" Badge**. Open **[play.tailwindcss.com](https://play.tailwindcss.com/)** and paste the following HTML:

```html
<div class="bg-slate-100 p-12 min-h-screen flex items-center justify-center">
  
  <!-- Product Card Container -->
  <div class="bg-white w-80 rounded-2xl shadow-sm overflow-hidden">
    
    <!-- Image Area with absolute placeholder -->
    <div class="bg-indigo-600 h-48 flex items-center justify-center text-white">
      Image Area
      
      <!-- Overlay Badge -->
      <span class="bg-amber-500 text-slate-900 text-xs font-bold px-3 py-1 rounded-full uppercase tracking-wider">
        Popular
      </span>
    </div>
    
    <!-- Product Details -->
    <div class="p-6">
      <h3 class="font-bold text-slate-900 text-lg">Wireless Headphones</h3>
      <p class="text-slate-500 text-sm mt-1">$129.99</p>
    </div>

  </div>
  
</div>
```

#### Your Tasks:
1. **Prepare the Parent Boundary:** The "Popular" badge is currently sitting inside the Image Area but isn't positioned correctly. Add the **`relative`** class to the Image Area `div` to make it the boundary container.
2. **Reposition the Badge:** Add classes to the **Overlay Badge** `span` to pluck it out of the normal layout and pin it exactly $16\text{px}$ from the top and $16\text{px}$ from the right of the Image Area. *Hint: Use `absolute`, `top-4`, and `right-4`.*
3. **Pin a Header (Bonus Concept):** Change the outer class of the page (`<div class="bg-slate-100...`) to instead have an absolute banner at the top of the entire screen. Take a look at how applying `absolute top-0 left-0 w-full` affects the layout.

---

### Phase 3 Milestone Project: Responsive Layout System

You have completed Phase 3! Now, let’s combine **Flexbox (3.1)**, **CSS Grid (3.2)**, and **Positioning (3.3)** into a structural project.

**Your Goal:** Build a **Responsive 3-Column Pricing Page** or a **Dashboard Layout** in Tailwind Play.

**Requirements:**
*   A page wrapper that centers your work on the screen.
*   A responsive columns grid (e.g. `grid-cols-1` wrapping to `grid-cols-3` or three equal columns side-by-side) with a robust `gap-6`.
*   At least one card marked as "Featured" or "Most Popular". 
*   Use `relative` and `absolute` to overlay a prominent badge on your "Featured" card.
*   Use Flexbox (`flex`, `items-center`, `justify-between`) inside the cards to align the features lists and CTA buttons.

Compile your work in the playground, test how elements stack, and paste your HTML here when you are ready. We can evaluate your structural logic and proceed directly to **Phase 4: State Variants, Forms, & Transitions**!
