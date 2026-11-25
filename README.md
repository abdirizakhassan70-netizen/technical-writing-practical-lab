# TECHNICAL WRITING PRACTICAL LAB

**Professional Documentation Exercises**

- Exercise A: User Manual Procedure
- Exercise B: API Reference Entry

**Prepared for:** First-Semester Computing Student  
**Submission-ready document**

**MOHAMED HASSAN DIRIYE**  
**ILO STUDENT - DRC-IFO1 HUB**

## Contents

- [Exercise A – User Manual Procedure](#exercise-a--user-manual-procedure)
- [Exercise B – API Reference Entry](#exercise-b--api-reference-entry)

# EXERCISE A: USER MANUAL PROCEDURE

## How to Create a GitHub Repository and Make Your First Commit

### 1. Introduction

GitHub is an online platform that allows developers to store, manage, and share software projects. It works with Git, a version control system that records changes made to project files. This procedure explains how a beginner can create a GitHub repository, add a project file, make a first commit, and upload the project to GitHub.

### 2. Prerequisites

- A computer running Windows, macOS, or Linux.
- A stable internet connection.
- An active GitHub account.
- Git installed on your computer.
- Visual Studio Code (VS Code) or another text editor.
- Basic experience using a web browser and a computer terminal.

### 3. Step-by-Step Procedure

#### Step 1: Open GitHub

**Action:** Open a web browser and go to https://github.com.  
**Expected result:** The GitHub homepage appears.

#### Step 2: Sign in to GitHub

**Action:** Enter your GitHub username or email address and password, then sign in.  
**Expected result:** Your GitHub dashboard opens.

#### Step 3: Start repository creation

**Action:** Select the **New repository** option.  
**Expected result:** The repository creation page appears.

#### Step 4: Enter a repository name

**Action:** Type `my-first-project` in the **Repository name** field.  
**Expected result:** The repository name is displayed in the form.

#### Step 5: Choose repository visibility

**Action:** Select **Public** or **Private**.  
**Expected result:** Your selected visibility option is shown.

#### Step 6: Create the repository

**Action:** Select **Create repository**.  
**Expected result:** GitHub creates the repository and displays its page.

#### Step 7: Create a local project folder

**Action:** Create a folder named `my-first-project` on your computer.  
**Expected result:** The new folder appears in the selected location.

#### Step 8: Open the folder in VS Code

**Action:** Open VS Code and select the `my-first-project` folder.  
**Expected result:** The folder appears in the VS Code Explorer.

#### Step 9: Create a README file

**Action:** Create a new file named `README.md` in the project folder.  
**Expected result:** `README.md` appears in the Explorer.

#### Step 10: Add project information

**Action:** Type a short description of the project in `README.md` and save the file.  
**Expected result:** The description is saved in `README.md`.

#### Step 11: Open the integrated terminal

**Action:** In VS Code, open **Terminal** and select **New Terminal**.  
**Expected result:** A terminal opens at the bottom of the VS Code window.

#### Step 12: Initialize Git

**Action:** Run:

```bash
git init
```

**Expected result:** Git initializes a local repository.

#### Step 13: Stage the README file

**Action:** Run:

```bash
git add README.md
```

**Expected result:** `README.md` is added to the Git staging area.

#### Step 14: Create the first commit

**Action:** Run:

```bash
git commit -m "Initial commit"
```

**Expected result:** Git records the first commit.

#### Step 15: Connect the remote repository

**Action:** Run the following command, replacing `YOUR-USERNAME` with your GitHub username:

```bash
git remote add origin https://github.com/YOUR-USERNAME/my-first-project.git
```

**Expected result:** The local repository is connected to the GitHub repository.

#### Step 16: Set the main branch name

**Action:** Run:

```bash
git branch -M main
```

**Expected result:** The current branch is named `main`.

#### Step 17: Upload the project

**Action:** Run:

```bash
git push -u origin main
```

**Expected result:** The committed project file is uploaded to GitHub.

### 4. Screenshot Description

**Screenshot 1: GitHub Repository Dashboard**

Include a screenshot of the completed `my-first-project` repository page. The screenshot should clearly show the repository name, the main branch, the `README.md` file, and the **Initial commit** message.

### 5. Troubleshooting

**Common beginner error:** `git is not recognized as an internal or external command` (Windows).

**Possible cause:** Git is not installed, or its installation folder is not included in the computer's `PATH`.

**Solution:** Download and install Git from https://git-scm.com. Close and reopen VS Code, open a new terminal, and run:

```bash
git --version
```

If Git is installed correctly, the terminal displays the installed version number.

### 6. Conclusion

Creating a GitHub repository and making a first commit are useful skills for computing students. Git and GitHub help developers track changes, organize project files, keep a record of their work, and collaborate with other programmers.

# EXERCISE B: API REFERENCE ENTRY

## Create a New Task in a Project Management Application

### 1. Overview

The Create Task API allows an authenticated user to create a new task inside an existing project. The user submits a title, an optional description, an assignee ID, a due date, and a priority level. If the request is valid and the user has permission, the API saves the task and returns its details, including a unique task ID.

### 2. HTTP Method and Endpoint

| Method | Endpoint path | Purpose |
|---|---|---|
| POST | `/v1/projects/{project_id}/tasks` | Create a new task in the specified project. |

The `{project_id}` path placeholder must be replaced with the unique ID of the project.

### 3. Description

This endpoint creates a task in a selected project. The request must include a valid access token. The authenticated user must also have permission to create tasks in that project.

### 4. Request Parameters

#### A. Path Parameters

| Parameter | Data type | Requirement | Description |
|---|---|---|---|
| `project_id` | String (UUID) | Required | Unique ID of the project. |

#### B. Query Parameters

This endpoint does not require query parameters.

#### C. Request Body Parameters

| Parameter | Data type | Requirement | Description |
|---|---|---|---|
| `title` | String | Required | Name of the task. It must not be empty. |
| `description` | String | Optional | Additional information about the task. |
| `assignee_id` | String (UUID) | Required | Unique ID of the assigned user. |
| `due_date` | String (YYYY-MM-DD) | Required | Date by which the task should be completed. |
| `priority` | String (enum) | Required | Accepted values: `low`, `medium`, or `high`. |

### 5. Required Request Headers

| Header | Requirement | Description |
|---|---|---|
| `Authorization` | Required | Bearer access token. |
| `Content-Type` | Required | Identifies JSON request body (`application/json`). |
| `Accept` | Required | Indicates a JSON response (`application/json`). |

Example request headers:

```text
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json
Accept: application/json
```

### 6. Example Request

```text
POST /v1/projects/550e8400-e29b-41d4-a716-446655440000/tasks
```

```json
{
  "title": "Prepare project report",
  "description": "Complete the monthly project progress report.",
  "assignee_id": "usr_10245",
  "due_date": "2026-12-15",
  "priority": "high"
}
```

### 7. Possible HTTP Response Codes

| HTTP code | Status | When it occurs |
|---|---|---|
| 201 | Created | The task was created successfully. |
| 400 | Bad Request | The request contains invalid JSON or is incorrectly formatted. |
| 401 | Unauthorized | The access token is missing, invalid, or expired. |
| 403 | Forbidden | The user lacks permission to create tasks in the project. |
| 404 | Not Found | The project or assignee cannot be found. |
| 409 | Conflict | The request conflicts with an existing resource or project state. |
| 422 | Unprocessable Entity | A value fails validation. |
| 429 | Too Many Requests | The API rate limit was exceeded. |
| 500 | Internal Server Error | An unexpected server error occurred. |
| 503 | Service Unavailable | The API is temporarily unavailable. |

### 8. Example Successful Response

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

### 9. Important Notes

- A valid access token is required for every request.
- The project identified by `project_id` must already exist.
- The assignee must be a valid user who belongs to the project.
- The title is required and must not be empty.
- The priority must be `low`, `medium`, or `high`.
- The due date must use the `YYYY-MM-DD` format.
- The server generates `task_id`, `status`, and `created_at`.
- Example IDs and access tokens must be replaced with valid values when testing.

### 10. Conclusion

The Create Task API provides a consistent way to add tasks to a project management application. A complete API reference helps developers understand how to send requests, authenticate users, provide correct data, and handle responses.

## Scope Note

The supplied lab instructions include Exercises A and B. Exercise C has not been added because its task description was not provided.
