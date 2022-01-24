---
layout: guides
navbar: Guides
title: Comparing Files in Eclipse
key: 4

#tags:
#  - text: 'New'
#    type: 'is-primary'
---

For homework and projects, it may be useful to compare actual and expected output files side-by-side. Eclipse has a nice comparison view that will align the files and highlight the differences, even differences in whitespaces that may be otherwise difficult to see.

## Opening Compare View

![Compare With]({{ "/images/comparewith.gif" | relative_url }}){: .is-800 }

To open this view, follow these steps:

  1. <kbd>Control + Click</kbd> or <kbd>Command + Click</kbd> the two files you want to compare so that they are both highlighted in the Project Explorer view.

  2. Right-click one of the selected files. This should open up a menu.

  3. Select "Compare With" from the menu.

  4. Select "Each Other" from the sub-menu.

## Comparison View

![Compare With]({{ "/images/compareview.png" | relative_url }}){: .is-600 }

The two files will be displayed side-by-side. If it is a long file, Eclipse will synchronize scrolling of the files.

Any differences between the two files will be highlighted. This is especially helpful to find difference in whitespaces.

You can also use the buttons on the top right to step through all of the differences in the file. This is useful for large files when it isn't clear where to find the differences.
