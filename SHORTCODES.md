# Custom Hugo Shortcodes

This document describes the custom shortcodes available in this project.

## Layout & Column Shortcodes

Create multi-column layouts with full alignment control.

### Basic Usage

**2-column layout (default):**
```markdown
{{< layout >}}
  {{< column >}}
    {{< figure src="/images/pic1.jpg" alt="First image" >}}
    Some text for the first column
  {{< /column >}}

  {{< column >}}
    {{< figure src="/images/pic2.jpg" alt="Second image" >}}
    Some other text for the second column
  {{< /column >}}
{{< /layout >}}
```

**3-column layout:**
```markdown
{{< layout cols="3" >}}
  {{< column >}}
    Content for column 1
  {{< /column >}}
  {{< column >}}
    Content for column 2
  {{< /column >}}
  {{< column >}}
    Content for column 3
  {{< /column >}}
{{< /layout >}}
```

### Layout Parameters

The `layout` shortcode accepts the following parameters:

| Parameter | Default | Description |
|-----------|---------|-------------|
| `cols` | `2` | Number of columns in the layout |
| `gap` | `2rem` | Space between columns |
| `caption` | `""` | Caption text displayed below the layout |
| `caption-position` | `center` | Caption text alignment: `left`, `center`, or `right` |
| `caption-class` | `""` | CSS class for the caption |
| `class` | `""` | Additional CSS classes |
| `style` | `""` | Inline CSS styles |

**Example:**
```markdown
{{< layout cols="4" gap="1rem" class="my-custom-class" caption="Figure 1: Comparison of different approaches" >}}
  <!-- columns here -->
{{< /layout >}}
```

### Column Parameters

The `column` shortcode accepts the following parameters:

| Parameter | Default | Options | Description |
|-----------|---------|---------|-------------|
| `align` | `left` | `left`, `center`, `right` | Horizontal alignment of content |
| `valign` | `top` | `top`, `center`, `bottom`, `stretch` | Vertical alignment of content |
| `class` | `""` | Any string | Additional CSS classes |
| `style` | `""` | Any CSS | Inline CSS styles |

**Example:**
```markdown
{{< column align="center" valign="center" >}}
  This content is centered both horizontally and vertically
{{< /column >}}
```

### Advanced Examples

**Mixed alignments:**
```markdown
{{< layout cols="3" >}}
  {{< column align="left" valign="top" >}}
    Top-left aligned content
  {{< /column >}}

  {{< column align="center" valign="center" >}}
    Centered content
  {{< /column >}}

  {{< column align="right" valign="bottom" >}}
    Bottom-right aligned content
  {{< /column >}}
{{< /layout >}}
```

**Custom styling:**
```markdown
{{< layout cols="2" gap="3rem" style="padding: 2rem; background: #f5f5f5;" >}}
  {{< column align="center" style="border: 1px solid #ddd; padding: 1rem;" >}}
    Content with custom border and padding
  {{< /column >}}

  {{< column align="center" >}}
    Regular column
  {{< /column >}}
{{< /layout >}}
```

**With caption (centered by default):**
```markdown
{{< layout cols="2" caption="Figure 1: Comparison between approach A and approach B" >}}
  {{< column align="center" >}}
    {{< figure src="/images/approach-a.jpg" alt="Approach A" >}}
    **Approach A**: Traditional method
  {{< /column >}}

  {{< column align="center" >}}
    {{< figure src="/images/approach-b.jpg" alt="Approach B" >}}
    **Approach B**: Modern method
  {{< /column >}}
{{< /layout >}}
```

**Caption with different alignments:**
```markdown
{{< layout cols="2" caption="Left-aligned caption" caption-position="left" >}}
  <!-- content -->
{{< /layout >}}

{{< layout cols="2" caption="Right-aligned caption" caption-position="right" >}}
  <!-- content -->
{{< /layout >}}
```

## Figure Shortcode

Display images with captions and custom styling.

```markdown
{{< figure src="/images/example.jpg"
           alt="Example image"
           caption="This is a caption"
           position="center" >}}
```

### Figure Parameters

| Parameter | Description |
|-----------|-------------|
| `src` | Image source URL |
| `alt` | Alt text for the image |
| `caption` | Caption text displayed below the image |
| `position` | Position class for the figure |
| `figure-class` | CSS class for the figure element |
| `figure-style` | Inline CSS for the figure element |
| `img-class` | CSS class for the img element |
| `style` | Inline CSS for the img element |
| `caption-class` | CSS class for the caption |

---

*Last updated: 2025-12-29*
