# CSS/SCSS Standards

This guide assumes the use of the [Sass](http://www.sass-lang.com) preprocessor, or PostCSS processing [configured to mimic nesting styles](https://github.com/jonathantneal/precss). The [traditional](http://sass-lang.com/documentation/file.SASS_REFERENCE.html#syntax) (SCSS) variant of Sass should be used, keeping the original SCSS as visually close to vanilla CSS as possible.

## Table of Contents
<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->


- [General Principals](#general-principals)
- [Terminology](#terminology)
  - [Rule declaration](#rule-declaration)
  - [Selectors](#selectors)
  - [Properties](#properties)
- [File Naming and Structure](#file-naming-and-structure)
  - [Folder Organization](#folder-organization)
  - [Partials](#partials)
- [Variables & Configuration](#variables--configuration)
- [Formatting](#formatting)
  - [ID selectors](#id-selectors)
  - [Spacing](#spacing)
  - [Nesting](#nesting)
  - [Quotes](#quotes)
  - [Comments](#comments)
- [Syntax](#syntax)
  - [Components](#components)
  - [Descendants](#descendants)
  - [Modifiers](#modifiers)
  - [States](#states)
- [Thanks](#thanks)
- [License](#license)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## General Principals
> "Part of being a good steward to a successful project is realizing that
> writing code for yourself is a Bad Idea™. If thousands of people are using
> your code, then write your code for maximum clarity, not your personal
> preference of how to get clever within the spec." - Idan Gazit

* Don't try to prematurely optimize your code; keep it readable and
  understandable.
* All code in any code-base should look like a single person typed it, even
  when many people are contributing to it.
* Strictly enforce the agreed-upon style.
* If in doubt when deciding upon a style use existing, common patterns.

## Terminology

The following are some terms used throughout this styleguide.

### Rule declaration

A “rule declaration” is the name given to a selector (or a group of selectors) with an accompanying group of properties. Here's an example:

```sass
.avatar {
  font-size: 18px;
  line-height: 1.2;
}
```

### Selectors

In a rule declaration, “selectors” are the bits that determine which elements in the DOM tree will be styled by the defined properties. Selectors can match HTML elements, as well as an element's class, ID, or any of its attributes. Here are some examples of selectors:

```sass
.avatar {
  font-size: 20px;
}

#id {
  font-size: 20px;
}
```

### Properties

Finally, properties are what give the selected elements of a rule declaration their style. Properties are key-value pairs, and a rule declaration can contain one or more property declarations. Property declarations look like this:

```sass
.avatar {
  background: rgb(255,255,255);
  color: rgb(33,33,33);
}
```

## File Naming and Structure

### Folder Organization

Grouping style declarations into folders makes it easier to quickly find rules that are related, and makes it much easier for future designers and developers to find rules that need to be changed.

```sh
styles/
styles/main.scss
styles/config
styles/config/_colors.scss
styles/config/_typography.scss
styles/common/_grid.scss
styles/mixins/_icons.scss
styles/components/avatar/_avatar.scss
```

### Partials

Stylesheets should be broken up into multiple [partials](http://www.sass-lang.com/guide#topic-4), each prefixed with an underscore to inform the Sass interperter the file is not to be built as a standalone stylesheet. Each partial should be related, with emphasis on grouping an entire component by file or folder.

## Variables & Configuration

Variables like font stacks, colors and other theme related preferences should be grouped by concern and placed together into a `config/` folder. If supporting multiple themes each theme should have it's own `config/` folder.

## Formatting

The following are some high level page formatting style rules.


### ID selectors

While it is possible to select elements by ID in CSS, it should generally be considered an anti-pattern. ID selectors introduce an unnecessarily high level of [specificity](https://developer.mozilla.org/en-US/docs/Web/CSS/Specificity) to your rule declarations, and they are not reusable.

For more on this subject, read [CSS Wizardry's article](http://csswizardry.com/2014/07/hacks-for-dealing-with-specificity/) on dealing with specificity.


### Spacing

CSS rules should be comma separated and leave on a new line:

```sass
/* wrong */
.avatar, .tweet {

}
```

```sass
/* right */
.avatar, 
.tweet {

}
```

Properties should use a space after `:` but not before:

```sass
/* wrong */
.avatar {
  font-size : 12px;
}

.tweet {
  font-size:12px;
}
```

```sass
/* right */
.avatar {
  font-size: 12px;
}
```


Rule declarations should have one property per line:

```sass
/* wrong */
.avatar {
  font-size: 12px; letter-spacing: 2px;
}
```

```sass
/* right */
.avatar {
  font-size: 12px; 
  letter-spacing: 2px;
}
```

Declaration should be separated by two new lines:

```sass
/* wrong */
.avatar {
  font-size: 12px;
}
.tweet {
  letter-spacing: 2px;
}
```

```sass
/* right */
.avatar {
  font-size: 12px;
}

.tweet {
  letter-spacing: 2px;
}
```

### Nesting

Do not nest elements. Keep nesting to pseudo-classes and direct interactions with the parent element. Although nesting is a powerful feature provided by Sass and PostCSS plugins, it can easily get out of control and generate terrible css ouput with high specificity or spoil the code legibility.

```sass
/* wrong */
.avatar {
  font-size: 12px;
  
  &:hover {
    font-size: 11px;
  }
  
  &__link {
    color: rgb(210,210,22);
  }

  &__photo {
    height: 20px;
  }
}
```

```sass
/* right */
.avatar {
  font-size: 12px;
  
  &:hover {
    font-size: 11px;
  }
}

.avatar__link {
  color: rgb(210,22,221);
}

.avatar__photo {
  height: 20px;
}
```

Nesting can also be used to when an element is dependent of a parent's modifier. This helps to keep all code related to an element on the same block.

```sass
.avatar {
  font-size: 12px;
}

.avatar__photo {
  height: 20px;
  
  .avatar--big & {
    height: 40px;
  }
}
```

### Quotes

Quotes are optional in CSS. You should use single quotes as it is visually clearer that the string is not a selector or a style property.

```sass
/* wrong */
.avatar {
  background-image: url(/img/you.jpg);
  font-family: Helvetica Neue Light, Helvetica Neue, Helvetica, Arial;
}
```

```sass
/* right */
.avatar {
  background-image: url('/img/you.jpg');
  font-family: 'Helvetica Neue Light', 'Helvetica Neue', Helvetica, Arial;
}

```

### Comments

Avoid freeform comments, instead consider using [SassDoc](http://sassdoc.com/) to document a component. Freeform comments are not easily mantainable and are usually used to supress application design mistakes. Leave freeform comments only to things that are **really** not straightforward such as browser-specific hacks. Put comments on their own lines to describe content below them.

```sass
/* wrong */
.avatar {
  height: 200px; /* this is the height of the container*/
  background-color: rgb(221,33,21); /* brand color */
}
```

```sass
/* right */
.avatar {
  height: 20px;
  
  /* this is a hack to fix click behavior on Safari 6.0 */
  pointer-events: none;
}
```

## Syntax

[BEM Syntax](https://css-tricks.com/bem-101): `<component-name>[--modifier-name|__descendant-name]`

Component driven development offers several benefits when reading and writing HTML and CSS:

* It helps to distinguish between the classes for the root of the component, descendant elements, and modifications.
* It keeps the specificity of selectors low.
* It helps to decouple presentation semantics from document semantics.

You can think of components as custom elements that enclose specific semantics, styling, and behaviour.

### Components 

Syntax: `component-name`

The component's name must be written in kebab case.

```sass
.my-component {
  font-size: 20px;
}
```

```html
<article class="my-component"></article>
```

### Descendants

Syntax: `component-name__descendant-name`

A component descendant is a class that is attached to a descendant node of a component. It's responsible for applying presentation directly to the descendant on behalf of a particular component. Descendant names must be written in kebab case.

```html
<article class="tweet">
  <header class="tweet__header">
    <img class="tweet__avatar" src="{$src}" alt="{$alt}">
    …
  </header>
  <div class="tweet__body">
    …
  </div>
</article>
```

### Modifiers

Syntax: `component-name--modifier-name`

A component modifier is a class that modifies the presentation of the base component in some form. Modifier names must be written in kebab case and be separated from the component name by two hyphens. The class should be included in the HTML _in addition_ to the base component class.

```sass
.btn {
  padding: 20px 10px;
}

.btn--primary { 
  background: rgb(148,146,231);
}
```

```html
<button class="btn btn--primary">…</button>
```

### States

Syntax: `component-name.is-state-of-component`

Use `is-stateName` for state-based modifications of components. The state name must be kebab case. **Never style these classes directly; they should always be used as an adjoining class.**

Javascript can be used to toggle these classes. This means the same state names can be used in multiple contexts, but each component must define its own styles for the state (as they are scoped to the component).

```sass
.tweet { 
  height: 90px;
}

.tweet.is-expanded { 
  height: 200px;
}
```

```html
<article class="tweet is-expanded"></article>
```

## Thanks

Modified from the fantasic [*Opinionated CSS styleguide for scalable applications*](https://github.com/grvcoelho/css-styleguide) by [Guilherme Rv Coelho](https://github.com/grvcoelho)

## License

[MIT](https://github.com/grvcoelho/css/blob/master/LICENSE) &copy; 2016