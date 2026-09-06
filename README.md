# Project Background

IntelliHub was originally developed collaboratively as a team project for a **FinTech Hackathon**, where our team successfully advanced to the **finalist stage**.

The project focuses on using AI-assisted knowledge retrieval to support fraud investigation, case management, and internal decision-making in a FinTech environment.

**Original Team Repository**:
https://github.com/LYYGG22/TehCBeng

This repository is maintained as my personal portfolio copy of the project for showcasing my experience and contributions during the hackathon.

---

## My Contributions

My primary contribution to IntelliHub focused on the frontend and user interface (UI) of the prototype. I worked on translating the team's ideas and system requirements into a functional and easy-to-understand interface for staff and managers.

My contributions included:

**Dashboard UI** — Worked on the dashboard interface and presentation of key information to provide users with a clear overview of the system.
**Knowledge Search Interface** — Worked on the Knowledge Search feature, including the frontend search interaction and presentation of retrieved internal information.
**Login Interface** — Contributed to parts of the login page and authentication-related user flow.
**UI/UX Development** — Focused mainly on the overall interface design, page layouts, navigation, visual consistency, and usability across the prototype.
**Frontend Integration** — Helped connect frontend components with the project's backend functions and data to ensure that key prototype features could be demonstrated during the hackathon.

Through this project, I gained practical experience in **rapid prototyping, frontend development, UI/UX design, teamwork, problem-solving, and integrating different system components under hackathon time constraints**.

**Note**: IntelliHub was developed collaboratively by the hackathon team. The features described in this repository represent the team's overall solution, while the section above highlights my individual areas of contribution.

---

## Quick Start

### Prerequisites

* **PHP 8.0+** with the `pdo_sqlite` extension enabled
* **Composer**
* A modern web browser
* Internet access for AI chatbot model requests and external CDN resources
* An **OpenRouter API key** for the chatbot

---

### Setup

Install the required PHP dependencies:

```bash
composer install
```

This installs the libraries used to process PDF, Word, and Excel documents.

Next, create your local environment file:

```bash
cp .env.example .env
```

For Windows PowerShell, you can use:

```powershell
Copy-Item .env.example .env
```

Open the newly created `.env` file and add your own OpenRouter API key:

```env
OPENROUTER_API_KEY=your_openrouter_api_key_here
```

You can obtain an API key from OpenRouter.

> **Important:**
> The `.env` file is excluded from Git through `.gitignore`, so your actual API key will not be uploaded to the repository.
> Do not place a real API key inside `.env.example`.

The `.env.example` file is provided only as a configuration template.

If the API key is not configured, the chatbot will return:

```text
OPENROUTER_API_KEY is not set
```

---

### Database Setup

The database is created automatically when the application runs for the first time.

`Logic/db.php` creates the SQLite database at:

```text
Data/app.db
```

It also creates the required tables and loads initial data from the JSON files stored inside the `Data/` directory.

No manual database migration is required.

---

## Run the Application

From the repository root, run:

```bash
php -S localhost:8000
```

Then open:

```text
http://localhost:8000/Interface/login.html
```

Alternatively, the project can also be placed inside an XAMPP `htdocs` directory and accessed through localhost.

---

## Demo Accounts

| Role    | Email                                                   | Password   |
| ------- | ------------------------------------------------------- | ---------- |
| Manager | [manager@intellihub.com](mailto:manager@intellihub.com) | manager123 |
| Staff   | [staff@intellihub.com](mailto:staff@intellihub.com)     | staff123   |

Manager and Staff accounts have different access permissions.

For example, **Process Insights** is available only to Manager users.

---

## Features to Try

### 1. Fraud Case Management

Log in as Staff and browse fraud cases.

Users can:

* View fraud cases
* Open individual case details
* Review transaction information
* View related policies and documents
* Search internal knowledge sources

---

### 2. AI-Assisted Chatbot

Ask the chatbot questions related to fraud investigation or internal procedures.

Example:

```text
How do we handle account takeover?
```

The chatbot retrieves relevant internal information before generating its answer and provides references to the sources used.

---

### 3. Knowledge Search

The Knowledge Search feature allows users to search through:

* Fraud cases
* Policies
* Transactions
* Internal documents

Search results are filtered according to the user's access level.

---

### 4. Manager Process Insights

Log in using the Manager account and open:

```text
Process Insights
```

This section provides information such as:

* Potential automation opportunities
* Repeated case patterns
* Process improvement opportunities
* Policy coverage gaps

This feature is restricted to Manager users.

---

### 5. Analysis & Reports

The Analysis & Report page allows users to review fraud-related information and generate reports.

Reports can be exported as:

* **PDF**
* **Excel**

The export process is handled directly in the browser.

---

### 6. Role-Based Permission Testing

Some internal documents are restricted to specific user roles.

For example:

```text
Data/Documents/device_verification_guide.docx
```

contains Manager-level information.

When Staff and Manager users perform the same search, restricted information is filtered according to their permissions.

This allows the system to enforce access control before information reaches the AI chatbot.

---

# Architecture

## Project Structure

```text
Interface/
    Frontend pages and user interface components.

    Includes individual PHP pages such as:
    dashboard.php
    cases.php
    reports.php
    knowledge.php

    Shared UI components are stored in:
    Interface/partials/

    JavaScript and CSS files are stored in:
    Interface/assets/


Logic/
    Backend PHP logic.

    Includes:
    auth.php
    data.php
    chatbot.php
    document.php
    case_actions.php
    db.php
    retrieve_data.php


Data/
    Contains the system data sources.

    Includes:
    fraud_cases.json
    policies.json
    transactions.json
    documents_cache.json

    Internal documents are stored in:
    Data/Documents/


vendor/
    Composer dependencies.

    This directory is excluded from Git.
```

IntelliHub currently uses a **multi-page PHP architecture** where individual pages are loaded separately during navigation.

An earlier single-page prototype using `dashboard.html` and `assets/app.js` may also exist in the repository but is not part of the primary application flow.

---

# Data Flow

JSON files inside the `Data/` directory act as editable source data.

For example:

```text
Data/fraud_cases.json
Data/policies.json
Data/transactions.json
```

On application requests, `Logic/db.php` synchronizes this information with the SQLite database.

This allows developers to update the JSON datasets without manually rebuilding the database.

---

## Document Processing

Documents stored in:

```text
Data/Documents/
```

can include:

* PDF
* Word documents
* Excel spreadsheets

These files must first be converted into searchable text.

Run:

```bash
php Logic/extract_documents.php
```

The extraction process uses document-processing libraries to convert the files into text and saves the results inside:

```text
Data/documents_cache.json
```

The resulting text can then be used by:

* Knowledge Search
* AI chatbot retrieval
* Document viewing
* Permission-aware search

If a document is added or modified, the extraction script should be run again.

---

# Permission-Aware Retrieval

Records such as cases, policies, transactions, and documents can contain an:

```text
access_level
```

field.

Example:

```json
{
  "access_level": "manager"
}
```

If no access level is specified, the record can be available to all authorized users.

`Logic/retrieve_data.php` checks the user's role before returning restricted information.

This means access control is enforced during the retrieval process rather than relying only on frontend visibility.

Restricted information therefore does not enter the chatbot's context for unauthorized users.

For extracted documents, the system can also detect markers such as:

```text
Access: Manager
```

and convert them into the corresponding access-control level.

---

# AI Chatbot

The AI chatbot is implemented mainly through:

```text
Logic/chatbot.php
Logic/retrieve_data.php
```

The system performs lightweight keyword-based retrieval across:

* Fraud cases
* Policies
* Transactions
* Internal documents

Relevant results are filtered based on the logged-in user's role.

The retrieved information is then provided as context to an AI model through OpenRouter.

The chatbot generates an answer based on this retrieved information rather than relying only on general model knowledge.

This lightweight retrieval approach was selected because the prototype uses a relatively small dataset and does not require a full vector database or embedding infrastructure.

---

# Report Export

The Analysis & Report page supports PDF and Excel export.

The export functionality is handled mainly through:

```text
Interface/assets/pages/reports.js
```

PDF reports are generated directly in the browser, while Excel-compatible files are generated using SpreadsheetML XML.

No additional server request is required during export.

---

# Dependencies

| Package                    | Purpose                                                    |
| -------------------------- | ---------------------------------------------------------- |
| `smalot/pdfparser`         | Extract text from PDF documents                            |
| `phpoffice/phpword`        | Extract text from Word `.docx` documents                   |
| `phpoffice/phpspreadsheet` | Extract data from Excel `.xlsx` documents                  |
| `marked.js`                | Render Markdown-formatted chatbot responses in the browser |

---

# Technologies Used

* PHP
* JavaScript
* HTML
* CSS
* SQLite
* JSON
* OpenRouter API
* Composer
* RAG-style information retrieval

---

# Project Background

IntelliHub was developed as a **FinTech Hackathon prototype** focused on improving fraud investigation, internal knowledge retrieval, and operational decision-making.

The project explores how AI can assist support and investigation teams by combining internal organizational knowledge with fraud case information while maintaining role-based information access.

This repository is maintained as a portfolio version of the hackathon project.

---

# Security Notes

* API keys should never be committed to the repository.
* Real API credentials should only be stored inside `.env`.
* `.env` is excluded through `.gitignore`.
* `.env.example` contains only configuration placeholders.
* Role-based access restrictions are enforced during data retrieval.
