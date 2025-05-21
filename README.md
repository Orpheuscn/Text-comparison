# Text Comparison and Editing Tool

This tool allows users to compare two pieces of text, highlighting the differences between them. It also supports manual highlighting of selected text portions and direct editing of the displayed texts.

## Features

- **Text Input**: Two text areas are provided for users to paste or type the texts they want to compare.
- **Comparison**: Clicking the "Comparer / Rafraîchir" button processes the two input texts. The differences are then displayed, with additions to the second text highlighted in green and deletions from the first text highlighted in red.
- **Display Modes**:
    - "Texte 2 uniquement": This option displays only the content of the second text input area, without any comparison highlights.
    - "Afficher les deux versions": This option displays both texts side-by-side in their current state, without any difference highlighting. This is useful for a clean view after editing.
- **Editing**:
    - "Éditer les textes affichés": Allows users to directly modify the content of the displayed text columns.
    - "Sauvegarder les modifications": After editing, this button saves the changes back to the original input text areas. The input fields are updated with the edited content.
- **Manual Highlighting**: Users can select any portion of text within either of the displayed text columns. A small popup menu will appear, allowing them to:
    - "Surligner": Apply a highlight to the selected text. Selections in the left column (Source 1) are highlighted in red (as if they were a deletion to be noted), and selections in the right column (Source 2) are highlighted in green (as if they were an addition to be noted).
    - "Annuler": Remove any existing manual highlight from the selected text portion.
- **Ruler**: A dynamic central ruler is displayed between the two text columns when in comparison mode on wider screens. It helps visually align corresponding paragraphs based on their height, making it easier to track differences across longer texts.
- **Responsive Design**: The layout adjusts for smaller screen sizes to ensure usability on various devices. For example, the text columns stack vertically on mobile, and the ruler is hidden.

## How to Use

1.  **Input Texts**: Paste the first text into the "Texte Source 1" text area and the second text into the "Texte Source 2" text area.
2.  **Compare**: Click the "Comparer / Rafraîchir" button. The two texts will be displayed side-by-side, with differences highlighted.
    *   Text added in Source 2 (compared to Source 1) will be green.
    *   Text removed from Source 1 (compared to Source 2) will be red and struck through.
3.  **View Options**:
    *   Click "Texte 2 uniquement" to see only the second text.
    *   Click "Afficher les deux versions" to see both texts without highlights.
4.  **Edit Texts**:
    *   Click "Éditer les textes affichés". The displayed texts become editable.
    *   Make your changes directly in the columns.
    *   Click "Sauvegarder les modifications" to update the input text areas with your changes. You can then compare the modified versions if needed.
5.  **Manual Highlighting**:
    *   In the comparison view, select any piece of text in either column.
    *   A popup will appear. Click "Surligner" to add a highlight (red for left column, green for right) or "Annuler" to remove an existing highlight.
    *   This is useful for drawing attention to specific parts of the text manually, independent of the automatic diff.
6.  **Ruler**: On wider screens, a central ruler automatically adjusts to help align paragraphs visually during comparison.

## Technologies Used

*   **HTML**: For the basic structure and layout of the web page.
*   **CSS**: For styling the elements, including the highlighting of differences and responsive design.
*   **JavaScript**: For all the client-side logic, including:
    *   Text processing and comparison.
    *   DOM manipulation to display differences and handle user interactions.
    *   Event handling for buttons and text selections.
    *   Manual highlighting functionality.
*   **diff-match-patch library**: A JavaScript library by Google (Neil Fraser) used for performing the text differencing algorithm. It's included via a CDN link.

## `index.html` File Structure Overview

The `index.html` file contains all the necessary code for the tool:

*   **CSS Styles**:
    *   Embedded within `<style>` tags in the `<head>`.
    *   Includes general page styling, input area layout, text column appearance, highlighting styles (for diffs and manual highlights), popup menu, and responsive media queries.
*   **HTML Layout**:
    *   Located within the `<body>`.
    *   `container`: Main wrapper for all content.
    *   `header`: Contains the main title.
    *   `input-area`: Holds the two `textarea` elements for text input.
    *   `controls`: Contains buttons for "Comparer / Rafraîchir", "Texte 2 uniquement", "Afficher les deux versions", "Éditer les textes affichés", and "Sauvegarder les modifications".
    *   `content`: The main area where the comparison results (or single text view) are dynamically rendered. This includes `textColumn1`, `rulerColumn`, and `textColumn2`.
    *   `legend`: Explains the meaning of the highlight colors.
    *   `notes`: Provides a hint about the manual selection feature.
    *   `highlight-popup`: The hidden popup menu for manual highlighting.
*   **JavaScript Logic**:
    *   Embedded within `<script>` tags at the end of the `<body>`.
    *   Global variables for state management (e.g., `source1Data`, `source2Data`, `isEditing`, `dmp` instance).
    *   Element references for quick DOM access.
    *   **Core Functions**:
        *   `setEditingState()`: Toggles the editing mode and button states.
        *   `findDifferences()`: Uses `diff_match_patch` to find differences between two text strings.
        *   `createRuler()`: Dynamically generates and updates the central ruler.
        *   `processTexts()`: Renders the basic structure for displaying two texts.
        *   `displayDifferences()`: Renders texts with diff highlights.
        *   `showOriginalOnly()`: Displays only the second text.
        *   `showBothVersions()`: Displays both texts without diff highlights.
    *   **Manual Highlighting Logic**:
        *   `showPopup()`, `hidePopup()`: Manage the visibility and position of the highlighting popup.
        *   Event listener on `textDisplayArea` for `mouseup` to trigger the popup on text selection.
        *   `findIntersectingHighlightSpans()`: Utility to find existing highlight spans within a selection.
        *   Event listeners for "Surligner" (`highlightBtn`) and "Annuler" (`removeHighlightBtn`) buttons in the popup to apply or remove `<span>` tags with appropriate classes.
    *   **Event Listeners**:
        *   Attached to buttons (`showDifferencesBtn`, `editTextsBtn`, `saveChangesBtn`, etc.) to trigger corresponding actions.
        *   Window `resize` listener to adjust the ruler.
    *   Initialization code (`DOMContentLoaded`) to set up the tool.

## Conclusion

This tool provides a straightforward way to compare and edit texts directly in the browser, with added flexibility for manual annotations.
