
<!---

This README is automatically generated from the comments in these files:
marked-element.html

Edit those files, and our readme bot will duplicate them over here!
Edit this file, and the bot will squash your changes :)

The bot does some handling of markdown. Please file a bug if it does the wrong
thing! https://github.com/PolymerLabs/tedium/issues

-->

[![Build status](https://travis-ci.org/PolymerElements/marked-element.svg?branch=master)](https://travis-ci.org/PolymerElements/marked-element)


## &lt;marked-element&gt;

Element wrapper for the [marked](https://github.com/chjj/marked) library.

`<marked-element>` accepts Markdown source, and renders it to a child
element with the slot `markdown-html`. This child element can be styled
as you would a normal DOM element. If you do not provide a child element
with the `markdown-html` slot, the Markdown source will still be rendered,
but to a shadow DOM child that cannot be styled.

The Markdown source can be specified several ways:

### Use the `markdown` attribute to bind markdown

```html
<marked-element markdown="`Markdown` is _awesome_!">
  <div slot="markdown-html"></div>
</marked-element>
```

### Use `<script type="text/markdown">` element child to inline markdown

```html
<marked-element>
  <div slot="markdown-html"></div>
  <script type="text/markdown">
    Check out my markdown!

    We can even embed elements without fear of the HTML parser mucking up their
    textual representation:

    ```html
    <awesome-sauce>
      <div>Oops, I'm about to forget to close this div.
    </awesome-sauce>
    ```
  </script>
</marked-element>
```

### Use `<script type="text/markdown" src="URL">` element child to specify remote markdown

```html
<marked-element>
  <div slot="markdown-html"></div>
  <script type="text/markdown" src="../guidelines.md"></script>
</marked-element>
```

Note that the `<script type="text/markdown">` approach is *static*. Changes to
the script content will *not* update the rendered markdown!

Though, you can data bind to the `src` attribute to change the markdown.

```html
<marked-element>
  <div slot="markdown-html"></div>
  <script type="text/markdown" src$="[[source]]"></script>
</marked-element>
...
<script>
  ...
  this.source = '../guidelines.md';
</script>
```

### Styling

If you are using a child with the `markdown-html` slot, you can style it
as you would a regular DOM element:

```css
[slot="markdown-html"] p {
  color: red;
}

[slot="markdown-html"] td:first-child {
  padding-left: 24px;
}
```

### Syntax Highlighting
Provides an opportunity to implement syntax highlighting, [e.g with highlightjs](https://highlightjs.org/).
An example handler can have this implementation : 
```
<marked-element id="syntaxHighlight" on-syntax-highlight="_highlightSyntax">
  ...
</marked-element>
```

```
_highlightSyntax(e, detail) {
   detail.code = hljs.highlightAuto(detail.code).value;
   return e;
 }
```
If using highlightjs, ensure the javascript library is loaded. You might also
need to inline the highlightjs CSS style you intend to use, or load it from a file
you can edit, so that you can prefix the rules to style content inside the marked-element's shadow DOM
E.g this rule in the highlightjs defeult CSS style file : 
```
.pl-c {
  color: #969896;
} 
```
becomes :
``` 
[slot="markdown-html"] .pl-c {
  color: #969896;
} 
```