Technical Writing Practical Lab
## Professional Documentation Exercises

**Prepared by:** Mohamed Hassan Diriye  
**Institution:** ILO Student – DRC-IFO1 Hub  
**Audience:** First-semester computing students

---

## Contents

1. Exercise A: User Manual Procedure — Create a GitHub Repository and Make a First Commit
2. Exercise B: API Reference Entry — Create a Task in a Project Management Application

---

# Exercise A: User Manual Procedure

## Create a GitHub Repository and Make a First Commit

### 1. Purpose and outcome

This procedure guides a beginner through creating a GitHub repository, preparing a local project folder, recording the first change with Git, and publishing the project to GitHub. When finished, the GitHub repository should contain a `README.md` file on the `main` branch and show an initial commit.

### 2. Prerequisites

Before starting, make sure you have:

- A computer running Windows, macOS, or Linux and an internet connection.
- An active GitHub account.
- Git installed and available in a terminal. Confirm this by running `git --version`.
- Visual Studio Code (VS Code) or another text editor.
- Basic familiarity with a web browser and terminal.

> **Note:** GitHub may ask you to authenticate when you push. Follow the sign-in prompt or use the authentication method configured for your account. Do not share your password or access token.

### 3. Procedure

#### Part 1: Create the remote repository

**Step 1 — Open GitHub and sign in**  
Open a browser, go to [https://github.com](https://github.com), and sign in.  
**Checkpoint:** Your GitHub dashboard is visible.

**Step 2 — Start a new repository**  
Select **New repository** (or use the plus menu and choose **New repository**).  
**Checkpoint:** The repository creation form opens.

**Step 3 — Configure the repository**  
Enter `my-first-project` as the repository name. Choose **Public** or **Private** according to your needs. For this procedure, leave **Add a README file** unchecked so that the remote repository starts empty.  
**Checkpoint:** The name and visibility are selected, and no README has been initialized online.

**Step 4 — Create the repository**  
Select **Create repository**.  
**Checkpoint:** The new, empty repository page appears. Keep this page open; the repository URL will be needed later.

#### Part 2: Prepare the local project

**Step 5 — Create a project folder**  
On your computer, create a folder named `my-first-project` in a convenient location.  
**Checkpoint:** The folder exists in File Explorer (Windows), Finder (macOS), or your file manager (Linux).

**Step 6 — Open the folder in VS Code**  
In VS Code, select **File > Open Folder** and choose `my-first-project`.  
**Checkpoint:** The folder name appears in the Explorer panel.

**Step 7 — Create and save a README**  
Create a file named `README.md` in the project folder. Add a brief project name and description, then save it. For example:

```markdown
# My First Project

A practice project for learning Git and GitHub.
```

**Checkpoint:** `README.md` appears in the Explorer and contains the saved text.

#### Part 3: Commit and publish the project

**Step 8 — Open a terminal in the project folder**  
In VS Code, select **Terminal > New Terminal**. Confirm that the terminal is located in the `my-first-project` folder. If needed, change directory to that folder before continuing.  
**Checkpoint:** The terminal prompt points to the project folder.

**Step 9 — Initialize Git**  
Run:

```bash
git init
```

**Checkpoint:** Git reports that an empty repository has been initialized. If Git is unavailable, see Troubleshooting.

**Step 10 — Stage the README**  
Run:

```bash
git add README.md
```

**Checkpoint:** The file is staged. To inspect the staging status, run `git status`; `README.md` should appear under “Changes to be committed.”

**Step 11 — Create the first commit**  
Run:

```bash
git commit -m "Initial commit"
```

**Checkpoint:** Git confirms that a commit was created. If Git asks for your identity, configure your name and email using the instructions in Troubleshooting, then repeat the commit.

**Step 12 — Connect the local repository to GitHub**  
Copy the HTTPS URL from the empty repository page. It should look like `https://github.com/YOUR-USERNAME/my-first-project.git`. Replace `YOUR-USERNAME` with your GitHub username, then run:

```bash
git remote add origin https://github.com/YOUR-USERNAME/my-first-project.git
```

**Checkpoint:** The remote named `origin` is configured. You can verify it with `git remote -v`.

**Step 13 — Name the branch `main`**  
Run:

```bash
git branch -M main
```

**Checkpoint:** The current branch is named `main`.

**Step 14 — Push the commit to GitHub**  
Run:

```bash
git push -u origin main
```

If prompted, complete GitHub authentication in the browser or through your configured credential manager.  
**Checkpoint:** Git reports that the branch was pushed and set to track `origin/main`.

### 4. Verify the result

Refresh the GitHub repository page. Confirm that:

- The repository is named `my-first-project`.
- The selected branch is `main`.
- `README.md` is listed and its contents are visible.
- The commit history includes **Initial commit**.

### 5. Screenshot evidence

Capture a screenshot of the completed repository page. Make sure the repository name, `main` branch, `README.md`, and **Initial commit** are visible. Do not include private information, credentials, or access tokens in the screenshot. Insert the screenshot in the submitted version of this exercise.

### 6. Troubleshooting

| Problem | Likely cause | Resolution |
|---|---|---|
| `git` is not recognized or command not found | Git is not installed or is not on the system PATH | Install Git from [https://git-scm.com](https://git-scm.com), reopen VS Code, and run `git --version`. |
| Commit fails because author identity is unknown | Git has not been configured with a name and email | Set them with `git config --global user.name "Your Name"` and `git config --global user.email "you@example.com"`, then retry the commit. Use the email associated with your GitHub account if you want commits linked to that account. |
| Push is rejected because the remote contains work | The GitHub repository was initialized with a file such as a README, so local and remote histories differ | For a beginner workflow, create a new empty GitHub repository and repeat the remote setup. Do not force-push unless you understand the effect. |
| Authentication fails during push | The account has not completed browser or credential-manager authentication | Follow the sign-in prompt. GitHub account passwords are not accepted as Git HTTPS credentials; use the supported browser sign-in or credential manager. Never paste a token into a shared document. |
| `remote origin already exists` | A remote named `origin` is already configured | Run `git remote -v` to inspect it. Correct the URL with `git remote set-url origin REPOSITORY-URL` if necessary. |

### 7. Conclusion

A successful first push demonstrates the basic local-to-remote workflow: create a repository, stage a change, save it in a commit, and publish the commit. The verification checks confirm that the expected file and commit are available on GitHub.

---

# Exercise B: API Reference Entry

## Create a Task in a Project Management Application

### 1. Overview

The Create Task endpoint adds a task to an existing project. An authenticated user with permission to manage that project submits task details as JSON. On success, the service returns the created task and its server-generated identifier.

This reference describes a sample API contract for the exercise. The endpoint and response format are illustrative; an actual application may use different field names or validation rules.

### 2. Endpoint

| Method | Path | Purpose |
|---|---|---|
| `POST` | `/v1/projects/{project_id}/tasks` | Create a task in the specified project. |

Replace `{project_id}` with the UUID of the target project. The request body must be JSON.

### 3. Authentication and permissions

Send a valid bearer access token in the `Authorization` header. The authenticated user must have permission to create tasks in the selected project. The project must exist, and the assigned user must be valid for that project.

### 4. Parameters

#### Path parameter

| Name | Type | Required | Description |
|---|---|---:|---|
| `project_id` | UUID string | Yes | Unique identifier of the project that will contain the task. |

#### Query parameters

None.

#### Request body

| Field | Type | Required | Description and validation |
|---|---|---:|---|
| `title` | String | Yes | Task name. Must contain at least one non-whitespace character. |
| `description` | String | No | Additional task details. May be omitted or set to an empty string. |
| `assignee_id` | String | Yes | Identifier of a valid user who belongs to the project. |
| `due_date` | String (`YYYY-MM-DD`) | Yes | Due date in calendar-date format, for example `2026-12-15`. |
| `priority` | String enum | Yes | One of `low`, `medium`, or `high`. Values are lowercase. |

The server generates `task_id`, `status`, and `created_at`; clients should not include these fields when creating a task.

### 5. Request headers

| Header | Required | Example | Purpose |
|---|---:|---|---|
| `Authorization` | Yes | `Bearer YOUR_ACCESS_TOKEN` | Authenticates the request. |
| `Content-Type` | Yes | `application/json` | Declares the request body format. |
| `Accept` | Recommended | `application/json` | Requests a JSON response. |

### 6. Example request

```http
POST /v1/projects/550e8400-e29b-41d4-a716-446655440000/tasks HTTP/1.1
Host: api.example.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json
Accept: application/json

{
  "title": "Prepare project report",
  "description": "Complete the monthly project progress report.",
  "assignee_id": "usr_10245",
  "due_date": "2026-12-15",
  "priority": "high"
}
```

Replace the example host, project ID, user ID, and token with valid values for the service. Treat access tokens as secrets.

### 7. Successful response

A successful creation returns **`201 Created`** and a JSON representation of the new task. Example:

```json
{
  "success": true,
  "message": "Task created successfully",
  "data": {
    "task_id": "task_78901",
    "project_id": "550e8400-e29b-41d4-a716-446655440000",
    "title": "Prepare project report",
    "description": "Complete the monthly project progress report.",
    "assignee_id": "usr_10245",
    "due_date": "2026-12-15",
    "priority": "high",
    "status": "pending",
    "created_at": "2026-11-25T10:30:00Z"
  }
}
```

`created_at` is an ISO 8601 timestamp in UTC, indicated by the `Z` suffix. The example values are illustrative.

### 8. Error responses

| HTTP status | Meaning | Typical cause and client action |
|---|---|---|
| `400 Bad Request` | Malformed request | Correct invalid JSON or request formatting. |
| `401 Unauthorized` | Authentication failed | Provide a valid, unexpired access token. |
| `403 Forbidden` | Permission denied | Confirm that the user may create tasks in this project. |
| `404 Not Found` | Resource not found | Check the project ID and assignee ID. |
| `409 Conflict` | Request conflicts with current resource state | Review the project state or duplicate/conflicting task rules, then retry only when appropriate. |
| `422 Unprocessable Entity` | Field validation failed | Correct missing, invalid, or out-of-range field values. |
| `429 Too Many Requests` | Rate limit exceeded | Wait before retrying; follow any `Retry-After` response header. |
| `500 Internal Server Error` | Unexpected server failure | Retry later if appropriate; contact the service operator if it continues. |
| `503 Service Unavailable` | Service temporarily unavailable | Retry later, preferably with backoff. |

Error response bodies are not specified in this sample contract. A production API reference should document the error body schema if the service defines one.

### 9. Implementation notes

- The project must exist before task creation.
- The assignee must be a valid project member.
- The title cannot be blank, and priority must be one of the documented values.
- The due date must be a valid date in `YYYY-MM-DD` format.
- The server assigns the task ID, initial status, and creation timestamp.
- Do not expose bearer tokens in source control, screenshots, or shared documents.

### 10. Conclusion

This reference gives a client developer the information needed to create a task: endpoint and authentication details, field requirements, a complete request example, the expected success response, and common error conditions. Clear response and validation documentation helps clients form valid requests and respond appropriately to failures.
