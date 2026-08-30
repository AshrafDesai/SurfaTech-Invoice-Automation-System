# SurfaTech Invoice Automation System

<img width="1983" height="793" alt="image" src="https://github.com/user-attachments/assets/ed8bff62-d5dc-44ab-9dc2-2daf08765189" />


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
```

## ✨ Features

* Customer information collection
* Company and billing information collection
* GSTIN collection
* Multiple product entries
* Quantity and unit-price input
* Automatic invoice numbering
* Financial-year based invoice numbering
* Product amount calculation
* Subtotal calculation
* GST calculation
* Grand-total calculation
* Google Apps Script automation
* Automated invoice generation architecture
* PDF generation and email delivery planned

## 🔢 Invoice Number Format

The invoice number follows this format:

`SIS/2026-27/0023`

### Format

`SIS / Financial Year / Invoice Sequence`

| Component | Description                          |
| --------- | ------------------------------------ |
| `SIS`     | SurfaTech identifier                 |
| `2026-27` | Current financial year               |
| `0023`    | Four-digit sequential invoice number |

For example:

```text
SIS/2026-27/0023
SIS/2026-27/0024
SIS/2026-27/0025
```

If the current invoice is:

`SIS/2026-27/0023`

the next invoice will be:

`SIS/2026-27/0024`

## 📝 Google Form

The Google Form is used to collect the information required for creating an invoice.

### Customer Details

* Customer Name
* Company Name
* Billing Address
* Phone Number
* Email
* GSTIN

### Product Details

The current form structure supports multiple products.

Each product contains:

* Product Name
* Quantity
* Unit Price
* Amount

Example:

```text
Product 1
Quantity: 10
Unit Price: ₹500
Amount: ₹5,000

Product 2
Quantity: 5
Unit Price: ₹300
Amount: ₹1,500
```

## 📊 Google Sheets

Google Sheets acts as the database and processing layer.

The workflow uses the Google Form response sheet for raw submissions and a separate processing structure for invoice-related calculations.

### Processing Structure

```text
Customer Information
        │
        ▼
Product Information
        │
        ▼
Quantity × Unit Price
        │
        ▼
Product Amount
        │
        ▼
Subtotal
        │
        ▼
GST
        │
        ▼
Grand Total
```

## ⚙️ Google Apps Script

Google Apps Script is used to automate the invoice workflow.

The primary trigger is:

`onFormSubmit`

The trigger is configured as:

```text
Event Source: From spreadsheet
Event Type: On form submit
```

When a form is submitted, the script processes the new response automatically.

### Basic Invoice Number Logic

```javascript
const financialYear = "2026-27";
const lastInvoiceNumber = 23;

const nextNumber = lastInvoiceNumber + 1;

const invoiceNumber =
  "SIS/" +
  financialYear +
  "/" +
  String(nextNumber).padStart(4, "0");
```

Output:

```text
SIS/2026-27/0024
```

## 💰 Invoice Calculation

The basic calculation logic is:

```text
Product Amount = Quantity × Unit Price
```

```text
Subtotal = Sum of Product Amounts
```

```text
GST Amount = Subtotal × GST Rate / 100
```

```text
Grand Total = Subtotal + GST Amount
```

### Example

```text
Product 1:
10 × ₹500 = ₹5,000

Product 2:
5 × ₹300 = ₹1,500
```

Therefore:

```text
Subtotal = ₹6,500
GST @ 18% = ₹1,170

Grand Total = ₹7,670
```

## 🏗️ Architecture

```text
┌─────────────────────┐
│   Customer / Staff  │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│    Google Form      │
│                     │
│ Customer Details    │
│ Product Details     │
│ Quantity / Price    │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│    Google Sheets    │
│                     │
│ Form Responses      │
│ Invoice Data        │
│ Calculations        │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│ Google Apps Script  │
│                     │
│ onFormSubmit        │
│ Invoice Number      │
│ Calculations        │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│  Invoice Template   │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│    PDF Invoice      │
└──────────┬──────────┘
           │
      ┌────┴────┐
      ▼         ▼
┌──────────┐ ┌──────────┐
│  Drive   │ │  Email   │
└──────────┘ └──────────┘
```

## 📁 Repository Structure

```text
SurfaTech-Invoice-Automation/
│
├── README.md
│
├── Apps-Script/
│   └── Code.gs
│
├── Documentation/
│   └── Project-Report.pdf
│
├── Invoice-Template/
│   └── invoice-template
│
├── Screenshots/
│   ├── google-form.png
│   ├── google-sheet.png
│   ├── apps-script.png
│   └── architecture.png
│
└── LICENSE
```

## 🔐 Security Considerations

The system handles customer and invoice information, so access should be properly restricted.

Recommended practices:

* Keep Google Sheets private.
* Give access only to authorized users.
* Do not upload customer information to GitHub.
* Do not commit API keys, credentials, or tokens.
* Store generated invoices in a controlled Google Drive folder.
* Restrict Apps Script project access.
* Maintain backups of finalized invoices.
* Implement concurrency protection for invoice-number generation.

## 🧪 Testing

The system was tested during development using sample invoice data.

Example:

```text
Previous Invoice:
SIS/2026-27/0023

Expected Next Invoice:
SIS/2026-27/0024
```

The `onFormSubmit` trigger was also configured to execute the automation whenever a new form response is submitted.

## ✅ Current Status

### Completed

* [x] Google Form created
* [x] Customer details fields created
* [x] Product fields created
* [x] Google Sheet connected
* [x] Invoice data structure created
* [x] Invoice number format implemented
* [x] Invoice number generation tested
* [x] `onFormSubmit` trigger configured
* [x] Architecture designed
* [x] Project documentation created

### Planned

* [ ] Complete automated product calculations
* [ ] Complete automated GST calculations
* [ ] Complete automated grand-total calculations
* [ ] Professional invoice template
* [ ] Automatic PDF generation
* [ ] Google Drive invoice storage
* [ ] Automatic email delivery
* [ ] Product master/pricing sheet
* [ ] Automatic financial-year rollover
* [ ] Duplicate invoice prevention
* [ ] Invoice dashboard
* [ ] Invoice status tracking

## 🗺️ Future Workflow

The final version of the system is planned to follow:

```text
Google Form
     │
     ▼
Form Response
     │
     ▼
Apps Script Trigger
     │
     ├── Validate Data
     ├── Generate Invoice Number
     ├── Calculate Amounts
     ├── Calculate GST
     └── Calculate Total
     │
     ▼
Invoice Template
     │
     ▼
Generate PDF
     │
     ├── Save to Google Drive
     │
     └── Send to Customer
```

## 🎯 Project Objective

The objective of this project is to create a **simple, reliable, and automated invoice-generation workflow** for SurfaTech Integrated Solutions using existing Google Workspace tools.

The system provides a foundation that can be expanded into a complete invoice-management solution without requiring a separate backend application.

## 👨‍💻 Author

**Ashrafraza Desai**

Computer Science Engineering
Cybersecurity | Data Engineering | DevOps

## 📜 License

This project is intended for business-process automation and development purposes.

Add an appropriate open-source or private license before publishing the repository publicly.
