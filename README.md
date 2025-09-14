# ServiceNow Quiz Hub

## Overview
**Quiz Hub** is a custom ServiceNow application that lets you:
- Build and manage **quizzes**.
- Create and import custom **questions & answers**.
- Submit and review **feedback** on questions, automatically updating their state, if necessary.
- Take quizzes through a dedicated **UI Page** that renders questions and evaluates answers in real-time.

---

## Features
- **Import quizzes from JSON** (or use files `csa_practice_quiz.json` and `cad_practice_quiz.json` to get started).
- **Create quizzes manually** using the ServiceNow `Create New Quiz` module.
- **Take a quiz** in the UI, with multi-choice and single-choice question support.
- **Submit feedback** on questions to flag errors or suggest improvements.
- **Automatic state management** of questions when feedback is submitted.

---

## Basic Instruction

1. **Access the App**
   - Navigate in the Application Navigator to **Quiz Hub**.

2. **Import a Quiz**
   - Go to **Import Quiz (JSON)**.
   - Upload a `.json` file that follows the required schema:
     ```json
     {
        "title": "",
        "dev": "QuizHub",
        "date": "08/04/2023",
        "description": "Just a template for creating a JSON file to import a new quiz into Quiz Hub",
        "questions": [
          {
            "prompt": "Question 1?",
            "type": "single",
            "choices": [
              "This is choice #1",
              "Choice #2 here",
              "And #3",
              "And lastly #4"
            ],
            "correct_answers": ["Choice #2 here"],
            "correct_answers_index": [1],
            "explanation": "Explanation of answer goes here"
          },
          {
            "prompt": "What do all of these mean?",
            "type": "multiple",
            "choices": [
              "Type can be either single or multiple. Single means one correct answer, multiple can be 1-6 correct answers.",
              "There must be at least 2 answers listed here in choices, with a max of 6.",
              "correct_answers is the index of the correct answer(s). Remember index starts with zero (0)!",
              "Explanation is the explanation of the answer"
            ],
            "correct_answers": ["There must be at least 2 answers listed here in choices.","correct_answers is the index of the correct answer(s). Remember index starts with zero (0)!"],
            "correct_answers_index": [1, 3],
            "explanation": "By default, cross-scope access is turned on in Table and Workflow"
          }
        ]
      }

     ```

3. **Create a Quiz Manually**
   - Use the **Create New Quiz** module.
   - Add questions via related list entries.

4. **Take a Quiz**
   - Open the **Quiz** module.
   - Select an active quiz to begin answering questions.
   - Submit answers and review explanations.

5. **Give Feedback**
   - Use the **Question Feedback** page/module.
   - Feedback can mark a question as needing deactivation or corrections.

---

## Installation

1. Fork this repo
- Fork this repo by clicking the "Fork" button
<img width="180" height="64" alt="Screenshot 2025-09-14 at 4 40 10 PM" src="https://github.com/user-attachments/assets/19e60ddc-2f05-4e40-b6ca-b0ca6d4d99ac" />

---

2. Create Token and Establish ServiceNow Credentials
- If you aren't familiar with creating a GitHub Token and linking with ServiceNow, you can click [here](#creating-a-github-personal-access-token-pat).

---

3. Open Studio
- Navigate to **System Applications → Studio** in the left-hand navigator.
- In the Studio landing page, click **Import from Source Control**.

---

4. Enter Repository Details
Fill in the following fields:
- **URL**: The HTTPS URL of your forked Git repository (e.g., `https://github.com/your-org/your-app.git`).
- **Credential**: Select or create a Credential record (Basic Auth or Personal Access Token).
- **Branch**: The branch you want to import (defaults to `main` if left blank).
- **Application Name**: Enter a unique name for the application being imported.
- **Scope**: Choose a unique application scope (this is generated automatically if left blank).

---

5. Click "Import"
- Click **Import** to start pulling the application from the repository.
- Studio will:
   - Create a new scoped application.
   - Pull all tracked files (metadata and scripts) from the repository.

---

6. Verify the Application
Once import completes:
- Browse through **Files & Explorer** in Studio to confirm that:
  - Business Rules, Script Includes, UI Actions, etc. are present.
  - Tables and Dictionary records were imported.
- Run the application to ensure no errors are thrown.

---


## Creating a GitHub Personal Access Token (PAT)

When importing from or linking to Source Control in ServiceNow Studio, you often need a **token** instead of your GitHub password. Here’s how to create one securely.

---

### 1. Go to GitHub Settings
1. Sign in to [GitHub](https://github.com/).
2. In the top-right corner, click your **profile picture** → **Settings**.
3. Scroll down the left-hand menu and click **Developer settings** → **Personal access tokens** → **Tokens (classic)**.

---

### 2. Generate a New Token
1. Click **Generate new token** → **Generate new token (classic)**.
2. Give your token a **descriptive name** (e.g., `ServiceNow Studio`).
3. Set **Expiration** to a reasonable period (e.g., 90 days).
4. Under **Select scopes**, check at least:
   - `repo` (Full control of private repositories — required to pull/push code)
   - `read:org` (optional, if your repo is in an organization and requires it)

> For security purposes, **only grant the minimum scopes needed**.  
> `repo` is sufficient for most ServiceNow use cases.

5. Scroll down and click **Generate token**.

---

### 3. Copy and Store Your Token
1. Copy the generated token and save it securely (password manager recommended).
> GitHub will not show it again once you leave the page.

---

### 4. Use the Token in ServiceNow
1. In your ServiceNow instance, go to **System Definition → Credentials** (or **Connections & Credentials → Credentials** depending on version).
2. Create a **Basic Auth Credential**:
   - **Username**: Your GitHub username
   - **Password**: Paste the **PAT** you just generated
3. Save the credential record.

---

### Best Practices
- **Rotate regularly**: Re-generate the token before it expires and update your credential in ServiceNow.
- **Limit scope**: Don’t select unnecessary permissions unless required by your workflow.
- **Revoke tokens when no longer needed**: Go back to **Developer settings** → **Personal access tokens** and delete old ones.

---

### Tips

- **Credentials**: If you don’t have a Credential record yet, create one under **System Definition → Credentials** before importing.
- **Branch Switching**: After import, you can use **Link to Source Control** in Studio to pull updates, switch branches, or commit changes back.
- **Conflicts**: If importing into an instance that already has an app with the same scope, you may need to rename the scope or delete the existing one first.

---

### Troubleshooting

- **Authentication Failed**: Double-check the repository URL and credential.
- **Scope Conflict**: Ensure the application scope is unique in your instance.
- **Partial Import**: Verify the branch contains a valid `sys_app` record and all required metadata files.

---

### References

- [ServiceNow Docs: Import from Source Control](https://developer.servicenow.com/dev.do#!/learn/learning-plans/tokyo/app_store_learnv2_sourcecontrol_tokyo_importing_from_source_control)
- [Studio Overview](https://docs.servicenow.com/bundle/tokyo-application-development/page/build/applications/concept/c_StudioOverview.html)


