# 🔥 Hot Durham Sensor Dashboard

This project collects environmental sensor data from Weather Underground (WU) and TSI devices, uploads it to Google Sheets, and provides options for local data storage and OneDrive integration. It supports both command-line and GUI interfaces, allows for live data preview, and selective chart generation.

---

## 🚀 Features

- Pulls telemetry from WU and TSI cloud APIs
- Logs hourly and weekly summary data
- Option to combine all sensors into a single sheet or keep them separate
- Generates charts for various metrics including PM2.5, Temperature, Relative Humidity, Solar Radiation, Wind Speed, Precipitation, and Heat Index.
- Device names are included in chart legends.
- Streamlit GUI for TSI data with live chart previews
- Auto-shares Google Sheet with a specified email address
- Data exported to Google Sheets using `gspread`
- Optional local data download in CSV or Excel format
- Optional OneDrive upload for exported files

---

## 📁 Project Structure

- `app/` - Potentially for application-specific code (currently empty or contents unknown)
- `creds/` — Credential files:
   - `google_creds.json` (Google Service Account)
   - `tsi_creds.json` (TSI API)
   - `wu_api_key.json` (Weather Underground API)
   - `onedrive_creds.json` (Microsoft OneDrive, if used)
   - `README.md` (Instructions for credentials)
- `hot_durham_wu_map/` - Web application for displaying WU data on a map:
   - `backend/server.js` (Node.js backend)
   - `frontend/index.html` (HTML/JS frontend)
- `oldPulls/` — Legacy data pulling scripts:
   - `old_wu_datapull.py`
   - `oldtsi_datapull.py`
- `scripts/` — Main Python scripts for data processing and Google Sheets integration:
   - `faster_wu_tsi_to_sheets_async.py` (Primary script for WU/TSI data to Sheets, with async operations)
   - `combined_wu_tsi_to_sheets_using_parallel.py` (Older version, uses parallel processing)
   - `tsi_streamlit_gui_with_preview.py` (Streamlit GUI for TSI data)
   - `tsi_to_google_sheets.py` (Script focused on TSI to Sheets)
- `README.md` — This file.
- `requirements.txt` — Python dependencies.
- `package.json` — Node.js dependencies (for `hot_durham_wu_map`).
- `toDo` — A file for tracking tasks and issues.
- `Hot Durham.iml` - IntelliJ IDEA module file.

---

## ⚙️ Setup

1.  **Clone the repository**
    ```bash
    git clone <your-repo-url>
    cd "Hot Durham"
    ```

2.  **Create a Python virtual environment (recommended)**
    ```bash
    python3 -m venv .venv
    source .venv/bin/activate  # On Windows: .venv\Scripts\activate
    ```

3.  **Install Python dependencies**
    ```bash
    pip install --upgrade pip
    pip install -r requirements.txt
    ```

4.  **Install Node.js dependencies (for WU Map)**
    Navigate to the `hot_durham_wu_map/backend/` directory:
    ```bash
    cd hot_durham_wu_map/backend/
    npm install
    cd ../../ # Navigate back to the project root
    ```

5.  **Place credentials in the `creds/` folder:**
   *   Save your TSI API credentials as `tsi_creds.json`.
   *   Save your Google Cloud Platform service account key as `google_creds.json`.
      *   Ensure the Google Drive API and Google Sheets API are enabled for your GCP project.
   *   Save your Weather Underground API key as `wu_api_key.json`.
   *   If using OneDrive, save your Microsoft Graph API credentials as `onedrive_creds.json`. (Refer to Microsoft documentation for creating these credentials).

    > ⚠️ These credential files are listed in `.gitignore` and should **never** be committed to your Git repository.

---

## ▶️ Usage

### Primary Script (Recommended for WU & TSI Data)

This script fetches data from both Weather Underground and TSI, then uploads it to Google Sheets. It uses asynchronous operations for improved performance.

```bash
python scripts/faster_wu_tsi_to_sheets_async.py
```

You will be prompted for:
- Data sources to fetch (WU, TSI, or Both)
- Start and end dates for data retrieval
- Email address to share the Google Sheet with
- Whether to save data locally (and file format/directory if yes)
- Whether to upload exported files to OneDrive (and folder path if yes)
- Whether to add charts to the Google Sheet

### TSI Data with Streamlit GUI

This script provides a graphical interface for fetching TSI data and previewing charts before uploading to Google Sheets.

```bash
streamlit run scripts/tsi_streamlit_gui_with_preview.py
```

1.  Upload your `tsi_creds.json` and `google_creds.json` files via the GUI.
2.  Choose the date range.
3.  Preview PM2.5, Temperature, and Relative Humidity charts.
4.  Click "Upload to Google Sheets" to generate the sheet.

### Other Scripts

-   `scripts/combined_wu_tsi_to_sheets_using_parallel.py`: An older version of the primary script that uses parallel processing.
-   `scripts/tsi_to_google_sheets.py`: A simpler script focused solely on TSI data to Google Sheets.

---

## 🗺️ Weather Underground Map Application

This project includes a simple web application to display Weather Underground station data on a map.

1.  **Start the backend server:**
    ```bash
    node hot_durham_wu_map/backend/server.js
    ```
    The server will typically start on `http://localhost:3000`.

2.  **Open the frontend:**
    Open `hot_durham_wu_map/frontend/index.html` in your web browser.

    *Note: Ensure your `wu_api_key.json` is also present in the `hot_durham_wu_map/backend/` directory for the map application to function correctly.*

---

## 📝 Notes

-   For backend/frontend development of the WU map, see the `hot_durham_wu_map/` directory.
-   Legacy scripts are available in the `oldPulls/` directory but are not actively maintained.
-   For any issues, feature requests, or tasks, check the `toDo` file or open an issue on the project's GitHub repository.

---

*Last updated: May 18, 2025*

