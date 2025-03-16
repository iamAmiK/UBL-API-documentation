# UBL API documentation: Invoice Generation and Validation

Welcome to Guard's repository. 

## Deployment

We have **three deployments**, **two for production** and **one for testing**. Of our **production deployments**, they both have **NO cold starts**. Our **testing deployment** has a **cold start (20 - 60 sec)** but every query after that is immediate. 

For the testing deployment, **once the cold start has passed the API will be fully accessible with speed**. Please use our Testing deployment and **if you like our features, email at z5480896@ad.unsw.edu.au and we will send over links to both Production deployments.**

- Testing Deployment: https://guard-ubl-api.onrender.com
- Production Deployments: Contact @ z5480896@ad.unsw.edu.au
**- Note: Both testing and production deployments have the exact same functions, routes and databases.**

## Features

1. Admin/User Creation: Create API with email, the email inputted will be the admin email and all other emails associated with that API will be users.
2. Order Document to Invoice Generation: Inputted Order documents get validated for features and if successful users recieve an Invoice XML.
3. Invoice Validation: Users can input Invoice XML's which get validated for structure, logic and other requirements.
4. Invoice XML to PDF: Allow users to covert there stored invoices into pdf's and download straight away.
5. Invoice Translation: Inputted Invoice XML's will be coverted to target language but all stringent business logic and numerals will remain in English.
6. CRUD Operations: Delete invoices, list users under admin, list invoices under user.
7. To be added: Email service.
