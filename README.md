# IntelliHub — AI-Assisted Fraud Investigation Platform

IntelliHub is an **AI-assisted fraud investigation and knowledge management platform** developed as a FinTech Hackathon prototype.

The platform helps support and investigation teams manage fraud cases, search internal knowledge, analyse operational information, and retrieve relevant information through an AI-assisted chatbot. It combines fraud case management with internal cases, policies, transactions, and company documents while maintaining **role-based access control** for Staff and Manager users.

---

## Screenshots

### Dashboard

Provides an overview of fraud cases, transaction activities, case trends, and key operational information.

<img width="1917" height="862" alt="IntelliHub Dashboard" src="https://github.com/user-attachments/assets/7ec13f7f-a1cb-410e-b5e9-77820cdec0e8" />

### Knowledge Search

Allows users to search and retrieve relevant information from internal cases, policies, transactions, and company documents.

<img width="1917" height="862" alt="IntelliHub Knowledge Search" src="https://github.com/user-attachments/assets/d0f951f8-2970-4ea7-a050-14bd59d78fc0" />

### AI-Assisted Chatbot

Provides AI-assisted responses based on retrieved internal information to support fraud investigation and decision-making.

<img width="1917" height="862" alt="IntelliHub AI Chatbot" src="https://github.com/user-attachments/assets/4dd748fe-b434-47c8-85b0-617d3e0cc785" />

### Login

Role-based login interface for Staff and Manager users.

<img width="1917" height="866" alt="IntelliHub Login" src="https://github.com/user-attachments/assets/d6e88464-2815-42e6-b57c-37dd56388e8b" />

---

## Key Features

### Fraud Case Management

* Browse and review fraud cases
* View individual case details
* Review related transaction information
* Access relevant policies and internal documents
* Search internal knowledge sources

### AI-Assisted Chatbot

* Answers fraud investigation and internal procedure questions
* Retrieves relevant internal information before generating responses
* Uses cases, policies, transactions, and internal documents as context
* Provides references to retrieved information

### Knowledge Search

* Search across fraud cases
* Search company policies
* Search transaction records
* Search extracted internal documents
* Permission-aware search results based on user roles

### Role-Based Access Control

* Separate Staff and Manager access
* Restricted information is filtered during retrieval
* Manager-only access to selected documents and features
* Process Insights is restricted to Manager users

### Process Insights

* Identifies repeated case patterns
* Highlights potential automation opportunities
* Identifies process improvement opportunities
* Highlights policy coverage gaps

### Analysis & Reports

* Review fraud-related operational information
* Generate reports
* Export reports as PDF
* Export reports as Excel

---

## My Contributions

My primary contribution to IntelliHub focused on the **frontend and user interface (UI)** of the prototype. I worked on translating the team's ideas and system requirements into a functional and easy-to-understand interface for Staff and Manager users.

My contributions included:

* **Dashboard UI** — Worked on the dashboard interface and presentation of key information to provide users with a clear overview of the system.

* **Knowledge Search Interface** — Worked on the Knowledge Search feature, including the frontend search interaction and presentation of retrieved internal information.

* **Login Interface** — Contributed to parts of the login page and authentication-related user flow.

* **UI/UX Development** — Focused mainly on the overall interface design, page layouts, navigation, visual consistency, and usability across the prototype.

* **Frontend Integration** — Helped connect frontend components with the project's backend functions and data to ensure that key prototype features could be demonstrated during the hackathon.

Through this project, I gained practical experience in **rapid prototyping, frontend development, UI/UX design, teamwork, problem-solving, time management, and integrating different system components under hackathon time constraints**.

---

## Project Background

IntelliHub was originally developed collaboratively as a **team project for a FinTech Hackathon**, where our team successfully advanced to the **finalist stage**.

The project explores how AI-assisted knowledge retrieval can support fraud investigation, case management, internal knowledge access, and operational decision-making in a FinTech environment.

**Original Team Repository:**
https://github.com/LYYGG22/TehCBeng

This repository is maintained as my **personal portfolio copy** of the project to showcase my experience and individual contributions during the hackathon.

> **Note:** IntelliHub was developed collaboratively by the hackathon team. The features described in this repository represent the team's overall solution, while the **My Contributions** section highlights my individual areas of contribution.

---

# Getting Started

## Prerequisites

Before running the project, make sure you have:

* **PHP 8.0+** with the `pdo_sqlite` extension enabled
* **Composer**
* A modern web browser
* Internet access for AI chatbot model requests and external CDN resources
* An **OpenRouter API key** for the chatbot

---

## Installation

### 1. Install Dependencies

From the project directory, run:

```bash
composer install
```

This installs the PHP libraries required to process PDF, Word, and Excel documents.

### 2. Configure the API Key

Create your local environment file:

```bash
cp .env.example .env
```

For Windows PowerShell:

```powershell
Copy-Item .env.example .env
```

Open the newly created `.env` file and add your own OpenRouter API key:

```env
OPENROUTER_API_KEY=your_openrouter_api_key_here
```

> **Important:** The `.env` file is excluded from Git through `.gitignore`, so your actual API key will not be uploaded to the repository. Never place a real API key inside `.env.example`.

The `.env.example` file is provided only as a configuration template.

If an API key is not configured, the chatbot will return:

```text
OPENROUTER_API_KEY is not set
```

---

## Database Setup

The database is created automatically when the application runs for the first time.

`Logic/db.php` creates the SQLite database at:

```text
Data/app.db
```

It also creates the required tables and loads the initial data from the JSON files stored inside the `Data/` directory.

No manual database migration is required.

---

## Run the Application

From the repository root:

```bash
php -S localhost:8000
```

Then open:

```text
http://localhost:8000/Interface/login.html
```

Alternatively, the project can be placed inside an XAMPP `htdocs` directory and accessed through localhost.

---

## Demo Accounts

| Role    | Email                                                   | Password   |
| ------- | ------------------------------------------------------- | ---------- |
| Manager | [manager@intellihub.com](mailto:manager@intellihub.com) | manager123 |
| Staff   | [staff@intellihub.com](mailto:staff@intellihub.com)     | staff123   |

Manager and Staff accounts have different access permissions.

For example, **Process Insights** is available only to Manager users.

---

# What to Try

### 1. Explore Fraud Cases

Log in as **Staff**, browse the available fraud cases, and open an individual case to review its information.

### 2. Test the Knowledge Search

Search for information across internal cases, policies, transactions, and company documents.

### 3. Ask the AI Chatbot

Try asking:

```text
How do we handle account takeover?
```

The chatbot retrieves relevant internal information before generating its response.

### 4. Explore Manager Features

Log in using the **Manager** account and open **Process Insights** to view repeated case patterns, automation opportunities, and policy coverage gaps.

### 5. Generate Reports

Visit the **Analysis & Report** page and export a report as either:

* PDF
* Excel

### 6. Test Role-Based Permissions

Some internal documents are restricted to specific roles.

For example:

```text
Data/Documents/device_verification_guide.docx
```

contains Manager-level information.

When Staff and Manager users perform searches involving restricted information, the results are filtered according to their access permissions.

---

# System Architecture

## Project Structure

```text
Interface/
    Frontend pages and user interface components.

    Includes:
    dashboard.php
    cases.php
    reports.php
    knowledge.php

    Shared UI:
    Interface/partials/

    JavaScript and CSS:
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
    System data sources.

    Includes:
    fraud_cases.json
    policies.json
    transactions.json
    documents_cache.json

    Internal documents:
    Data/Documents/


vendor/
    Composer dependencies.
    This directory is excluded from Git.
```

IntelliHub currently uses a **multi-page PHP architecture**, where individual pages are loaded separately during navigation.

An earlier single-page prototype using `dashboard.html` and `assets/app.js` may also exist in the repository, but it is not part of the primary application flow.

---

# Data Flow

JSON files inside the `Data/` directory act as editable source data.

Examples include:

```text
Data/fraud_cases.json
Data/policies.json
Data/transactions.json
```

On application requests, `Logic/db.php` synchronizes this information with the SQLite database.

This allows developers to update the JSON datasets without manually rebuilding the database.

---

## Document Processing

Internal documents are stored inside:

```text
Data/Documents/
```

Supported document types include:

* PDF
* Word documents
* Excel spreadsheets

These files must first be converted into searchable text.

Run:

```bash
php Logic/extract_documents.php
```

The extraction process uses document-processing libraries to convert the files into text and stores the results inside:

```text
Data/documents_cache.json
```

The extracted information can then be used by:

* Knowledge Search
* AI chatbot retrieval
* Document viewing
* Permission-aware search

If a document is added or modified, the extraction script should be run again.

---

# Permission-Aware Retrieval

Cases, policies, transactions, and documents can contain an:

```text
access_level
```

field.

For example:

```json
{
  "access_level": "manager"
}
```

If no access level is specified, the record can be available to all authorized users.

`Logic/retrieve_data.php` checks the logged-in user's role before returning restricted information.

This means access control is enforced during the **retrieval process**, rather than relying only on frontend visibility.

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

Relevant results are filtered according to the logged-in user's role.

The retrieved information is then provided as context to an AI model through OpenRouter.

The chatbot generates an answer based on the retrieved internal information rather than relying only on general model knowledge.

This lightweight retrieval approach was selected because the prototype uses a relatively small dataset and does not require a full vector database or embedding infrastructure.

---

# Report Export

The Analysis & Report page supports **PDF and Excel export**.

The export functionality is handled mainly through:

```text
Interface/assets/pages/reports.js
```

PDF reports are generated directly in the browser, while Excel-compatible files are generated using SpreadsheetML XML.

No additional server request is required during export.

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

# Dependencies

| Package                    | Purpose                                                    |
| -------------------------- | ---------------------------------------------------------- |
| `smalot/pdfparser`         | Extract text from PDF documents                            |
| `phpoffice/phpword`        | Extract text from Word `.docx` documents                   |
| `phpoffice/phpspreadsheet` | Extract data from Excel `.xlsx` documents                  |
| `marked.js`                | Render Markdown-formatted chatbot responses in the browser |

---

# Security Notes

* API keys should never be committed to the repository.
* Real API credentials should only be stored inside `.env`.
* `.env` is excluded through `.gitignore`.
* `.env.example` contains only configuration placeholders.
* Role-based access restrictions are enforced during data retrieval.
