# HolyGrail
Fixing The HolyGrail Problem Using FlexBox Layout CSS3

# The Problem 

Many web pages require a layout with multiple (often three) columns, with the main page content in one column (often the center), and supplementary content such as menus and advertisements in the other columns (sidebars). These columns commonly require separate backgrounds, with borders between them, and should appear to be the same height no matter which column has the tallest content. A common requirement is that the sidebars have a fixed width, with the center column adjusting in size to fill the window (fluid or liquid layout). Another common requirement is that, when a page does not contain enough content to fill the screen, the footer should drop to the bottom of the browser window instead of leaving blank space underneath.

CSS, although quite useful for styling, currently has limited capabilities for page layout.
The height of block elements (such as div elements) is normally determined by their content. So two divisions, side by side, with different amounts of content, will have different heights unless their height is somehow set to an appropriate value.
HTML is meant to be used semantically; HTML elements should be chosen which accurately describe their content. The appearance of a web page as rendered by a user agent should be determined independently by style rules. Many implementations misuse HTML by using tables for non-tabular data, or nesting multiple div elements without semantic purpose. Non-semantic use of HTML confuses users or user agents who are trying to discern the structure of the page content, and is an accessibility issue .
As search engines consider content in the beginning of a web page's source code to be more relevant, web designers desire the ability to place the content in the page source in an arbitrary order, without affecting the appearance of the page.
Because of incorrect rendering of content by different browsers, a method that works in a standards-compliant browser may not work in one that does not implement CSS correctly.

# Known workarounds

###### Tables : 
Before the widespread implementation of CSS, designers commonly used tables to lay out pages. Sometimes they achieved their desired layout by nesting several tables inside each other. Although placing the columns inside table cells easily achieves the desired visual appearance, using a table is semantically incorrect, although the "role" WAI-ARIA HTML attribute can be set to "presentation" to regain semantic context. There is also no way to control the order of the columns in the page source.

###### Divisions with display:table
It is possible to make columns equal height using the CSS display property. This requires nested container divisions that are set to display: table and display: table-row, and columns that are set to display: table-cell. This is semantically correct, as only the display is affected. However, this method lacks the ability to control the order of the source code. It will also not work with some older, unsupported browsers, such as Internet Explorer 7.

###### Faux columns
This method uses a background image which provides the background colors and vertical borders of all three columns.The content of each column is enclosed in a division, and positioned over its background using techniques such as floats, negative margins, and relative positioning. The background is normally only a few pixels high, and is made to cover the page using the "repeat-y" attribute. This works fine for fixed-width layouts, and can be adapted for percentage-based variable-width pages, but cannot be used for fluid center pages.

###### JavaScript
In this method, after the page is loaded, a script measures the height of each of the columns, and sets the height of each column to the greater value. This will not work in browsers that do not support JavaScript, or have JavaScript disabled.

###### Fixed or absolute positioning
In this method, the corners of the column divisions are locked in a specific place on the page. This may be acceptable or even desired, but does not solve the holy grail problem as it is a significantly different layout. The consequences of this method may include having content appearing below the columns (such as a footer) fixed at the screen bottom, blank space under the column content, and requiring scrollbars for each column to view all the content.

###### Nested divisions
A division with its background will grow in height to contain its content. This behavior is used to solve the problem by creating three divisions nested inside each other which provide the three backgrounds. These divisions are placed in their proper location using positioning techniques, and the three content divisions are placed inside the innermost background division, positioned over their respective backgrounds. The background divisions then become as tall as the tallest content division. The drawbacks of this method include the three non-semantic divisions, and the difficulty of positioning the elements of this complex layout.

###### Border color
A simpler version of the nested division method entails using a single container division. The background properties of this division provides the background of the center column, and the left and right borders, which are given widths equal to the side column widths, provide the background colors of the sidebars. The content of each column is positioned over its background. This method still uses one non-semantic division, and makes it difficult to apply background images and borders to the sidebars.

###### Bottom padding
By placing a large amount of padding at the bottom of the column container, the background will extend far below the column content. A corresponding negative margin will bring content below the columns back into its proper position. Positioning is simple in this method, as the container of a column's content also contains its background. A padding value of 32767px is the largest that will be recognized by all modern browsers. If the difference in column heights is greater than this, the background of the shorter column will not fully fill the column.

# Current solution

###### CSS3 Flexible Box Layout (Flexbox)

The World Wide Web Consortium (W3C) has approached the layout issue through various proposals. The most mature proposal is the Flexible Box Module (A.K.A. Flexbox), which is in Candidate Recommendation status as of October 2017 . Setting an element's display property to "flex" or "inline-flex" causes the element to become a new type of container (similar to a block or inline block, respectively), with new methods of positioning child objects. Content can flow in any direction, and be displayed in any order. The W3C proposal contains an example which achieves the holy grail column layout using four simple CSS rules, and makes the layout responsive with a simple media query rule. The module can also be used to address many other layout issues.

The Flexible Box Module is supported in all of the modern browsers. Older browsers still have issues, but most of those (mainly Internet Explorer 9 and below) are no longer supported by their vendors. Many designers will choose to provide compatible styling for older browsers, to be overridden in modern browsers by the new syntax. In spite of the continued existence of legacy browsers, this module is currently touted as a solution to the holy grail issue.

References : https://en.wikipedia.org 

