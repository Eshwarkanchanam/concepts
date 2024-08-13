## Box model

The Box Model in CSS is a concept that describes how elements on a webpage are structured. It consists of four parts:

- **Content**: The actual content of the element (text, images, etc.).
- **Padding**: Space between the content and the border.
- **Border**: The line surrounding the padding and content.
- **Margin**: Space outside the border, separating the element from others.

This model determines the total width and height of an element on a page.

## Inline versus Block Elements. Examples.

**Inline Elements**:

- Do not start on a new line and only take up as much width as needed.
- Examples: ```<span>, <a>, <img>```

**Block Elements**:

- Start on a new line and take up the full width available.
  Examples: ```<div>, <p>, <h1>```

## Positioning: Relative/Absolute

**Relative Positioning:**

- Element is positioned relative to its normal position.
- Offset by top, right, bottom, or left values but still occupies its original space.

**Absolute Positioning:**

- Element is positioned relative to its nearest positioned ancestor or the initial containing block if none exists.
- Removed from the normal document flow, so it doesn't affect the position of other elements.

## Common CSS structural classes

Common CSS structural classes include:

- **Container**: Centers and constrains content width (e.g., .container).
- **Row**: Defines a row for layout, often used in grid systems (e.g., .row).
- **Column**: Divides a row into columns, often with a responsive layout (e.g., .col-md-6).

## Common CSS syling classes

Common CSS styling classes include:

- **Text Alignment:** Aligns text (e.g., .text-center, .text-right).
- **Background:** Adds background color or images (e.g., .bg-primary, .bg-light).
- **Font Style:** Adjusts font appearance (e.g., .font-weight-bold, .italic).
- **Visibility:** Controls element visibility (e.g., .d-none, .visible).
- **Borders:** Adds or styles borders (e.g., .border, .rounded).

## CSS Specificity

CSS Specificity determines which CSS rule is applied when multiple rules target the same element. It's calculated based on the types of selectors used:

- **Inline Styles**: Highest specificity (e.g., style="...").
- **IDs:** High specificity (e.g., #header).
- **Classes, Attributes, Pseudo-classes:** Moderate specificity (e.g., .btn, [type="text"], :hover).
- **Elements, Pseudo-elements:** Low specificity (e.g., div, h1, ::before).

## CSS Responsive Queries

CSS Responsive Queries (Media Queries) allow you to apply styles based on the device's screen size or other characteristics. They help create responsive designs that adapt to different devices.

```
@media (max-width: 768px) {
  .container {
    width: 100%;
  }
}
```

In this example, the .container class will take up 100% width on screens that are 768px wide or less.

## Flexbox/Grid

**Flexbox:**

- Used for 1D layouts (row or column).
- Aligns and distributes space among items in a container.
- Example: Aligning items horizontally or vertically in a navbar.

**Grid:**

- Used for 2D layouts (rows and columns).
- Creates complex, responsive layouts by dividing the page into regions.
- Example: Designing a webpage layout with header, sidebar, and content areas.

Both are powerful CSS layout tools but are suited for different types of layouts.

## Common header meta tags

Common header meta tags include:

- **Charset:** Defines the character encoding (e.g., <meta charset="UTF-8">).
- **Viewport:** Controls the page's dimensions and scaling on mobile devices (e.g., <meta name="viewport" content="width=device-width, initial-scale=1">).
- **Description:** Provides a brief description of the page for search engines (e.g., <meta name="description" content="A brief description of the page.">).
- **Keywords:** Specifies keywords related to the page's content (less used now) (e.g., <meta name="keywords" content="HTML, CSS, Web Development">).
- **Author:** Indicates the author of the page (e.g., <meta name="author" content="Your Name">).

## different types of encoding

Here are the differences between common text encodings:

- **UTF-8:**
- **Description:** A variable-width encoding that can represent every character in the Unicode character set.
- **Usage:** Widely used on the web; supports most languages and symbols.

- **ISO-8859-1 (Latin-1):**
- **Description:** A single-byte encoding for Western European languages.
- **Usage:** Limited to a specific set of characters; less versatile than UTF-8.

- **ASCII:**
- **Description:** A 7-bit encoding representing English characters and basic symbols.
- **Usage:** Very limited; only supports basic English characters and control codes.

- **UTF-16**:
- **Description:** A variable-width encoding using one or two 16-bit code units to represent characters.
- **Usage:** Often used in programming environments and for internal data storage.

- **UTF-32:**
- **Description:** A fixed-width encoding using 32 bits per character.
- **Usage:** Simple to use but inefficient in terms of storage; rarely used for web content.

Each encoding has different applications based on character support, efficiency, and compatibility.
