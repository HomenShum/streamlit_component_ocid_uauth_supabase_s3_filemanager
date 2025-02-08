# streamlit_component_ocid_uauth_supabase_s3_filemanager
A lightweight Streamlit component for browsing and managing files in Supabase Storage (S3), featuring folder creation, file upload/download/delete, and user authentication via Streamlit's built-in user management.

# Lite S3 File Manager Streamlit Component (Supabase Storage)

[![Streamlit App](https://static.streamlit.io/badges/streamlit_badge_black_white.svg)](https://share.streamlit.io/your-streamlit-username/your-repo-name) <!-- Replace with your Streamlit Share link if deployed -->

A lightweight and user-friendly Streamlit component for browsing, managing, and interacting with files stored in Supabase Storage (S3-compatible). This component provides a simple web interface within your Streamlit application to perform common file management tasks directly in your browser.

**Features:**

*   **Browse S3 Buckets:** Navigate your Supabase Storage bucket's folders and files in a tree-like structure.
*   **Folder Management:**
    *   Create new folders.
    *   Delete folders (recursively deletes contents).
*   **File Management:**
    *   Upload files (with success feedback).
    *   Download files.
    *   Delete files.
*   **File Information:** Display file name, type, and size.
*   **Selection & Actions:** Select files and folders for batch actions (currently only folder deletion is implemented in batch).
*   **Pagination:**  Browse large folders with configurable items per page.
*   **User Authentication:** Leverages Streamlit's built-in user authentication (`st.experimental_user`) for secure access (Google Login).
*   **"Selected Items" DataFrame:** Displays a summary of selected folders and files in a Pandas DataFrame.
*   **Responsive Path Navigation:**  Breadcrumb-style path display with clickable components for easy navigation.

**Tech Stack:**

*   [Streamlit](https://streamlit.io/) -  For building the interactive web application.
*   [Supabase](https://supabase.com/) - As the backend and S3-compatible storage provider.
*   [boto3](https://boto3.amazonaws.com/v1/documentation/api/latest/index.html) - AWS SDK for Python to interact with S3-compatible storage.
*   [Pandas](https://pandas.pydata.org/) - For displaying selected items in a DataFrame.

**Setup and Installation:**

1.  **Prerequisites:**
    *   **Streamlit:**  Ensure you have Streamlit installed (`pip install streamlit`).
    *   **Supabase Account:** You need a Supabase project set up and a storage bucket created.
    *   **Secrets Configuration:** Configure your Streamlit secrets (usually in `.streamlit/secrets.toml` or Streamlit Cloud secrets) with your Supabase Storage credentials.  You'll need:
        ```toml
        [supabase]
        SUPABASE_URL = "YOUR_SUPABASE_URL"
        SUPABASE_KEY = "YOUR_SUPABASE_ANON_KEY" # or service_role key if needed for broader access

        [supabase.s3] # Supabase Storage (S3) Credentials
        SUPABASE_S3_BUCKET_NAME = "YOUR_SUPABASE_STORAGE_BUCKET_NAME"
        SUPABASE_S3_ENDPOINT_URL = "YOUR_SUPABASE_STORAGE_ENDPOINT_URL"
        SUPABASE_S3_BUCKET_REGION = "YOUR_SUPABASE_STORAGE_REGION"
        SUPABASE_S3_BUCKET_ACCESS_KEY = "YOUR_SUPABASE_STORAGE_ACCESS_KEY"
        SUPABASE_S3_BUCKET_SECRET_KEY = "YOUR_SUPABASE_STORAGE_SECRET_KEY"
        ```
        **Note:**  Obtain these credentials from your Supabase project settings -> Storage -> Settings.

2.  **Clone the Repository:**
    ```bash
    git clone [repository-url]
    cd streamlit_component_ocid_uauth_supabase_s3_filemanager
    ```

3.  **Install Dependencies:**
    ```bash
    pip install -r requirements.txt # if you have a requirements.txt
    # or
    pip install streamlit supabase boto3 pandas
    ```

**Usage:**

1.  **Run the Streamlit app:**
    ```bash
    streamlit run your_streamlit_app_file.py # e.g., streamlit run app.py
    ```

2.  **Integrate the component into your Streamlit app:**

    ```python
    import streamlit as st
    from sidebar_content_fragment_st_file_manager_component import sidebar_content_fragment_st_file_manager_component # Assuming your component code is in this file

    def main():
        with st.sidebar:
            sidebar_content_fragment_st_file_manager_component()

    if __name__ == "__main__":
        main()
    ```

    *   Make sure to replace `your_streamlit_app_file.py` and `sidebar_content_fragment_st_file_manager_component` with your actual file and function names.
    *   The component is designed to be placed in the Streamlit sidebar for a cleaner layout.

**Configuration:**

*   **Supabase Storage Credentials:**  As mentioned in the "Setup" section, configure these in your Streamlit secrets.
*   **Pagination:** The `ITEMS_PER_PAGE_OPTIONS` list in the code allows you to customize the available options in the "Items per page" dropdown. You can modify this list directly in your code.
*   **`KEY_PREFIX`:** This is used to avoid session state conflicts if you are using multiple instances of this component or other components that might use similar session state keys. You can change this prefix if needed.

**Contributing:**

[Optional: Add your contributing guidelines here, if you want to encourage contributions.]

**License:**

[Optional: Specify your license, e.g., MIT License]

---

**Disclaimer:** This is a "Lite" file manager and provides basic functionalities. For more advanced features, you might need to extend or customize it further based on your specific requirements.
