# sqs-zscaler-tableau

## How to Deploy Custom Extensions for Clients

Currently, the custom Tableau extensions run on a local development server (`http://localhost:8766` and `http://localhost:8767`). This means anyone opening the `.twbx` file must also run the Python server locally.

To share the Tableau workbook with clients without requiring them to set up a local server, you can host the extensions using **GitHub Pages**. 

### Step 1: Push the Repository to GitHub
1. Commit all your files and push them to a GitHub repository.
   *Note: If the repository is private, GitHub Pages requires a GitHub Enterprise or Pro account. Otherwise, you can use a public repository to host the extension UI.*

### Step 2: Enable GitHub Pages
1. Go to your repository on GitHub.
2. Navigate to **Settings** > **Pages** (on the left sidebar).
3. Under **Build and deployment**, select **Deploy from a branch**.
4. Choose your main branch (e.g., `main` or `master`), select the `/ (root)` folder, and save.
5. GitHub will generate a URL for your site, typically looking like:
   `https://<your-username>.github.io/sqs-zscaler-tableau/`

### Step 3: Update the `.trex` Manifest Files
You need to update the `<url>` tags in the manifest files to point to the new GitHub Pages URLs instead of `localhost`.

Open the following files:
1. `custom extensions/hierarchy viz extension/manifest.trex`
2. `custom extensions/Filter extension/manifest.trex`

Change the `<url>` tag inside `<source-location>`:

**From:**
```xml
<url>http://localhost:8766/index.html</url>
<!-- or 8767 for the filter -->
```

**To:**
```xml
<url>https://<your-username>.github.io/sqs-zscaler-tableau/custom%20extensions/hierarchy%20viz%20extension/index.html</url>
<!-- and for the filter: -->
<url>https://<your-username>.github.io/sqs-zscaler-tableau/custom%20extensions/Filter%20extension/index.html</url>
```
*(Note: Be sure to replace `<your-username>` with your actual GitHub username, and ensure spaces in the folder path are replaced with `%20`).*

### Step 4: Update the Tableau Dashboard
1. Open your `.twbx` file in Tableau Desktop.
2. Remove the old localhost extensions from the dashboard, or reload them by selecting the newly updated `.trex` files.
3. Save the `.twbx` file.

### Step 5: Share with the Client
Now you can send the `.twbx` file to your client. When they open it, Tableau will fetch the extension's UI and logic directly from GitHub Pages. They will not need to run any local Python server!