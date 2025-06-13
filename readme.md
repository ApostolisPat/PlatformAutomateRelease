# Platform Automate

Automate the management, upload, and metadata collection of Digital Learning Objects (DLOs) for the [ebooksdl.cti.gr](https://ebooksdl.cti.gr/) platform using Selenium and custom JavaScript scripts.

---

## Features

- **Automated DLO Management:** Upload, delete, and update DLOs and their metadata on the platform.
- **Metadata Collection & Export:** Collects metadata from the platform and exports to CSV for auditing and reporting.
- **Browser Support:** Works with Chrome, Edge, and Firefox via Selenium WebDriver.
- **JavaScript DOM Automation:** Uses custom JS scripts for UI automation (tab navigation, form filling, button clicks).
- **Progress Tracking:** Tracks upload and metadata update progress in JSON and Excel logs per lesson.
- **Robust Error Handling:** Handles missing files, platform changes, and UI exceptions gracefully.
- **Lesson-Specific Data:** Manages DLOs and logs per lesson folder for easy organization.
- **Dummy DLO Generation:** Supports creation of dummy DLOs for testing and validation.
- **Customizable Automation:** Easily extendable with new JS scripts for additional platform actions.

---

## Project Structure

```
PlatformAutomate/
├── build.bat
├── changelog.txt
├── platformAutomate.spec
├── readme.md
├── requirements.txt
├── DLOs_folder/
│   └── <Lesson Folders>/
│       └── Logs/
│           ├── entries.json
│           ├── Files_Uploaded-<date>.csv
│           └── ...
├── env/
│   └── ...
└── src/
    ├── anaklisi.py
    ├── anartisi.py
    ├── collect_metadata.py
    ├── create_dummies.py
    ├── delete_and_upload_files.py
    ├── diathesima_pros_epilegmena.py
    ├── epilegmena_pros_diathesima.py
    ├── main.py
    ├── update_metadata.py
    ├── data/
    │   └── lessons.py
    ├── js_scripts/
    │   ├── metadata-updater.js
    │   ├── parse-metadata.js
    │   ├── return-to-available.js
    │   └── ...
    └── py_functions/
        ├── load_excel_row_openpy.py
        ├── find_excel_openpy.py
        ├── write_to_CSV.py
        └── ...
```

---

## Requirements

- Python 3.10+
- Selenium
- Pillow (for image creation)
- Chrome, Edge, or Firefox browser
- Node.js (for running JS scripts outside Selenium, if needed)

Install dependencies:
```sh
pip install -r requirements.txt
```

---

## Usage

1. **Build the executable (optional):**
   ```sh
   ./build.bat
   ```
2. **Run the main script:**
   ```sh
   python src/main.py
   ```
   or, if you built the executable:
   ```sh
   dist/platformAutomate.exe
   ```
3. **Follow the prompts** to select browser and desired operation (upload, update metadata, collect metadata, etc.).

---

## Main Scripts

- [`src/main.py`](src/main.py): Entry point, handles user input and workflow selection.
- [`src/collect_metadata.py`](src/collect_metadata.py): Collects metadata from the platform.
- [`src/delete_and_upload_files.py`](src/delete_and_upload_files.py): Handles file upload and deletion.
- [`src/update_metadata.py`](src/update_metadata.py): Updates metadata on the platform.
- [`src/create_dummies.py`](src/create_dummies.py): Generates dummy DLOs for testing.

---

## JavaScript Automation

Custom JS scripts in [`src/js_scripts/`](src/js_scripts/) are injected via Selenium to automate UI actions, such as:

- Opening tabs and navigating between them
- Clicking buttons (e.g., submit, next tab, return to available)
- Filling forms and dropdowns (including jQuery UI and custom dropdowns)
- Extracting and parsing values from the DOM

**Key scripts:**
- [`metadata-updater.js`](src/js_scripts/metadata-updater.js): Handles step-by-step metadata update logic for each DLO.
- [`parse-metadata.js`](src/js_scripts/parse-metadata.js): Extracts metadata fields from the platform UI.
- [`return-to-available.js`](src/js_scripts/return-to-available.js): Automates returning DLOs from "selected" to "available" state.

Scripts are executed via `driver.execute_script()` in Python, passing parameters as needed (e.g., step number, metadata JSON).

---

## Data & Logging

- **Lesson Data:** Managed in [`src/data/lessons.py`](src/data/lessons.py).
- **Logs & Progress:** Each lesson folder in `DLOs_folder/<Lesson>/Logs/` contains:
  - `entries.json`: Tracks upload and metadata update status per DLO.
  - `Files_Uploaded-<date>.csv`: Exported metadata and upload logs.
- **Error Handling:** Errors and exceptions are logged to the console and relevant log files.

---

## Changelog

See [`changelog.txt`](changelog.txt) for detailed version history, bug fixes, and feature additions.

---

## Extending & Customization

- **Add new automation steps:** Create new JS scripts in [`src/js_scripts/`](src/js_scripts/) and call them from Python as needed.
- **Update lesson data:** Edit or extend [`src/data/lessons.py`](src/data/lessons.py).
- **Adjust workflow:** Modify [`src/main.py`](src/main.py) to add new menu options or workflows.

---

## Troubleshooting

- Ensure the correct browser driver is installed and matches your browser version.
- If the platform UI changes, update the relevant JS scripts in [`src/js_scripts/`](src/js_scripts/).
- Check the `Logs/` folder for per-lesson logs and error reports.

---

*This project is maintained for automating DLO management on the ebooksdl.cti.gr platform. For questions or contributions, please refer to the repository or contact the maintainer.*