# SCSS starter

[![MIT license](https://img.shields.io/badge/license-MIT-yellow.svg?style=flat-square)](https://opensource.org/licenses/MIT)

SCSS self-documented starter for any kind of project: grid, helpers and guidelines to keep your CSS light, legible and clean, making it highly maintainable without effort.

[Read guidelines](scss/README.md)

---

## About
Regular CSS frameworks predefine a huge amount of classes, in a OOCSS-like approach, altering the legibility and maintainability of your style, often ending in a cascading chaos when several developers contribute in a single project. They are better suited for admin panels and prototypes, but when it comes to integrating commissioned interfaces, they bring far more mess than cohesion.

This starter is meant as a SCSS toolbox instead of a standalone CSS framework, and serves modular mixins and placeholder classes to extend your own components, preserving your namespace and your DOM.

## Benefits
- Highly flexible grid, that could have instances of different configuration.
- Focused on essentials: reset, breakpoints and grid.
- Mixins and helpers prevent loading unused style.
- Low compilation time.
- Self documented core components.
- Keeps the DOM legible and straightforwards.
- Keeps style in stylesheets only.
- Keeps the cascade clean and avoid heavy selectors.
- Components make writing evolutions effortless.
- Equally suitable for any kind of project.
- Lightweight.

## FAQ

1. [OOCSS prevents code duplication and respects the cascade, right?](#1-oocss-prevents-code-duplication-and-respects-the-cascade-right)
2. [How could your grid be better than Bootstrap or Foundation?](#2-how-could-your-grid-be-better-than-bootstrap-or-foundation)
3. [Frameworks serve useful components like form fields, dropdowns, nav and sliders, why avoid them?](#3-frameworks-serve-useful-components-like-form-fields-dropdowns-nav-and-sliders-why-avoid-them)
4. [Including mixins duplicates code and extending helpers create confusion, isn’t that bad?](#4-including-mixins-duplicates-code-and-extending-helpers-create-confusion-isnt-that-bad)

### 1. OOCSS prevents code duplication and respects the cascade, right?
Production OOCSS projects all end up with an absurd amount of undocumented classes you should guess how to combine them, and the cascade still takes efforts to dive into. You need to go back and forth DOM and stylesheets to understand how properties apply. With a component based approach, your DOM looks more like this:

```html
<section class="Blog">
  <div class="Blog-wrap">
    <article class="Blog-item is-highlighted">
      <header class="Blog-item-header">
        <h1 class="Blog-item-header-title">…</h1>
        <p class="Blog-item-header-excerpt">…</p>
        <time class="Blog-item-header-date">…</time>
      </header>
      <!-- … -->
    </article>
    <!-- … -->
  </div>
</section>
```

In a glimpse, you just know that style for the blog will be exclusive to the `.Blog-*` component and you could start writing evolutions right know.

### 2. How could your grid be better than Bootstrap or Foundation?
This flexbox grid is highly adaptive without polluting the namespace: it's a set of mixins that you include and configure when needed on your components, allowing you to choose different gap values, columns count and responsive behaviors across the same project. It counts column in the most natural way—not in subdivision of 12 or 16 columns—, and allow breakpoint specificity. With the same clean DOM of the above example, a typical grid component looks like this:

```scss
.Blog {
  @include grid(20px); // 20px is the gap width

  &-wrap {
    @include row((sm: 2, md: 3, lg: 4)); // split into 2 columns in small screen, 3 in medium…
  }

  &-item {
    // default article is 1 column wide

    &.is-highlighted {
      @include column((sm: 2, md: 3, lg: 2));  // full width in small/medium, half width in large
    }
  }
}
```

### 3. Frameworks serve useful components like form fields, dropdowns, nav and sliders, why avoid them?
From experience, all these components vary between projects, and way too often even between pages of a same project—they always need customization, causing a cascade saturation. Better write your own bank of standalone helpers, mixins and components that you could include only if needed. Most of the time, it consumes less time writing the needed components than customizing a framework, that may generate critical side-effects.

### 4. Including mixins duplicates code and extending helpers create confusion, isn’t that bad?
The fear of duplicates in CSS is kind of absurd, and even worse when a heavy framework stylesheet gets loaded. You either end up with a huge list of selectors matching the same properties, or the same properties duplicated into that same huge amount selectors. For the cascade's sake, it's often better to duplicate code. But I agree, some components having a similar behavior like a grid, form fields, etc. could be easily assembled into an extendable helper or a standalone component like `.Button`, `%4x4-grid`, `%input`, `%dropdown`, etc. Extending becomes harmful when it comes to keeping the OOCSS logic inside preprocessors: that just moves the DOM mess into the stylesheets; however, it remains a powerful and clean tool when used sparingly.
