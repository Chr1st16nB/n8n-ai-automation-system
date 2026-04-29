# AI Support Ticket Triage and Auto-Response System (n8n Workflow)

This repository contains an n8n automation workflow designed for hospitality, property management, and SaaS support teams.
It automatically reads support tickets from Google Forms, classifies them with an AI agent, sends personalized customer replies, and logs everything into a support tracker.

This workflow demonstrates practical AI automation using:

n8n

OpenRouter LLM models

Google Sheets

Gmail

No webhooks are required.

## System Architecture

Below is the full visual structure of the workflow:

Main Workflow Diagram


## Features

Fully automated (runs every 5 minutes)

AI-powered classification of:

Category

Priority

Sentiment

Automatic customer email replies

Internal summary generation

JSON schema validation to ensure LLM reliability

Google Sheets integration for ticket input and support logs

Modular design for easy reuse and upgrades

## Workflow Breakdown
### 1. Scheduled Trigger

Polls every 5 minutes for new support tickets.

### 2. Workflow Configuration

Stores static values such as Google Sheet IDs, tab names, and last processed row pointer.

### 3. Read New Support Tickets

Reads new rows from your Google Form responses sheet.

### 4. AI Triage Agent

Sends the customer ticket to an OpenRouter LLM, which returns structured JSON containing:

{
  "category": "",
  "priority": "",
  "sentiment": "",
  "reply_to_customer": "",
  "internal_summary": ""
}


Using Require Specific Output Format, the AI agent returns only valid JSON.

### 5. Structured Output Parser

Ensures the LLM output is valid JSON matching the exact schema required.

### 6. Format Triage Results

Converts the parsed fields into clean, usable variables for email and logging.

### 7. Send Email to Customer

Uses Gmail to send the AI-generated response automatically.

### 8. Log to Support Tracker (Optional)

Writes category, response, priority, and timestamp into a Google Sheet for reporting.

Requirements

n8n Cloud or self-hosted

OpenRouter API Key

Google Sheets and Gmail credentials

Google Form connected to a Sheet

Basic n8n expression knowledge

## Installation

Import the workflow JSON file into n8n

Create credentials for:

Google Sheets

Gmail

OpenRouter

Fill the Workflow Configuration node with:

Support sheet ID

Tracker sheet ID

Sheet tab names

Update Gmail sender email

Activate the workflow

## Folder Structure
/
├── README.md
├── n8n-workflow.json
└── screenshots/
    ├── main-workflow.png
    ├── trigger.png
    ├── config.png
    ├── read-sheet.png
    ├── ai-agent.png
    ├── structured-parser.png
    ├── format-results.png
    ├── send-email.png
    └── log-tracker.png

## Customization Ideas

You can expand the workflow to include:

Slack or WhatsApp notifications

Multi-language customer responses

CRM logging (HubSpot, Salesforce, Notion, Airtable)

Escalation rules for high-priority tickets

Multi-agent processing (classification + verification)