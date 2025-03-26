# Task 1: Format JSON Data with Locale-Aware Dates

## Overview

This script processes a JSON array of articles and displays them in a human-readable format, with dates formatted according to the **user's browser locale and timezone**. The solution avoids forcing UTC or a specific locale, ensuring dates align with the user's local settings.

## Approach

1. **Date Parsing**

   - The `creation_date` (e.g., `"2021-09-13"`) is split into `year`, `month`, and `day` components.
   - A `Date` object is created in the user's local timezone using `new Date(year, month - 1, day)`.
   - **Why?** Parsing dates directly from ISO strings (e.g., `new Date("2021-09-13")`) would interpret them as UTC, potentially causing timezone shifts. By splitting the string, we ensure the date is treated as local.

2. **Date Formatting**

   - `Intl.DateTimeFormat` uses the browser's default locale and timezone when no arguments are specified.
   - Formatting options (`year: 'numeric', month: 'long', day: 'numeric'`) produce a readable string like `September 13, 2021` (en-US) or `13. September 2021` (de-DE).

3. **Dynamic Output**
   - Results are joined with `<br>` tags to ensure proper line breaks in HTML.

## How to Use

1. Open `index.html` in a web browser.
2. The formatted results will appear under "Results of my code".

## Example Outputs

- **en-US (Chrome):**  
  `Article "André Baniwa" (Page ID 6682420) was created at September 13, 2021.`
- **pt-BR (Chrome):**  
  `Article "André Baniwa" (Page ID 6682420) was created at 13 de setembro de 2021.`
- **de-DE (Firefox):**  
  `Article "André Baniwa" (Page ID 6682420) was created at 13. September 2021.`

## Browser Compatibility

- Uses `Intl.DateTimeFormat`, which is supported in all modern browsers (Chrome, Firefox, Safari, Edge).
- Not tested on Internet Explorer.
