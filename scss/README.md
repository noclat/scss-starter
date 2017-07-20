# Guidelines

## Naming convention

```scss
.ComponentName-descendantName {}
.ComponentName-descendantName.modifier {}
.ComponentName-descendantName.is-stateName {} // or .has-* or .not-* etc.
.u-utilityClass {}
```

**JS-only selectors**: `#ID`, `.js-selectorName`, `[data-attr-name]`.

## Defining styles

Try to:

- avoid styling over ID selectors,
- avoid using `!important`,
- avoid nesting selectors, except for:

```scss
// Element states & pseudo-elements
.CustomElement {
    color: black;

    &:hover, &:focus { color: red; }
    &.active { color: green; }
    &.disabled { color: gray; }
    &.is-customState { color: blue; }
}

// Making components: compiled CSS won't be nested
.Component {
    &-title { … } // compiles into `.Component-title { … }`
    &-subtitle { … } // compiles into `.Component-subtitle { … }`
}

// Parents modifiers
.CustomElement {
    background: black; // default background

    // .Wrapper is a standalone component, here child of .CustomElement
    .Wrapper.red & { background: red; }
    .Wrapper.blue & { background: blue; }
}

// Lists and consistent DOM trees
.CustomNav {
    ul { list-style: none; }

    li {
        display: inline-block;
        &.active a { text-decoration: underline; }
    }
}
```

- avoid duplicating behaviors, prefer using `%selector` helpers:

```scss
%Component-heading {
    // common styles
}

.Component-title {
    @extend %Component-heading;
    // specific styles
}

.Component-subtitle {
    @extend %Component-heading;
    // specific styles
}
```

## Applying styles

Try to keep your DOM straightforwards, classes must be explicit inside a component.

Try to keep the classes in that order: **component, modifiers, utilities, js**.

```html
<ul class="HomeNav snap js-snap">
    <!-- … -->
    <li class="HomeNav-item u-uppercase">
        <!-- … -->
    </li>
</ul>
```
