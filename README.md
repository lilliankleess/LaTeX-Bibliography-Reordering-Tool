# LaTeX Bibliography Reordering Tool

## Overview
This tool automates the reordering of `\bibitem` entries in a LaTeX `.tex` file based on a specific order provided in an Excel file. It is designed to streamline bibliography organization for LaTeX documents, making it especially useful for researchers and academic writers.

---

## Features

1. Interactive File Uploads
   - Uses `ipywidgets` to enable interactive uploading of an Excel file (`.xlsx`) and a LaTeX file (`.tex`).

2. Bibliography Entry Extraction
   - Extracts all `\bibitem` entries from the LaTeX file using regular expressions.
   - Captures the label from each `\bibitem{label}` for reordering purposes.

3. Excel-Based Reordering
   - Reads the Excel file to extract the desired order of `\bibitem` labels from a specific column.
   - Reorders the LaTeX bibliography entries based on this order.

4. Output File Generation
   - Saves the reordered bibliography as a new LaTeX file (`<original_filename>_reordered.tex`) in the same directory.

5. Error Handling
   - Includes robust error handling to:
     - Verify the presence of both files.
     - Ensure the Excel file has the required structure.
     - Handle encoding issues in the LaTeX file.
     - Provide meaningful error messages.

---

## Workflow

1. Upload Files
   - Upload an Excel file (`.xlsx`) containing the order list and a LaTeX file (`.tex`) with `\bibitem` entries via the provided widgets.

2. Processing
   - The Excel file is processed to extract the order list from the desired column.
   - The LaTeX file is parsed to identify and extract all `\bibitem` entries.
   - The extracted entries are reordered based on the order provided in the Excel file.

3. Output
   - The reordered `\bibitem` entries are saved into a new LaTeX file.

---

## Functions

### `extract_bibitems(tex_content)`
Parses LaTeX content to extract all `\bibitem` entries and maps them to their respective labels.

- Args:
  - `tex_content (str)`: Content of the `.tex` file.

- Returns:
  - `dict`: A dictionary where keys are labels and values are corresponding `\bibitem` entries.

### `reorder_bibitems(bibitems, order_list)`
Reorders the extracted `\bibitem` entries based on the order provided in the Excel file.

- Args:
  - `bibitems (dict)`: Dictionary of extracted `\bibitem` entries.
  - `order_list (list)`: List of labels in the desired order.

- Returns:
  - `str`: Reordered LaTeX content.

### `save_to_tex(reordered_content, output_path)`
Saves the reordered LaTeX bibliography to a new `.tex` file.

- Args:
  - `reordered_content (str)`: Reordered LaTeX content.
  - `output_path (str)`: Path for the new `.tex` file.

### `process_files(excel_file, tex_file)`
Handles the end-to-end processing of the Excel and LaTeX files.

- Steps:
  1. Loads the Excel file to extract the order list.
  2. Extracts `\bibitem` entries from the LaTeX file.
  3. Reorders the entries based on the order list.
  4. Saves the reordered entries to a new LaTeX file.

- Args:
  - `excel_file (dict)`: The uploaded Excel file.
  - `tex_file (dict)`: The uploaded LaTeX file.

### `handle_upload(change)`
Handles the upload event when files are selected via widgets. Triggers the `process_files` function once both files are uploaded.

---

## Installation and Usage

1. Environment Setup:
   - Ensure Python is installed with the following libraries:
     - `pandas`
     - `ipywidgets`
     - `openpyxl`

2. Run the Code:
   - Open a Jupyter Notebook and execute the script.
   - Upload the required Excel and LaTeX files using the provided widgets.

3. Output:
   - The reordered LaTeX bibliography will be saved as `<original_filename>_reordered.tex`.

---

## File Structure

- Excel File:
  - Should have at least two columns. The second column (index 1) should contain the desired order of `\bibitem` labels (e.g., `authorlastnameyear`).

- LaTeX File:
  - Should contain `\bibitem` entries with labels in the format `\bibitem{label}`.

---

## Example

1. Input Files:
   - Excel: Contains the following:
     | Index | AuthorLastNameYear |
     |-------|--------------------|
     | 1     | Doe2021            |
     | 2     | Smith2020          |
   
   - LaTeX:
     ```latex
     \bibitem{Smith2020} Some bibliography entry.
     \bibitem{Doe2021} Another bibliography entry.
     ```

2. Output File:
   - Reordered LaTeX file:
     ```latex
     \bibitem{Doe2021} Another bibliography entry.

     \bibitem{Smith2020} Some bibliography entry.
     ```

---

## Error Handling

- File Upload Errors:
  - Prompts the user to upload both an Excel and a LaTeX file if either is missing.

- Excel Structure Validation:
  - Checks that the Excel file has at least two columns and provides an error message if not.

- Encoding Issues:
  - Handles encoding errors in the LaTeX file by replacing invalid characters.

---

## Benefits

- Automation: Saves time and effort by automating the reordering of `\bibitem` entries.
- Accuracy: Ensures correct and consistent ordering based on the Excel file.
- User-Friendly: Provides an interactive interface with clear error messages.

---


## Limitations

- Assumes that the Excel file contains the correct labels matching the LaTeX `\bibitem` entries.
- Works only with `.xlsx` and `.tex` file formats.

---

## Future Enhancements

- Add support for more customizable column selection in the Excel file.
- Improve compatibility with alternative bibliography styles.
- Provide a graphical user interface (GUI) for non-technical users.

