---
title: "Writing Your First Jekyll Post"
date: 2025-02-01 09:00:00 +0800
categories: [Tutorial, Jekyll]
tags: [jekyll, blogging, markdown, chirpy]
lang: en
---

Jekyll posts are written in **Markdown** and placed in the `_posts/` directory.
Every post filename must follow the format `YYYY-MM-DD-title.md`.

## Front Matter

Every post starts with YAML front matter between `---` delimiters:

```yaml
---
title: "Your Post Title"
date: 2025-02-01 09:00:00 +0800
categories: [Category, Subcategory]
tags: [tag1, tag2]
lang: en
---
```

Add `lang: en` for English posts or `lang: zh-CN` for Chinese posts —
this enables the language filter on the home page.

## Markdown Basics

### Headings

```markdown
# H1 heading
## H2 heading
### H3 heading
```

### Code Blocks

Syntax highlighting is built-in. Specify the language after the triple backticks:

```python
def greet(name: str) -> str:
    return f"Hello, {name}!"

print(greet("World"))
```

### Math Equations

Chirpy supports KaTeX for math. Inline: $E = mc^2$

Block:

$$
\sum_{n=1}^{\infty} \frac{1}{n^2} = \frac{\pi^2}{6}
$$

### Alerts / Prompts

Chirpy has built-in prompt styles:

> This is a **tip**.
{: .prompt-tip }

> This is an **info** note.
{: .prompt-info }

> This is a **warning**.
{: .prompt-warning }

> This is a **danger** alert.
{: .prompt-danger }

## Images

```markdown
![Alt text](/path/to/image.jpg)
_Caption text_
```

## Summary

That covers the basics! Now you're ready to start writing your own posts.
Check the [Chirpy documentation](https://chirpy.cotes.page) for more advanced features.
