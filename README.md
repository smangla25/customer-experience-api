# Customer Experience API

MuleSoft Mule 4 Experience Layer API built for the SCRUM-5 story.  
Deployment target: **CloudHub 2.0** · Runtime: **4.6.0**

## Endpoints

| Method | Path | Description |
|--------|------|-------------|
| GET | `/api/customers/{customerId}` | Get customer by ID |
| POST | `/api/customers` | Create new customer |
| GET | `/api/customers?status={status}` | Search customers by status |

## Architecture

```
Mobile App → Customer Experience API → Customer System API → Salesforce CRM
            (this service)             (system layer)
```

## Local Development

1. Open in Anypoint Studio
2. Set run configuration property: `-Dsecure.key=<your-key> -Dmule.env=dev`
3. Run on `http://localhost:8081`

## Bug Fixes (WarRoom AI — SCRUM-5 Prevention Run)

| ID | Fix |
|----|-----|
| H-001 | GET path now uses `http:uri-params` map instead of string-embedded `#[expr]` |
| H-002 | POST validation uses `raise-error` → guaranteed HTTP 400 response |
| M-002 | All error handlers changed `on-error-propagate` → `on-error-continue` |
| M-001 | Added `case "S" -> "suspended"` to both status transforms; aligned `else → "unknown"` |
| L-001 | `createdDate` null fallback is now `null` instead of `now()` |
