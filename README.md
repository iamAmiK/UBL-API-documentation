# UBL API documentation: Invoice Generation and Validation

Welcome to my repository. 

## Deployment (One production link, one testing link)

This has multiple features including Order Document to Invoice Validation and Generation, Invoice Validation, Invoice Rendering to pdf, List users under admin with optional filtering, List invoices under users, Delete invoice/invoices, Email pdf and xml versions of invoice or multiple invoices, translate invoice. 

There are **two deployments**, **one for production** and **one for testing**. The **production deployments**, has **NO cold starts** and is on AWS. The **testing deployment** has a **no cold start too**, I just have two deployments to save my AWS credits. **Note: Both testing and production deployments have the exact same features functions, routes and databases.** 

Please use the Testing deployment and **if you like the features, email at z5480896@ad.unsw.edu.au and I will send over links to our AWS Production deployment link.**

- Testing Deployment: [(https://iamamik710-bvpzkbif.leapcell.dev/)](https://iamamik710-bvpzkbif.leapcell.dev/)
- **Production Deployments (AWS): Contact @ z5480896@ad.unsw.edu.au** (same routes as above link just a little faster)

Please read the text above!!!

Swagger: https://iamamik.github.io/UBL-API-documentation/

Postman: https://amitabhk-8884800.postman.co/workspace/Amitabh-K's-Workspace~cea0c384-efd6-457d-8547-d860f4c6d6c1/collection/43573699-56f3827a-1cdc-4014-bbe3-c7c6a8169c1a?action=share&creator=43573699

https://documenter.getpostman.com/view/43573699/2sB2cUB3M5#c5be3b59-6814-4971-8a8a-bcc5a170635e

## Features (17 Features, check Swagger)

1. Admin/User Creation: Create API with email, the email inputted will be the admin email and all other emails associated with that API will be users.
2. Order Document to Invoice Generation: Inputted Order documents get validated for features and if successful users recieve an Invoice XML.
3. Invoice Validation: Users can input Invoice XML's which get validated for structure, logic and other requirements.
4. Invoice XML to PDF: Allow users to covert there stored invoices into pdf's and download straight away.
5. Invoice Translation: Inputted Invoice XML's will be coverted to target language but all stringent business logic and numerals will remain in English.
6. CRUD Operations: Delete invoice/invoices from user, list users under admin, list invoices under user, list invoices under user with filters.
7. Email Service: Send stored invoice or invoices to email with custom content and sent in both pdf and xml format.
