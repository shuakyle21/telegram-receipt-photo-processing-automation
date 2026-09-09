# Telegram Receipt Processor

## Overview

An n8n workflow that automatically processes receipt photos sent through Telegram.

The workflow uses Google Gemini to extract receipt details, saves the original photo to Google Drive by submission date, and logs the extracted information with a Drive link in Google Sheets.

## Workflow

```mermaid
graph TD;
    A[Telegram<br/>Receive Receipt Photo] --> B[Add Submission Date];
    A --> C[Preserve Photo Binary];
    B --> D[Gemini Vision<br/>Extract Receipt Details];
    D --> E[Parse Receipt JSON];
    E --> F[Find Date Folder];
    F --> G{Folder Exists?};
    G -->|Yes| H[Use Existing Folder];
    G -->|No| I[Create Date Folder];
    H --> J[Combine Photo + Folder];
    I --> J;
    C --> J;
    J --> K[Save Photo to Google Drive];
    K --> L[Log to Google Sheets];
```

## Features

- Telegram receipt photo processing
- Gemini Vision receipt extraction
- Merchant, amount, and receipt date extraction
- Automatic Google Drive archiving
- Date-based folder organization
- Google Sheets logging
- Direct Google Drive file link
- Retry handling for Google Sheets writes

## Archive Structure

```text
Receipts/
└── <submission-date>/
    └── receipt_<timestamp>.jpg
```

### Example

```text
Receipts/
└── 2026-09-06/
    └── receipt_20260906_003510.jpg
```

## Tech Stack

[![n8n](https://img.shields.io/badge/n8n-EA4B71?style=for-the-badge&logo=n8n&logoColor=white)](https://n8n.io/)
[![Telegram](https://img.shields.io/badge/Telegram-26A5E4?style=for-the-badge&logo=telegram&logoColor=white)](https://telegram.org/)
[![Google Gemini](https://img.shields.io/badge/Google%20Gemini-4285F4?style=for-the-badge&logo=googlegemini&logoColor=white)](https://ai.google.dev/)
[![Google Drive](https://img.shields.io/badge/Google%20Drive-4285F4?style=for-the-badge&logo=googledrive&logoColor=white)](https://drive.google.com/)
[![Google Sheets](https://img.shields.io/badge/Google%20Sheets-34A853?style=for-the-badge&logo=googlesheets&logoColor=white)](https://sheets.google.com/)
[![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)](https://developer.mozilla.org/en-US/docs/Web/JavaScript)