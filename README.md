# Order Processing Automation (AutoCart)

## Overview
Production-grade n8n workflow for e-commerce order processing.

## Features
- ✅ Webhook order reception
- ✅ Input validation
- ✅ Inventory API integration
- ✅ CRM contact creation
- ✅ Conditional routing (in-stock/backorder)
- ✅ Email notifications
- ✅ Error handling with retries
- ✅ Comprehensive logging

## Architecture

### Main Workflow
[Describe flow]

### Sub-Workflows
1. **Inventory Check** - Validates product availability
2. **CRM Contact Creation** - Creates customer records
3. **Backorder Handling** - Processes out-of-stock items

## Setup Instructions

### Prerequisites
- n8n Cloud account
- mockapi.io account (for mock APIs)
- Mailtrap account (for email testing)

### Mock APIs
1. Create Inventory resource: `GET /products/:id`
   Response: `{ "id", "name", "stock" }`

2. Create CRM resource: `POST /contacts`
   Request: `{ "name", "email", "orderId", "status" }`

### Credentials
Configure in n8n:
- Header Auth for Inventory API
- Header Auth for CRM API
- SMTP for Email notifications

### Testing

**Scenario 1: All Items In Stock**
```json
{
  "orderId": "ORD-1001",
  "customerName": "Jane Doe",
  "customerEmail": "jane@example.com",
  "items": [
    { "productId": "a1b2", "quantity": 2 },
    { "productId": "c3d4", "quantity": 3 }
  ]
}
```
Expected: HTTP 200, status: "fulfilled"

**Scenario 2: Out-of-Stock**
Expected: HTTP 200, status: "partially_backordered"

**Scenario 3: API Error with Retry**
Expected: Auto-retry after 30s, then success

## File Structure
