# AI Lead Qualifier

AI-powered lead qualification and routing workflow built with n8n.

The system receives an incoming lead through a webhook, uses an AI agent to analyze the request, stores the structured lead data, routes the lead by priority, and sends a notification to a manager via Telegram.

It also includes an automated error-handling workflow that sends an alert when the main workflow fails.

## Business Problem

Businesses often receive leads from websites, forms, messaging apps, or other channels. Manually reviewing every lead can be slow and inconsistent, and high-priority requests can be missed.

This workflow automates the first stage of lead processing:

- receive the lead
- understand what the customer needs
- classify the request
- assign a priority
- store the lead
- notify the manager
- alert the manager if the automation itself fails

## Workflow Architecture

```text
Incoming Lead
     |
     v
Lead Intake (Webhook)
     |
     v
Prepare Lead
     |
     v
Qualify Lead (AI Agent)
     |
     v
Structured Output Parser
     |
     v
Save Lead (Data Table)
     |
     v
Check High Priority
   /          \
 Yes           No
 |              |
 v              v
Telegram     Check Medium
               /       \
            Yes         No
             |           |
             v           v
          Telegram    Telegram
Error Handling

Main Workflow
     |
   Error
     |
     v
AI Lead Qualifier - Error Handler
     |
     v
Error Trigger
     |
     v
Telegram Alert

What the AI Produces
For each lead, the AI extracts:
- Name
- Company
- Email
- Need
- Category
- Priority: Low, Medium, or High
- Summary
The AI is instructed not to invent information that is not present in the incoming lead.
Example
Incoming lead
We receive around 50-100 customer inquiries every day. Our team currently processes them manually, and some leads are getting lost. We need an automated system that can collect incoming leads, classify them by priority, and notify our sales manager about urgent requests.

AI result
- Priority: High
- Category: Lead management automation
- Need: Automated lead-management system
- Summary: The company receives a high volume of inquiries and wants to automate lead collection, prioritization, and urgent-request notifications.
The High Priority branch then sends the lead information to Telegram.
Main Components
Component	Purpose
Webhook	Receives incoming lead data
Edit Fields	Prepares the lead data for AI processing
AI Agent	Analyzes and qualifies the lead
Structured Output Parser	Forces the AI response into a predictable structure
Data Table	Stores qualified leads
IF nodes	Routes leads by priority
Telegram	Notifies the manager
Error Trigger	Starts the error-handling workflow when the main workflow fails


Testing
The workflow was tested using the n8n Production Webhook.
Tested scenarios include:
- High-priority lead
- Medium-priority lead
- Low-priority lead
- Successful production execution
- Deliberate workflow failure
- Automatic error workflow execution
- Telegram error notification
- Data storage in the lead table
Tech Stack
- n8n
- OpenAI
- Telegram Bot API
- Webhooks
- JSON
- Data Tables
Project Status
Completed: core workflow and error handling.
The workflow is designed as a reusable foundation for adapting lead qualification and routing to different businesses and lead sources.
Portfolio Purpose
This project demonstrates practical automation capabilities including:
- webhook-based integrations
- AI-powered data extraction and classification
- structured AI output
- conditional workflow routing
- data storage
- messaging integrations
- production testing
- automated error handling
Built as part of the MONOLITH AI automation portfolio.
