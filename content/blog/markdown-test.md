---
title: "Markdown formatting test"
date: 2026-05-25
designation: "TEST-001"
---

## Headings

### Third level heading

#### Fourth level heading

## Paragraphs and inline formatting

This is a regular paragraph. It contains **bold text**, *italic text*, ***bold italic text***, and `inline code`. Here is a [link to something](https://example.org) in the middle of a sentence.

This is a second paragraph to show spacing between paragraphs. It has ~~strikethrough text~~ and also a longer passage to show how body text wraps across multiple lines when the viewport is narrow enough to force it.

## Unordered list

- First item
- Second item with **bold** inside it
- Third item with a [link](https://example.org)
- Fourth item

## Ordered list

1. First step
2. Second step
3. Third step with `code` in it
4. Fourth step

## Nested lists

- Outer item one
  - Inner item A
  - Inner item B
- Outer item two
  - Inner item C

## Blockquote

> This is a blockquote. It might contain a longer passage that wraps across
> multiple lines. Often used for quoting someone else or calling out a key
> statement.

> Multi-paragraph blockquote first paragraph.
>
> Second paragraph inside the same blockquote.

## Code block

```c
#include <stdio.h>

int main(void) {
    printf("Hello, world.\n");
    return 0;
}
```

## Table

| Component | Voltage | Status |
|-----------|---------|--------|
| Servo X   | 24V     | Active |
| Servo Y   | 24V     | Active |
| Spindle   | 380V    | Idle   |
| Coolant   | 12V     | Off    |

## Horizontal rule

Content above the rule.

---

Content below the rule.

## Image

{{< img src="hmi-panel-old.png" alt="Test image for layout reference" >}}

## Footnotes

This sentence has a footnote[^1]. And here is another[^2].

[^1]: This is the first footnote content.
[^2]: This is the second footnote content with a [link](https://example.org).

## Definition-style content

**Term one**
: Definition of term one. This is a longer definition to show how wrapping behaves.

**Term two**
: Definition of term two.

## Mixed content

Here is a paragraph leading into a list:

- Item with a `code snippet` and then a blockquote after the list

> A blockquote immediately following a list.

And then back to a paragraph with **bold**, *italic*, and a [final link](https://example.org).
