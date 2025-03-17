# UBL API Testing Documentation

This document provides comprehensive information about the testing framework for the UBL Invoice Generation and Validation API.

If you're a group deciding whether to use our API, you should! We have multiple features including Order Document to Invoice Validation and Generation, Invoice Validation, Invoice Rendering to pdf, List users under admin, List invoices under users, Delete invoice, Email pdf and xml versions of invoice or multiple invoices, translate invoice.

## Important Notes
No Password Required: This API uses API key authentication, not username/password authentication. Users are identified by their email address and associated with an API key.
Automatic Creation: Users are created automatically when they access an endpoint with a valid API key and a new email address. There's no explicit "create user" endpoint.
User Association: All users created this way will be associated with the API key used in the request.
Multiple Users per API Key: You can have multiple users associated with a single API key.
Different Data Access: Each user will have their own set of invoices. When you authenticate with a specific user's email, you'll only see invoices created by that user.

## POSTMAN API TESTING INSTRUCTIONS
Postman testing instructions:
http://localhost:3000/api/healthcheck GET
Response:
{
    "status": "success",
    "message": "M13A_Guard011 API is up and running. We are an API for UBL Invoice Generation and Validation!",
    "database": "connected",
    "timestamp": "2025-03-13T11:00:45.025Z"
}

http://localhost:3000/api/keys/generate post
Set Content-Type header to application/json
    {
       "companyName": "Amitabh",
       "contactEmail": "amitabh@kumar.com"
     }

Reponse:
{
    "message": "API key generated successfully",
    "apiKey": "f3ec96bef98ccef284d3ca265d19a75a97169d25c795ccbb0b90fac6adb6b07f"
}


http://localhost:3000/api/keys/details GET
In headers:
x-api-key - f3ec96bef98ccef284d3ca265d19a75a97169d25c795ccbb0b90fac6adb6b07f
X-User-Email - amitabh@kumar.com

Use route with different emails but same API
Response:
{
    "apiKey": {
        "id": "30a3577c-a335-402a-b1a5-2cb526c1711a",
        "companyName": "Amitabh",
        "contactEmail": "amitabh@kumar.com",
        "active": true,
        "createdAt": "2025-03-16T01:06:24.183Z",
        "users": []
    }
}

http://localhost:3000/api/invoices/generate POST
X-API-Key: Your API key
X-User-Email: Your email
Content-Type: application/xml
paste in body the sample order and invalid case
response:
{
    "message": "Invoice generated successfully",
    "invoiceId": "d34c814b-64d5-4ab6-944a-8016e34b8ea5",
    "invoiceXml": "<Invoice xmlns=\"urn:oasis:names:specification:ubl:schema:xsd:Invoice-2\" xmlns:cac=\"urn:oasis:names:specification:ubl:schema:xsd:CommonAggregateComponents-2\" xmlns:cbc=\"urn:oasis:names:specification:ubl:schema:xsd:CommonBasicComponents-2\">\n  <cbc:UBLVersionID>2.1</cbc:UBLVersionID>\n  <cbc:ID>INV-964d6f7b</cbc:ID>\n  <cbc:IssueDate>2025-03-16</cbc:IssueDate>\n  <cbc:DueDate>2025-04-15</cbc:DueDate>\n  <cbc:InvoiceTypeCode listID=\"UN/ECE 1001\" listAgencyID=\"6\">380</cbc:InvoiceTypeCode>\n  <cbc:DocumentCurrencyCode>USD</cbc:DocumentCurrencyCode>\n  <cac:OrderReference>\n    <cbc:ID>PO-12345</cbc:ID>\n  </cac:OrderReference>\n  <cac:AccountingSupplierParty>\n    <cac:Party>\n      <cac:PartyName>\n        <cbc:Name>Supplier Inc.</cbc:Name>\n      </cac:PartyName>\n      <cac:PartyTaxScheme>\n        <cbc:CompanyID>US987654321</cbc:CompanyID>\n        <cac:TaxScheme>\n          <cbc:ID>VAT</cbc:ID>\n        </cac:TaxScheme>\n      </cac:PartyTaxScheme>\n    </cac:Party>\n  </cac:AccountingSupplierParty>\n  <cac:AccountingCustomerParty>\n    <cac:Party>\n      <cac:PartyName>\n        <cbc:Name>Acme Corporation</cbc:Name>\n      </cac:PartyName>\n      <cac:PartyTaxScheme>\n        <cbc:CompanyID>US123456789</cbc:CompanyID>\n        <cac:TaxScheme>\n          <cbc:ID>VAT</cbc:ID>\n        </cac:TaxScheme>\n      </cac:PartyTaxScheme>\n    </cac:Party>\n  </cac:AccountingCustomerParty>\n  <cac:TaxTotal>\n    <cbc:TaxAmount currencyID=\"USD\">150.00</cbc:TaxAmount>\n    <cac:TaxSubtotal>\n      <TaxableAmount currencyID=\"USD\">1500.00</TaxableAmount>\n      <TaxAmount currencyID=\"USD\">150.00</TaxAmount>\n      <TaxCategory>\n        <ID schemeID=\"UN/ECE 5305\" schemeAgencyID=\"6\">S</ID>\n        <Percent>10</Percent>\n        <TaxScheme>\n          <ID schemeID=\"UN/ECE 5153\" schemeAgencyID=\"6\">VAT</ID>\n        </TaxScheme>\n      </TaxCategory>\n    </cac:TaxSubtotal>\n  </cac:TaxTotal>\n  <cac:LegalMonetaryTotal>\n    <cbc:LineExtensionAmount currencyID=\"USD\">1500.00</cbc:LineExtensionAmount>\n    <cbc:TaxExclusiveAmount currencyID=\"USD\">1500.00</cbc:TaxExclusiveAmount>\n    <cbc:TaxInclusiveAmount currencyID=\"USD\">1650.00</cbc:TaxInclusiveAmount>\n    <cbc:PayableAmount currencyID=\"USD\">1650.00</cbc:PayableAmount>\n  </cac:LegalMonetaryTotal>\n  <cac:InvoiceLine>\n    <cbc:ID>1</cbc:ID>\n    <cbc:InvoicedQuantity unitCode=\"EA\">10</cbc:InvoicedQuantity>\n    <cbc:LineExtensionAmount currencyID=\"USD\">1000.00</cbc:LineExtensionAmount>\n    <cac:Item>\n      <cbc:Description>Laptop Computer Model</cbc:Description>\n      <cac:ClassifiedTaxCategory>\n        <cbc:ID>S</cbc:ID>\n        <cbc:Percent>10</cbc:Percent>\n        <cac:TaxScheme>\n          <cbc:ID>VAT</cbc:ID>\n        </cac:TaxScheme>\n      </cac:ClassifiedTaxCategory>\n    </cac:Item>\n    <cac:Price>\n      <cbc:PriceAmount currencyID=\"USD\">100.00</cbc:PriceAmount>\n    </cac:Price>\n  </cac:InvoiceLine>\n  <cac:InvoiceLine>\n    <cbc:ID>2</cbc:ID>\n    <cbc:InvoicedQuantity unitCode=\"EA\">5</cbc:InvoicedQuantity>\n    <cbc:LineExtensionAmount currencyID=\"USD\">500.00</cbc:LineExtensionAmount>\n    <cac:Item>\n      <cbc:Description>External Monitor</cbc:Description>\n      <cac:ClassifiedTaxCategory>\n        <cbc:ID>S</cbc:ID>\n        <cbc:Percent>10</cbc:Percent>\n        <cac:TaxScheme>\n          <cbc:ID>VAT</cbc:ID>\n        </cac:TaxScheme>\n      </cac:ClassifiedTaxCategory>\n    </cac:Item>\n    <cac:Price>\n      <cbc:PriceAmount currencyID=\"USD\">100.00</cbc:PriceAmount>\n    </cac:Price>\n  </cac:InvoiceLine>\n</Invoice>"
}
{
    "message": "Invalid order XML format"
}


POST
http://localhost:3000/api/invoices/validate
Add headers:
X-API-Key: Your API key
X-User-Email: Your email
Content-Type: application/xml
Body: sample invoice and invalid
Response:
{
    "valid": true,
    "errors": [],
    "warnings": [
        "Missing PaymentTerms (recommended)"
    ]
}
Reponse:
{
    "valid": false,
    "errors": [
        "Missing UBLVersionID",
        "Missing InvoiceTypeCode",
        "Missing AccountingSupplierParty",
        "Invoice must contain at least one InvoiceLine"
    ],
    "warnings": [
        "Missing PaymentTerms (recommended)"
    ]
}

GET
http://localhost:3000/api/invoices/{invoiceId}
Create a GET request to {{base_url}}/api/invoices/{invoiceId}
Replace {invoiceId} with an actual invoice ID from a previous generate request
Add headers:
X-API-Key: Your API key
X-User-Email: Your email
Response:
{
    "invoice": {
        "id": "b24d62ba-cf69-475e-9042-c1a3f3ceec1b",
        "invoiceNumber": "INV-26619fcc",
        "buyerName": "Acme Corporation",
        "sellerName": "Supplier Inc.",
        "totalAmount": "1650.00",
        "currency": "USD",
        "issueDate": "2025-03-13",
        "dueDate": "2025-04-12",
        "createdAt": "2025-03-12T12:51:18.084Z",
        "xmlContent": "<Invoice xmlns=\"urn:oasis:names:specification:ubl:schema:xsd:Invoice-2\" xmlns:cac=\"urn:oasis:names:specification:ubl:schema:xsd:CommonAggregateComponents-2\" xmlns:cbc=\"urn:oasis:names:specification:ubl:schema:xsd:CommonBasicComponents-2\">\n  <cbc:UBLVersionID>2.1</cbc:UBLVersionID>\n  <cbc:ID>INV-26619fcc</cbc:ID>\n  <cbc:IssueDate>2025-03-12</cbc:IssueDate>\n  <cbc:DueDate>2025-04-12</cbc:DueDate>\n  <cbc:InvoiceTypeCode listID=\"UN/ECE 1001\" listAgencyID=\"6\">380</cbc:InvoiceTypeCode>\n  <cbc:DocumentCurrencyCode>USD</cbc:DocumentCurrencyCode>\n  <cac:OrderReference>\n    <cbc:ID>PO-12345</cbc:ID>\n  </cac:OrderReference>\n  <cac:AccountingSupplierParty>\n    <cac:Party>\n      <cac:PartyName>\n        <cbc:Name>Supplier Inc.</cbc:Name>\n      </cac:PartyName>\n      <cac:PartyTaxScheme>\n        <cbc:CompanyID>US987654321</cbc:CompanyID>\n        <cac:TaxScheme>\n          <cbc:ID>VAT</cbc:ID>\n        </cac:TaxScheme>\n      </cac:PartyTaxScheme>\n    </cac:Party>\n  </cac:AccountingSupplierParty>\n  <cac:AccountingCustomerParty>\n    <cac:Party>\n      <cac:PartyName>\n        <cbc:Name>Acme Corporation</cbc:Name>\n      </cac:PartyName>\n      <cac:PartyTaxScheme>\n        <cbc:CompanyID>US123456789</cbc:CompanyID>\n        <cac:TaxScheme>\n          <cbc:ID>VAT</cbc:ID>\n        </cac:TaxScheme>\n      </cac:PartyTaxScheme>\n    </cac:Party>\n  </cac:AccountingCustomerParty>\n  <cac:TaxTotal>\n    <cbc:TaxAmount currencyID=\"USD\">150.00</cbc:TaxAmount>\n    <cac:TaxSubtotal>\n      <TaxableAmount currencyID=\"USD\">1500.00</TaxableAmount>\n      <TaxAmount currencyID=\"USD\">150.00</TaxAmount>\n      <TaxCategory>\n        <ID schemeID=\"UN/ECE 5305\" schemeAgencyID=\"6\">S</ID>\n        <Percent>10</Percent>\n        <TaxScheme>\n          <ID schemeID=\"UN/ECE 5153\" schemeAgencyID=\"6\">VAT</ID>\n        </TaxScheme>\n      </TaxCategory>\n    </cac:TaxSubtotal>\n  </cac:TaxTotal>\n  <cac:LegalMonetaryTotal>\n    <cbc:LineExtensionAmount currencyID=\"USD\">1500.00</cbc:LineExtensionAmount>\n    <cbc:TaxExclusiveAmount currencyID=\"USD\">1500.00</cbc:TaxExclusiveAmount>\n    <cbc:TaxInclusiveAmount currencyID=\"USD\">1650.00</cbc:TaxInclusiveAmount>\n    <cbc:PayableAmount currencyID=\"USD\">1650.00</cbc:PayableAmount>\n  </cac:LegalMonetaryTotal>\n  <cac:InvoiceLine>\n    <cbc:ID>1</cbc:ID>\n    <cbc:InvoicedQuantity unitCode=\"EA\">10</cbc:InvoicedQuantity>\n    <cbc:LineExtensionAmount currencyID=\"USD\">1000.00</cbc:LineExtensionAmount>\n    <cac:Item>\n      <cbc:Description>Laptop Computer</cbc:Description>\n      <cac:ClassifiedTaxCategory>\n        <cbc:ID>S</cbc:ID>\n        <cbc:Percent>10</cbc:Percent>\n        <cac:TaxScheme>\n          <cbc:ID>VAT</cbc:ID>\n        </cac:TaxScheme>\n      </cac:ClassifiedTaxCategory>\n    </cac:Item>\n    <cac:Price>\n      <cbc:PriceAmount currencyID=\"USD\">100.00</cbc:PriceAmount>\n    </cac:Price>\n  </cac:InvoiceLine>\n  <cac:InvoiceLine>\n    <cbc:ID>2</cbc:ID>\n    <cbc:InvoicedQuantity unitCode=\"EA\">5</cbc:InvoicedQuantity>\n    <cbc:LineExtensionAmount currencyID=\"USD\">500.00</cbc:LineExtensionAmount>\n    <cac:Item>\n      <cbc:Description>External Monitor</cbc:Description>\n      <cac:ClassifiedTaxCategory>\n        <cbc:ID>S</cbc:ID>\n        <cbc:Percent>10</cbc:Percent>\n        <cac:TaxScheme>\n          <cbc:ID>VAT</cbc:ID>\n        </cac:TaxScheme>\n      </cac:ClassifiedTaxCategory>\n    </cac:Item>\n    <cac:Price>\n      <cbc:PriceAmount currencyID=\"USD\">100.00</cbc:PriceAmount>\n    </cac:Price>\n  </cac:InvoiceLine>\n</Invoice>"
    }
}

GET
http://localhost:3000/api/invoices
Add headers:
X-API-Key: Your API key
X-User-Email: Your email
Response:
{
    "count": 2,
    "invoices": [
        {
            "id": "c3aefe6a-6d21-458c-aae7-5845bfd83e33",
            "invoiceNumber": "INV-79e8af01",
            "buyerName": "AMIn",
            "sellerName": "Supplier Inc.",
            "totalAmount": "1650.00",
            "currency": "USD",
            "issueDate": "2025-03-13",
            "dueDate": "2025-04-12",
            "createdAt": "2025-03-12T14:25:33.169Z"
        },
        {
            "id": "35c24a09-521e-4e0b-b39f-e10fc1d901ac",
            "invoiceNumber": "INV-888095ee",
            "buyerName": "Acme Corporation",
            "sellerName": "Supplier Inc.",
            "totalAmount": "1650.00",
            "currency": "USD",
            "issueDate": "2025-03-13",
            "dueDate": "2025-04-12",
            "createdAt": "2025-03-12T14:24:29.831Z"
        }
    ]
}

DELETE
http://localhost:3000/api/invoices/{invoice_id}
Response:
{
    "message": "Invoice deleted successfully",
    "invoiceId": "c3aefe6a-6d21-458c-aae7-5845bfd83e33"
}
If you check for id under invoices it should be gone.

GET
http://localhost:3000/api/invoices/{invoice_id}/pdf
X-API-Key: Your API key
X-User-Email: Your email
Response:pdf

POST
http://localhost:3000/api/invoices/{invoice_id}/translate
Content-Type: application/json
Body:
{
  "target_language": "hindi"
}
Note: You can use these valid languages: ['english', 'spanish', 'french', 'italian', 'hindi', 'japanese', 'chinese' ]
Response:
{
    "message": "Invoice translated successfully",
    "originalInvoiceId": "d34c814b-64d5-4ab6-944a-8016e34b8ea5",
    "translatedInvoiceId": "396f2c3c-7fa3-476c-b826-0199594e5e10"
}

You can copy the new invoice id for the translation, then fetch it and you can render it.

POST
http://localhost:3000/api/invoices/{invoice_id}/email
Replace invoiceid with existing invoice
X-API-Key: Your API key
X-User-Email: Your email
Body:
{
  "recipient_email": "dummybearsayshi@gmail.com",
  "custom_message": "Pay me now bitch!"
}
Response:
{
    "message": "Invoice sent successfully",
    "emailInfo": {
        "messageId": "<37f90e61-1647-09bb-c9f3-0e41726568a6@gmail.com>",
        "recipient": "dummybearsayshi@gmail.com",
        "invoiceNumber": "INV-964d6f7b-hi"
    }
}

POST
http://localhost:3000/api/invoices/email/batch
X-API-Key: Your API key
X-User-Email: Your email
Body:
{
  "invoice_ids": ["f48b15f4-504c-49cc-b900-fd9cb1c13c8e", "f2fade02-6b39-4506-9ea4-576e6e76e3b6"],
  "recipient_email": "test@example.com",
  "custom_message": "Here are your invoices for this month, you better pay me."
}
## Running Test Commands

The following npm scripts are available for running tests:

# Run all tests
npm test

# Run unit tests only
npm run test:unit

# Run integration tests only
npm run test:integration

# Run validation tests only
npm run test:validation

## Test Coverage
npm run test:coverage

## Continuous Integration

The testing framework is designed to be run in a CI/CD pipeline. Tests should be run:

- Before merging pull requests
- After deployment to staging
- Before deployment to production
