# ServiceNow Quiz Hub

## Overview
**Quiz Hub** is a custom ServiceNow application that lets you:
- Build and manage **quizzes** (title, description, state).
- Create and import **questions** (1–6 answer choices, explanation, correct answer(s)).
- Collect and review **feedback** on questions, automatically updating their state with Business Rules.
- Take quizzes through a dedicated **UI Page** that renders questions and evaluates answers in real-time.

The app is scoped as `x_274343_quiz_hub`.

---

## Features
- **Import quizzes from JSON** (see sample files `csa_quiz_data.json` and `cad_quiz_data.json`).
- **Create quizzes manually** via ServiceNow modules.
- **Take a quiz** in the UI, with multi-choice and single-choice support.
- **Submit feedback** on questions to flag errors or suggest improvements.
- **Automatic state management** of questions when feedback is submitted.
- **Role-based access** with ACLs to control who can create, edit, or take quizzes.

---

## How to Use

1. **Access the App**
   - Navigate in the Application Navigator to **Quiz Hub**.

2. **Import a Quiz**
   - Go to **Import Quiz (JSON)**.
   - Upload a `.json` file that follows the required schema:
     ```json
     {
       "title": "CSA Practice Quiz",
       "description": "Sample questions for CSA exam",
       "questions": [
         {
           "prompt": "What is a schema map?",
           "type": "single",
           "choices": [
             "JavaScript configured to run on record events",
             "UI control to add columns to a list",
             "Graphical representation of table relationships"
           ],
           "correct_answers": [
             "Graphical representation of table relationships"
           ],
           "correct_answers_index": [2],
           "explanation": "Schema maps show referenced/referencing and extended/parent table relationships."
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

### 1. Clone / Download
If working locally with GitHub:
```bash
git clone https://github.com/<your-org>/ServiceNowQuizHub.git

