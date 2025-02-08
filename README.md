# 🚀 Lite S3 File Manager Streamlit Component (Supabase Storage) 📁

[![Streamlit App](https://static.streamlit.io/badges/streamlit_badge_black_white.svg)](https://st-supabase-s3-manager-with-ocid.streamlit.app/) <!--  Streamlit Share link -->
[![Open Source Love](https://badges.frapsoft.com/os/v1/open-source.svg?v=103)](https://github.com/HomenShum/streamlit_component_ocid_uauth_supabase_s3_filemanager) <!--  GitHub repo -->

A lightweight and user-friendly Streamlit component for browsing, managing, and interacting with files stored in Supabase Storage (S3-compatible).  This component provides a simple web interface within your Streamlit application to perform common file management tasks directly in your browser.

**✨ Features:**

*   **📂 Browse S3 Buckets:** Navigate your Supabase Storage bucket's folders and files in a tree-like structure.
*   **📁 Folder Management:**
    *   ➕ Create new folders.
    *   🗑️ Delete folders (recursively deletes contents).
*   **📄 File Management:**
    *   ⬆️ Upload files (with success feedback).
    *   ⬇️ Download files.
    *   ❌ Delete files.
*   **ℹ️ File Information:** Display file name, type, and size.
*   **☑️ Selection & Actions:** Select files and folders for batch actions (currently only folder deletion is implemented in batch).
*   **🔢 Pagination:**  Browse large folders with configurable items per page.
*   **🔒 User Authentication:** Leverages Streamlit's built-in user authentication (OpenID Connect - Google Identity) for secure access.
*   **📊 "Selected Items" DataFrame:** Displays a summary of selected folders and files in a Pandas DataFrame.
*   **🧭 Responsive Path Navigation:**  Breadcrumb-style path display with clickable components for easy navigation.

**🛠️ Tech Stack:**

*   [<img src="https://streamlit.io/images/brand/streamlit-mark-color.png" width="25"> Streamlit](https://streamlit.io/) -  For building the interactive web application.
*   [<img src="https://supabase.com/favicon/favicon.ico" width="25"> Supabase](https://supabase.com/) - As the backend and S3-compatible storage provider.
*   [<img src="https://boto3.amazonaws.com/v1/documentation/api/latest/_static/boto3-logo.png" width="35"> boto3](https://boto3.amazonaws.com/v1/documentation/api/latest/index.html) - AWS SDK for Python to interact with S3-compatible storage.
*   [<img src="https://pandas.pydata.org/static/img/favicon.ico" width="20"> Pandas](https://pandas.pydata.org/) - For displaying selected items in a DataFrame.
*   **🔐 OpenID Connect (OIDC)** -  For User Authentication via Google Identity.

**⚙️ Setup and Installation:**

1.  **Prerequisites:**
    *   **Streamlit:**  Ensure you have Streamlit installed (`pip install streamlit`).
    *   **Supabase Account:** You need a Supabase project set up and a storage bucket created.
    *   **Google Cloud Platform Project:** You need a Google Cloud Platform project to configure the OAuth 2.0 Client ID for Google Login.
    *   **Secrets Configuration:** Configure your Streamlit secrets (usually in `.streamlit/secrets.toml` or Streamlit Cloud secrets) with your Supabase Storage credentials and Google Login credentials.

2.  **Supabase Storage Secrets:** Add the following to your Streamlit secrets:

    ```toml
    [supabase]
    SUPABASE_URL = "YOUR_SUPABASE_URL"
    SUPABASE_KEY = "YOUR_SUPABASE_ANON_KEY" # or service_role key if needed for broader access
    SUPABASE_S3_BUCKET_NAME = "YOUR_SUPABASE_STORAGE_BUCKET_NAME"
    SUPABASE_S3_ENDPOINT_URL = "YOUR_SUPABASE_STORAGE_ENDPOINT_URL"
    SUPABASE_S3_BUCKET_REGION = "YOUR_SUPABASE_STORAGE_REGION"
    SUPABASE_S3_BUCKET_ACCESS_KEY = "YOUR_SUPABASE_STORAGE_ACCESS_KEY"
    SUPABASE_S3_BUCKET_SECRET_KEY = "YOUR_SUPABASE_STORAGE_SECRET_KEY"
    ```

    **Note:**  Obtain these credentials from your Supabase project settings -> Storage -> Settings.

3.  **Google Login (OIDC) Secrets:** Configure Google Login for user authentication. You need to set up an OAuth 2.0 Client ID in your Google Cloud Platform project.

    *   **Google Cloud Setup:**
        1.  Go to the [Google Cloud Console](https://console.cloud.google.com/).
        2.  Select your project (or create a new one).
        3.  Navigate to "APIs & Services" > "Credentials".
        4.  Click "+ CREATE CREDENTIALS" > "OAuth client ID".
        5.  Select "Web application" as the Application type.
        6.  Give your OAuth 2.0 client a name (e.g., "Streamlit App Login").
        7.  In "Authorized redirect URIs", add your app's redirect URI. For local development, this is typically `http://localhost:8501/oauth2callback`. If deploying to Streamlit Cloud, use your Streamlit app's URL with `/oauth2callback` appended (e.g., `https://your-streamlit-app.streamlit.app/oauth2callback`).
        8.  Click "CREATE".
        9.  You will be given your **Client ID** and **Client secret**.

    *   **Add Google Login secrets to `.streamlit/secrets.toml`:**

        ```toml
         [auth]
         redirect_uri = "http://localhost:8501/oauth2callback" # Or your Streamlit Cloud app URL + /oauth2callback
         cookie_secret = "YOUR_RANDOM_STRONG_SECRET" # Generate a strong random string
         client_id = "YOUR_GOOGLE_CLIENT_ID" # Get it from Google Cloud Platform under your project
         client_secret = "YOUR_GOOGLE_CLIENT_SECRET" # Get it from Google Cloud Platform under your project
         server_metadata_url = "https://accounts.google.com/.well-known/openid-configuration"
        ```

        *   **`redirect_uri`**:  Must match the "Authorized redirect URIs" you configured in Google Cloud. For local development, use `http://localhost:8501/oauth2callback`. For Streamlit Cloud, use your deployed app URL + `/oauth2callback`.
        *   **`cookie_secret`**: This is used to securely sign the user's session cookie. Generate a strong, random string. You can use online tools or Python's `secrets` module to generate this (e.g., `import secrets; secrets.token_urlsafe(32)`). Keep this secret value secure.
        *   **`client_id`**:  Your OAuth 2.0 Client ID from Google Cloud.
        *   **`client_secret`**: Your OAuth 2.0 Client Secret from Google Cloud.
        *   **`server_metadata_url`**: This is the standard OpenID configuration URL for Google Identity.

4.  **Clone the Repository:**

    ```bash
    git clone https://github.com/HomenShum/streamlit_component_ocid_uauth_supabase_s3_filemanager.git
    cd streamlit_component_ocid_uauth_supabase_s3_filemanager
    ```

5.  **Install Dependencies:**

    ```bash
    pip install -r requirements.txt # if you have a requirements.txt
    # or
    pip install streamlit supabase boto3 pandas
    ```

**🚀 Usage:**

1.  **Run the Streamlit app:**

    ```bash
    streamlit run your_streamlit_app_file.py # e.g., streamlit run app.py
    ```

2.  **Integrate the component into your Streamlit app:**

    ```python
    import streamlit as st
    from sidebar_content_fragment_st_file_manager_component import sidebar_content_fragment_st_file_manager_component  # Assuming your component code is in this file

    def main():
        if not st.experimental_user.is_logged_in:
            st.button("🔑 Log in with Google", on_click=st.login)
            st.stop()  # Stop the app execution until the user logs in

        if st.button("🚪 Log out"):
            st.logout()

        st.sidebar.markdown(f"👋 Welcome, {st.experimental_user.name}!")  # Display user name in sidebar

        with st.sidebar:
            sidebar_content_fragment_st_file_manager_component()

    if __name__ == "__main__":
        main()
    ```

    *   Make sure to replace `your_streamlit_app_file.py` and `sidebar_content_fragment_st_file_manager_component` with your actual file and function names.
    *   The component is designed to be placed in the Streamlit sidebar for a cleaner layout.
    *   The example code demonstrates basic user login and logout using `st.experimental_user`, `st.login()`, and `st.logout()`.
    *   The `st.stop()` after `st.login()` prevents the rest of the app from running until the user successfully logs in, simplifying the control flow.

**🔐 User Authentication Details:**

*   **Streamlit User Authentication:** This component utilizes Streamlit's built-in user authentication feature, which is based on OpenID Connect (OIDC) and configured to use Google Identity Provider by default.
*   **`st.experimental_user`:**  This object provides access to user information after successful login. `st.experimental_user.is_logged_in` checks the login status.  `st.experimental_user.name` (and other attributes depending on Google's configuration) provides user details.
*   **`st.login()`:**  Redirects the user to Google for login. After successful authentication, Streamlit sets an identity cookie and redirects back to your app.
*   **`st.logout()`:** Removes the identity cookie, logging the user out.
*   **Session Management:** Streamlit manages user sessions using cookies. If a user logs in, they will remain logged in across different tabs of the same app in the browser.
*   **Cookie Expiration:** The identity cookie expires after 30 days of inactivity in the browser. This expiration is managed by Streamlit and is not configurable.
*   **Security:** Streamlit handles the secure storage of the identity cookie.  It's crucial to keep your `cookie_secret`, `client_id`, and `client_secret` secure and not expose them in your client-side code.

**⚙️ Configuration:**

*   **Supabase Storage Credentials:**  As mentioned in the "Setup" section, configure these in your Streamlit secrets.
*   **Google Login Credentials:** Configure these in your Streamlit secrets as detailed in the "Setup" section.
*   **Pagination:** The `ITEMS_PER_PAGE_OPTIONS` list in the code allows you to customize the available options in the "Items per page" dropdown. You can modify this list directly in your code.
*   **`KEY_PREFIX`:** This is used to avoid session state conflicts if you are using multiple instances of this component or other components that might use similar session state keys. You can change this prefix if needed.
*   **Advanced OIDC Parameters:** For more advanced customization of the login flow (e.g., changing scopes, prompts), you can explore the `client_kwargs` option as described in the [Streamlit documentation for `st.login()`](https://docs.streamlit.io/library/api-reference/authentication/st.login). You would add a `client_kwargs` dictionary under the `[auth.google]` section in your `secrets.toml`.

**🤝 Contributing:**

[Optional: Add your contributing guidelines here, if you want to encourage contributions.]

**📄 License:**

[Optional: Specify your license, e.g., MIT License]

---

**⚠️ Disclaimer:** This is a "Lite" file manager and provides basic functionalities. For more advanced features, you might need to extend or customize it further based on your specific requirements.  Remember to replace placeholders like, `your_streamlit_app_file.py`, `sidebar_content_fragment_st_file_manager_component`, `YOUR_SUPABASE_URL`, `YOUR_SUPABASE_KEY`, `YOUR_SUPABASE_STORAGE_BUCKET_NAME`, `YOUR_SUPABASE_STORAGE_ENDPOINT_URL`, `YOUR_SUPABASE_STORAGE_REGION`, `YOUR_SUPABASE_STORAGE_ACCESS_KEY`, `YOUR_SUPABASE_STORAGE_SECRET_KEY`, `YOUR_GOOGLE_CLIENT_ID`, `YOUR_GOOGLE_CLIENT_SECRET`, and `YOUR_RANDOM_STRONG_SECRET` with your actual values.

**🎬 Demo:**

[Streamlit App Demo](https://st-supabase-s3-manager-with-ocid.streamlit.app/)

![Streamlit Lite S3 File Manager Supabase Storage - Demo Gif](https://github.com/HomenShum/streamlit_component_ocid_uauth_supabase_s3_filemanager/raw/main/Streamlit%20Lite%20S3%20File%20Manager%20Supabase%20Storage%20-%20Demo%20Gif%20020825.gif)

**📹 Youtube Link:**
https://www.youtube.com/watch?v=BTsZI-Oq-Fc

## Supabase Storage Policies and SQL Examples (Publicly Viewable)

**Storage Policies:**

Safeguard your files with policies that define the operations allowed for users at the bucket level.  Below are some example policies (replace `14q6af7` with your unique user identifiers as needed):

*   **Give users access to their own folder (SELECT):**

    ```sql
    -- Policy Name: Give users access to own folder (SELECT)
    -- Policy Target:  SELECT
    -- Using Expression:  auth.uid() = '14q6af7_0'  -- Example:  Replace with your logic
    ```
*    **Give users access to own folder (INSERT):**
    ```sql
    -- Policy Name: Give users access to own folder (INSERT)
    -- Policy Target: INSERT
    -- WITH CHECK Expression: auth.uid() = '14q6af7_1' -- Example: Replace
    ```
* **Give users access to own folder (UPDATE):**
    ```sql
    -- Policy Name: Give users access to own folder (UPDATE)
    -- Policy Target: UPDATE
    -- Using Expression: auth.uid() = '14q6af7_2' -- Example: Replace
    -- WITH CHECK Expression: auth.uid() = '14q6af7_2' -- Example: Replace
    ```
*   **Give users access to own folder (DELETE):**
    ```sql
     -- Policy Name: Give users access to own folder (DELETE)
    -- Policy Target: DELETE
    -- Using Expression: auth.uid() = '14q6af7_3'  -- Example: Replace
    ```

**SQL Examples:**

The following SQL code demonstrates how to create tables for managing user data and storage information, along with setting up Row Level Security (RLS) policies.  This provides a basic structure for linking users to their respective folders in Supabase Storage.

```sql
-- Create the users table with id as uuid
CREATE TABLE public.users (
    id uuid primary key,
    email text NOT NULL,
    name text,
    google_sub text,      -- For linking to Google User ID
    created_at timestamp with time zone default now(),
    CONSTRAINT users_email_unique UNIQUE (email)
);

-- Create the storage table with user_id referencing the users table
CREATE TABLE public.storage (
    id bigint primary key generated always as identity,
    bucket_id text,  --  Store the bucket name here (e.g., 'my-documents')
    foldername text,  -- The folder path within the bucket
    user_id uuid references public.users(id) on delete cascade,
    created_at timestamp with time zone default now()
);

-- Create the RLS policy for the storage table
-- This allows users to SELECT their own folders within *their* bucket.
CREATE POLICY "Allow user access to their own folders"
ON public.storage
FOR SELECT
USING (
    bucket_id = 'YOUR_BUCKET_NAME' AND  --  IMPORTANT: Replace 'YOUR_BUCKET_NAME' with your actual bucket name
    user_id = auth.uid()
);

-- Enable Row Level Security on the storage table
ALTER TABLE public.storage ENABLE ROW LEVEL SECURITY;
```
