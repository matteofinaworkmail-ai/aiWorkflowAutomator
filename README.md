# aiWorkflowAutomator# AI Workflow Automator

A lightweight workflow automation system for processing emails, documents and files using Azure Functions and Azure OpenAI.  
The goal is to provide SMEs with a simple way to extract structured information from unstructured inputs and trigger follow-up actions without writing code.

---

## Project Goal

This project aims to:

- Ingest input from email, files or API requests  
- Use Azure OpenAI models to extract structured data from PDFs, images or text  
- Validate and normalize the AI output  
- Trigger follow-up workflow steps (webhooks, API calls, storage writes, etc.)  
- Provide a foundation for building custom automations for small and medium businesses  

The project starts with a minimal MVP and expands incrementally.

---

## Current Features (MVP)

- Receive documents via HTTP upload or URL
- AI-based extraction using Azure OpenAI (GPT-4o mini / GPT-4o)
- Normalized JSON output
- Automatic saving to Azure Blob Storage
- Minimal API for testing and integration

---

## Technologies Used

- **Azure Functions** (HTTP Trigger, Queue Trigger in future)
- **Azure OpenAI**
- **Azure Blob Storage**
- **.NET 8** (backend)
- **Node.js / Next.js** (optional UI layer)
- **Docker** (planned)
- **Bicep** (Infrastructure as Code, planned)

---

## Architecture (Initial MVP)

Input (Email / File / API)
↓
Azure Function (HTTP Trigger)
↓
AI Extraction Layer (Azure OpenAI)
↓
Validation / Normalization
↓
Output (Blob Storage / Webhook / API)


The first version focuses on the extraction pipeline.  
Workflow actions and UI will be added step by step.

---

## Getting Started (Development)

### 1. Requirements
- .NET 8 SDK  
- Node.js 18+ (if using the UI)  
- Azure CLI installed  
- Azure subscription with:
  - Resource Group
  - Storage Account
  - Azure OpenAI resource

---

### 2. Clone the repository

```bash
git clone https://github.com/<your-username>/ai-workflow-automator.git
cd ai-workflow-automator


## Start the backend (Azure Functions)

cd backend
func start

## Start the frontend (optional)

cd frontend
npm install
npm run dev

### API 

## Example Request 
POST /api/extract
Content-Type: application/json

{
  "fileUrl": "https://.../invoice.pdf",
  "extractType": "invoice"
}

## Example Response

{
  "status": "ok",
  "fields": {
    "invoiceNumber": "RB-2025-143",
    "date": "2025-01-12",
    "amount": 1290.50
  }
}

