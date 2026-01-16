## GitHub App & Permissions (Required for PR Comments)

HarperBot needs elevated GitHub permissions to comment on pull requests and create or update issues. If you see errors related to `actions/create-github-app-token@v2`, it means the required **GitHub App credentials are not configured**.

### Why this is needed

The default `GITHUB_TOKEN` may not have sufficient permissions in all repositories. To reliably post PR reviews and manage issues, HarperBot uses a **GitHub App token** with explicit scopes.

---

### Recommended Setup: GitHub App (Production)

#### 1. Create a GitHub App

Create a GitHub App under the **harpertoken** organization:

* Go to:
  [https://github.com/organizations/harpertoken/settings/apps](https://github.com/organizations/harpertoken/settings/apps)
* Click **New GitHub App**
* Configure:

  * **Name**: `HarperBot`
  * **Homepage URL**:
    [https://github.com/harpertoken/harperbot](https://github.com/harpertoken/harperbot)
  * **Webhook**: Disable (not required)
  * **Repository Permissions**:

    * Contents: **Read**
    * Issues: **Read & Write**
    * Pull Requests: **Read & Write**

After creation:

* Generate a **private key** and download the `.pem` file
* Note the **App ID**

---

#### 2. Add Repository Secrets

In `harpertoken/harperbot`:

* Go to **Settings → Secrets and variables → Actions**
* Add the following secrets:

| Name             | Value                                   |
| ---------------- | --------------------------------------- |
| `APP_ID`         | GitHub App ID                           |
| `PRIVATE_KEY`    | Full contents of the `.pem` private key |
| `GEMINI_API_KEY` | *(existing – no change)*                |

---

#### 3. Verify Workflow Configuration

Ensure `.github/workflows/harperbot.yml` uses the app credentials:

```yaml
- name: Create GitHub App token
  uses: actions/create-github-app-token@v2
  with:
    app-id: ${{ secrets.APP_ID }}
    private-key: ${{ secrets.PRIVATE_KEY }}
```

This token is then used by HarperBot to authenticate GitHub API requests.

---

### Alternative: Simple / Local Testing

For quick testing or forks, you may skip the GitHub App and use the built-in token:

* Modify the workflow to use `GITHUB_TOKEN` directly
* Be aware that permissions may be limited depending on repo settings

This approach is **not recommended for production**.
