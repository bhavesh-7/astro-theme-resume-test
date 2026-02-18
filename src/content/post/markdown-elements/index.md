---
title: "Understanding Markdown: A Complete Guide"
description: "Learn how to write and format content using Markdown - the simple markup language for creating formatted text"
publishDate: "18 Feb 2026"
updatedDate: 18 Feb 2026
tags: ["markdown", "writing", "documentation", "guide"]
---

## What is Markdown?

Markdown is a lightweight markup language that allows you to write formatted text using plain text syntax. It's widely used for documentation, README files, blog posts, and more.

## Headings

Create headings using `#` symbols:

## This is a H2 Heading

### This is a H3 Heading

#### This is a H4 Heading

##### This is a H5 Heading

###### This is a H6 Heading

## Horizontal Rules

Separate content with horizontal lines using `---`:

---

---

---

## Text Emphasis

**This is bold text** using `**text**` or `__text__`

_This is italic text_ using `*text*` or `_text_`

~~Strikethrough~~ using `~~text~~`

## Quotes

"Double quotes" and 'single quotes' are just regular text.

## Blockquotes

Use `>` for blockquotes:

> Blockquotes can also be nested...
>
> > ...by using additional greater-than signs right next to each other...

## Footnotes and References

An example containing a clickable reference[^1] with a link to the source.

Second example containing a reference[^2] with a link to the source.

[^1]: Reference first footnote with a return to content link.
[^2]: Second reference with a link.

Footnotes are automatically added to the bottom of the page.

## Lists

### Unordered Lists

Create unordered lists with `-`, `*`, or `+`:

- Create a list by starting a line with `+`, `-`, or `*`
- Sub-lists are made by indenting 2 spaces:
  - Marker character change forces new list start:
    - Ac tristique libero volutpat at
    - Facilisis in pretium nisl aliquet
    - Nulla volutpat aliquam velit
- Very easy!

### Ordered Lists

1. Lorem ipsum dolor sit amet
2. Consectetur adipiscing elit
3. Integer molestie lorem at massa

4. You can use sequential numbers...
5. ...or keep all the numbers as `1.`

Start numbering with offset:

57. foo
1. bar

## Code

### Inline Code

Use backticks for inline `code` like this: \`code\`

### Indented Code Blocks

Indent with 4 spaces or a tab:

    // Some comments
    line 1 of code
    line 2 of code
    line 3 of code

### Fenced Code Blocks

Use triple backticks:

```
Sample text here...
```

### Syntax Highlighting

Specify the language after the opening backticks:

```js
var foo = function (bar) {
	return bar++;
};

console.log(foo(5));
```

## Advanced Code Features

### Adding Titles

```js title="file.js"
console.log("Title example");
```

### Terminal Examples

```bash
echo "A bash terminal example"
```

### Highlighting Lines

```js title="line-markers.js" del={2} ins={3-4} {6}
function demo() {
	console.log("this line is marked as deleted");
	// This line and the next one are marked as inserted
	console.log("this is the second inserted line");

	return "this line uses the neutral default marker type";
}
```

This uses [Expressive Code](https://expressive-code.com/) for enhanced code blocks with features like line highlighting, titles, and more.

## Tables

Create tables using pipes `|` and hyphens `-`:

| Option | Description                                                               |
| ------ | ------------------------------------------------------------------------- |
| data   | path to data files to supply the data that will be passed into templates. |
| engine | engine to be used for processing templates. Handlebars is the default.    |
| ext    | extension to be used for dest files.                                      |

### Right Aligned Columns

Use colons to align columns:

| Option |                                                               Description |
| -----: | ------------------------------------------------------------------------: |
|   data | path to data files to supply the data that will be passed into templates. |
| engine |    engine to be used for processing templates. Handlebars is the default. |
|    ext |                                      extension to be used for dest files. |

## Images

Reference images in the same folder:

![Astro theme cactus logo](logo.png)

Syntax: `![Alt text](image-path.png)`

## Links

Create links using `[text](url)`:

[Markdown Guide](https://www.markdownguide.org/)

## Best Practices

1. **Keep it simple** - Markdown is meant to be readable as plain text
2. **Use consistent formatting** - Stick to one style for lists, emphasis, etc.
3. **Preview your work** - Always check how your markdown renders
4. **Learn your editor** - Most editors have markdown preview features
5. **Use code blocks** - Properly format code with syntax highlighting

## Common Use Cases

- **Documentation** - README files, wikis, technical docs
- **Blogging** - Static site generators like Astro, Jekyll, Hugo
- **Note-taking** - Obsidian, Notion, Bear
- **Communication** - GitHub issues, Discord, Slack
- **Writing** - Books, articles, reports

## Conclusion

Markdown is a powerful yet simple way to format text. Once you learn the basics, you can write formatted content quickly without taking your hands off the keyboard. It's become the standard for technical writing and is supported almost everywhere.

Start practicing with these examples and you'll be a Markdown pro in no time!

## Learn More

- [Markdown Guide](https://www.markdownguide.org/)
- [CommonMark Spec](https://commonmark.org/)
- [GitHub Flavored Markdown](https://github.github.com/gfm/)
- [Expressive Code Documentation](https://expressive-code.com/)
