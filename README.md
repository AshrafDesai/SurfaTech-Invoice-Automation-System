# SurfaTech Invoice Automation System

A Google Workspace-based invoice automation system built using **Google Forms, Google Sheets, and Google Apps Script** to simplify customer data collection, invoice numbering, calculations, and invoice generation.

## 📌 Project Overview

The system automates the initial stages of invoice creation by collecting customer and product details through a Google Form and processing the submitted data using Google Sheets and Google Apps Script.

### Workflow

```text
Customer / Staff
       │
       ▼
 Google Form
       │
       ▼
 Google Sheets
       │
       ▼
 Google Apps Script
       │
       ├── Invoice Number Generation
       ├── Product Amount Calculation
       ├── Subtotal Calculation
       ├── GST Calculation
       └── Grand Total Calculation
       │
       ▼
 Invoice Template
       │
       ▼
 PDF Invoice
       │
       ├── Google Drive
       └── Email
