# Blog Authoring Guide

This guide explains how to run the blog locally, create a category, publish an
article under that category, and use the most common Markdown formatting.

## Run the blog locally

This blog is built with [Jekyll](https://jekyllrb.com/) and GitHub Pages. The
Jekyll project is inside the `docs` directory.

### Prerequisites

Install the following software before running the blog:

- Ruby
- Bundler (`gem install bundler`)

### Install dependencies

From the repository root, run:

```shell
cd docs
bundle install
```

You normally need to run `bundle install` only after cloning the repository or
when `Gemfile` changes.

### Start the local server

From the `docs` directory, run:

```shell
bundle exec jekyll serve
```

Alternatively, run the supplied script from the repository root:

```shell
cd docs
sh run.sh
```

Open <http://127.0.0.1:4000> in a browser. Jekyll automatically rebuilds the
site when most files change. If you edit `_config.yml`, stop the server with
`Ctrl+C` and start it again.

## Create a category

Category pages live directly inside `docs` and use the `category` layout. To
create an `Aeron` category, add `docs/aeron.md` with this front matter:

```yaml
---
layout: category
title: Aeron
cat: aeron
permalink: /aeron/
---
```

The values have these purposes:

- `layout` selects the category page template.
- `title` is the heading shown on the page.
- `cat` identifies which articles belong to the category.
- `permalink` defines the category page's URL.

To show the category in the site's header, add its filename to `header_pages`
in `docs/_config.yml`:

```yaml
header_pages:
  - performance-engineering.md
  - scratch.md
  - aeron.md
```

Restart the local Jekyll server after changing `_config.yml`.

## Create an article under a category

Articles belong in `docs/_posts`. Name each file using this pattern:

```text
YYYY-MM-DD-article-name.markdown
```

For example:

```text
docs/_posts/2026-10-10-getting-started-with-aeron.markdown
```

Start the file with Jekyll front matter, followed by the article content:

```markdown
---
layout: post
title: "Getting Started with Aeron"
date: 2026-10-10 10:00:00 +0800
categories: aeron
author: Isuru
---

Write the article introduction here.

## First topic

Add the article content here.
```

The value of `categories` must match the `cat` value in the category page. In
this example, both values are `aeron`, so the article appears on `/aeron/`.

An article can belong to multiple categories by separating them with spaces:

```yaml
categories: aeron performance-engineering
```

Before publishing, run the blog locally and check both the article and its
category page. Commit and push the new files when they are ready.

## Markdown cheat sheet

### Headings

```markdown
# Heading 1
## Heading 2
### Heading 3
```

Use a single `#` for the main title and add more `#` characters for nested
sections.

### Emphasis

```markdown
**bold text**
*italic text*
~~strikethrough text~~
```

### Links and images

```markdown
[Link text](https://example.com)
![Image description](/assets/images/example.png)
```

Store blog images under a suitable directory inside `docs/assets` so Jekyll
can include them in the generated site.

### Lists

```markdown
- First item
- Second item
  - Nested item

1. First step
2. Second step
3. Third step
```

### Blockquotes

```markdown
> This is a blockquote.
>
> It can contain multiple paragraphs.
```

### Inline code and code blocks

Use backticks for `inline code`:

```markdown
Run `bundle install` to install the dependencies.
```

Use three backticks and a language name for a fenced code block:

````markdown
```java
public class Hello {
    public static void main(String[] args) {
        System.out.println("Hello");
    }
}
```
````

### Tables

```markdown
| Column A | Column B |
|----------|----------|
| Value 1  | Value 2  |
| Value 3  | Value 4  |
```

### Horizontal rules

```markdown
---
```

Leave a blank line before and after the rule. Avoid placing it immediately at
the start of a Jekyll file, where `---` is used for front matter.

### Task lists

```markdown
- [x] Completed item
- [ ] Incomplete item
```

### Escaping Markdown characters

Add a backslash before a formatting character when you want to display it
literally:

```markdown
\*This text is not italic.\*
```
