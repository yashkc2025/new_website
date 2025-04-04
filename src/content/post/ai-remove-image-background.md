---
layout: ../../layouts/post.astro
title: The definitive guide to SASS
description: Sass is a preprocessor scripting language that is interpreted or compiled into Cascading Style Sheets.
dateFormatted: September 20, 2022
---

CSS which stands for Cascading Style Sheets is a language used to style the web. Giving it all the colors, fonts, and layouts you see on the web thus enriching the User Experience

> But, it too has shortcomings. Like you can't use any functions or mixins. Where are Control Directives ?

This is where SASS comes into play. SASS is a CSS preprocessor which means it is a language that extends CSS. It adds features that aren't available in CSS yet like variables, nesting, mixins, inheritance and other cool stuff.

Prior to deployment the SASS code is compiled into regular CSS so that the browser can read it.

Warning: SASS has two syntaxes:

- .scss: A superset of CSS
- .sass: Uses indentation instead of curly braces and semicolons to describe the format of the document.

In this guide we will be exploring the .scss syntax.

## Installing SASS

nstalling SASS is quick and simple like any other module. Just run the following command in your terminal:

```bash
npm install -g sass
```

## Variables

Variables are a way to store information that you want to reuse throughout your stylesheet. In SASS, variables are declared using the $ symbol followed by the variable name.

This is particulary useful when you want to use a value at multiple places. Also, you can just change the value of the variable and it will be reflected everywhere 😉

Changing the value at 100 places manually is a nightmare. Isn't it ?

```scss
$primary-color: #333;

body {
  color: $primary-color;
}
```

Here, the above code when compiled results in:

```css
body {
  color: #333;
}
```

When SASS is compiled, it replaces the variable with the value assigned to it.

## Nesting

Nesting refers to the process of placing selectors inside other selectors in order to create a hierarchy of CSS rules.

This is how you would do it in CSS:

```css
div a {
  color: red;
}

div ul {
  display: flex;
}

div h1 {
  font-size: 2rem;
}
```

But, in SASS you can nest the selectors like this:

```scss
iv {
  a {
    color: red;
  }

  ul {
    display: flex;
  }

  h1 {
    font-size: 2rem;
  }
}
```

Now, tell me which method seems more clean and dev friendly.

## Mixins

Suppose you want to use a particular set of CSS properties at multiple places.

How would you achieve it ? For a single value you can use variables but what about multiple values ?

By using Mixins you can declare a set of CSS properties under one single name and reuse them everywhere you want

```scss
@mixin flex-center {
  display: flex;
  justify-content: center;
  align-items: center;
}
```

This is the code to ceter child elements inside a parent element.

Now, you can use this mixin anywhere you want by using the `@include` directive.

```scss
div {
  @include flex-center;
  // this will include all the properties defined in the mixin
}

ul {
  @include flex-center;
}
```

## Functions

As devs, we all love functions. They are a way to store a set of instructions that you want to use again and again.

SASS provides a lot of built-in functions like `lighten()`, `darken()`, `saturate()`, `desaturate()` etc.

To define a custom function you can use the `@function` directive.

```scss
@function add($a, $b) {
  @return $a + $b;
}
```

This will return the sum of the two numbers. You might need these while designing your own UI library.

Use them like :

```scss
div{
    width: add(10px, 20px); # returns 30px
}
```

## Ampersand Operator

Ah! This is my personal favorite. The reason why people love SASS so much.

The Ampersand operator & is used to refer to the parent selector.

Here's a quick example:

```scss
.btn {
  &.green {
    background-color: green;
  }
}
```

Compile the code and you will recieve:

```scss
.btn.green {
  background-color: green;
}
```

Warning: `.btn.green` is not the same as `.btn .green`

This will style the element containing both the classes `.btn` and `.green`. Setting the background color to green.

### Selecting a Psuedo Class

```scss
.btn {
  &:hover {
    background-color: red;
  }

  &:active {
    background-color: blue;
  }

  &:focus {
    background-color: yellow;
  }
}
```

`:hover` is a psuedo class. It is activated only when the user hovers over the element.

The CSS equivalent for this would be:

```scss
.btn:hover {
  background-color: red;
}

.btn:active {
  background-color: blue;
}

.btn:focus {
  background-color: yellow;
}
```

### Breaking up classes

What if you have multiple classes like `.btn`, `.btn-primary`, `.btn-secondary` etc. and you want to style them differently ?
You can use the ampersand operator along with `-` to break em up.

```scss
.btn {
  background-color: green;

  &-primary {
    background-color: red;
  }

  &-secondary {
    background-color: blue;
  }
}
```

This will compile to:

```scss
.btn {
  background-color: green;
}

.btn-primary {
  background-color: red;
}

.btn-secondary {
  background-color: blue;
}
```

## Control Directives

Control Directives are similar to conditional statements in programming languages. Check the following example:

```scss
$primary-color: red;

body {
  @if $primary-color == red {
    background-color: red;
  } @else if $primary-color == blue {
    background-color: blue;
  } @else {
    background-color: green;
  }
}
```

SASS supports the following control directives:

-`@if` -`@else if` -`@else` -`@for` -`@each` -`@while`

#### `@while` Directive

Let's say you have to generate a set of classes with different font sizes. Instead of writing them manually you can use the `@while` directive.

```scss
$i: 1;

@while $i < 5 {
  .font-#{$i} {
    font-size: #{$i}rem;
  }
  $i: $i + 1;
}
```

I know, I know ! It looks messy, but let me explain.

The `@while` directive check if `$i` is less than `5`. If it is, it will generate a class with the font size equal to the value of `$i` and increment `$i` by `1` unless $i is equal to `5`.

This results in :

```scss
.font-1 {
  font-size: 1rem;
}

.font-2 {
  font-size: 2rem;
}

.font-3 {
  font-size: 3rem;
}

.font-4 {
  font-size: 4rem;
}
```

#### `@each` Directive

The `@each` directive is used to iterate over a list of values.

```scss
$colors: red, blue, green;
// this is a list of colors

@each $color in $colors {
  .#{$color} {
    background-color: $color;
  }
}
```

This will generate the following classes:

```scss
.red {
  background-color: red;
}

.blue {
  background-color: blue;
}

.green {
  background-color: green;
}
```

Think of the possibilities. You can use this to generate a set of classes with different font sizes, colors, etc.

Are you ever going back to CSS again ?

## Bonus

Here is a complex SASS code that I wrote.

```scss
$breakpoints: (
  small: 576px,
  medium: 768px,
  large: 992px,
  xlarge: 1200px,
);

$columns: 12;
$column-spacing: 20px;
$container-width: 1000px;

@each $breakpoint, $width in $breakpoints {
  @media (min-width: $width) {
    .container {
      max-width: $container-width;
      margin: 0 auto;
    }

    @for $i from 1 through $columns {
      .col-#{$i} {
        width: (100% / $columns) * $i - $column-spacing;
        margin-right: $column-spacing;
      }

      &:last-child {
        margin-right: 0;
      }
    }
  }
}
```

This will generate a CSS code that is about 360 lines long. Use the basic concepts that you learned in this guide to understand it. It is easy.

SASS is one of the tools that you will surely need in your web development journey. It is a must learn.
