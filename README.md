# UBL API documentation: Invoice Generation and Validation

Welcome to Guard's repository. 

## Deployment (Two production links, one testing link)

If you're a group deciding whether to use our API, you should! We have multiple features including Order Document to Invoice Validation and Generation, Invoice Validation, Invoice Rendering to pdf, List users under admin, List invoices under users, Delete invoice, Email pdf and xml versions of invoice or multiple invoices, translate invoice. 

We have **three deployments**, **two for production** and **one for testing**. Of our **production deployments**, they both have **NO cold starts** and are on AWS. Our **testing deployment** has a **cold start (20 - 60 sec)** but every query after that is immediate. **Note: Both testing and production deployments have the exact same features functions, routes and databases.** You can use our sample files for testing on Postman (put in body).


For the testing deployment, **once the cold start has passed the API will be fully accessible with speed**. Please use our Testing deployment and **if you like our features, email at z5480896@ad.unsw.edu.au and we will send over links to both Production deployments.**

- Testing Deployment: https://guard-ubl-api.onrender.com
- **Production Deployments (AWS): Contact @ z5480896@ad.unsw.edu.au**

Please read the text above!!!

## Features

1. Admin/User Creation: Create API with email, the email inputted will be the admin email and all other emails associated with that API will be users.
2. Order Document to Invoice Generation: Inputted Order documents get validated for features and if successful users recieve an Invoice XML.
3. Invoice Validation: Users can input Invoice XML's which get validated for structure, logic and other requirements.
4. Invoice XML to PDF: Allow users to covert there stored invoices into pdf's and download straight away.
5. Invoice Translation: Inputted Invoice XML's will be coverted to target language but all stringent business logic and numerals will remain in English.
6. CRUD Operations: Delete invoice/invoices from user, list users under admin, list invoices under user, list invoices under user with filters.
7. Email Service: Send stored invoice or invoices to email with custom content and sent in both pdf and xml format.
