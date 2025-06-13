# Blackbird-Assessment
CRM and feedback data merge project using Python and API

1. Project Description
This project simulates a CRM automation task where event feedback is used to update an existing contact record system. Using data retrieved from two APIs—one returning CRM data (CSV) and the other returning form submissions (JSON)—the goal is to merge and update contact logs, fill in missing data, and generate an output file for CRM ingestion.

2. Approach
    1) Data Collection
        - I retrieved CRM records using a CSV-based API and event form submissions using a JSON-based API. The CRM data provided structured contact records with fields like name, email, phone, and contact history (see screenshot: CRM Form print result.png).
        - The feedback data was nested under the data key and required normalization to access relevant fields such as name, email, timestamp, message, and phone (see screenshot: Feedback form data.png).

    2) Data Preprocessing
        From the form data, I:
        - Split the full name field into first and last names.
        - Renamed columns to match CRM naming conventions.
        - Added _form suffixes to avoid naming conflicts during the merge process.

    3) Merging and Updating
        - Merged both datasets using the email field as the primary key.
        - Used .combine_first() to update missing CRM values with form data while preserving existing values.
        - Replaced the last contact date and last contact text fields with the latest form submission.
        - Created an all contact text field to retain a complete communication history.

    4) Output and ID Handling
        - Automatically generated new unique IDs (bfx-####) for contacts without existing IDs.
        - Exported the final result to crm_update.csv with all required fields in the correct format.

3. Assumptions Made
- Email is treated as the unique identifier for each contact.
- Latest form feedback is considered more up-to-date and used to overwrite previous contact date and notes.
- Form names follow First Last format and are split accordingly.
- Only contacts missing an ID are assigned a new one following the CRM's existing format.

4. Tools Used
- Language: Python 3
- Libraries: pandas, requests
- Environment: Jupyter Notebook
- Output: crm_update.csv, screenshots, script.ipynb, script.py.txt
