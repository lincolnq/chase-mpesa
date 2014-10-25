This documents the API for programmatically sending money from your M-Pesa
account.

Overview
--------

Requests must be made using authenticated HTTP POST requests to certain URLs on the website.

Site URIs:

* staging - http://ec2-54-68-40-210.us-west-2.compute.amazonaws.com/
* production - TBD

The authentication is HTTP basic auth using the username and password assigned by Chase Bank.


Submitting a Transaction
------------------------

POST to `/api/eft`.

Headers must include
* Authorization header (HTTP basic auth with your username/password)
* Content-type: application/json

The body of the POST is a JSON stream with the following structure:

```javascript
{
// 0 is bank-to-bank, 1 is bank-to-mobile
"Type": 0 or 1,

// ID of company, assigned by Chase Bank
"CompanyId": '00000000-1111-2222-3333-444444444444',

// Comment on this batch.
"Remarks": "My Testing",

// List of transactions to make:
"OrderLines": [
    
    {
    // Name of recipient. Not checked against government database.
    "Payee": "Name Name",

    // Phone # or account # of recipient - where the money is going
    "PrimaryAccountNumber": "1116031422",

    // Amount of money you are sending
    "Amount": 3000,
    
    // Recipient bank. Required for bank-to-bank. Omit for bank-to-mobile.
    "BankCode": "30011",

    // Internal reference for your own purposes.
    "Reference": "Salary1",
    }, 

    // ...Additional Orders as necessary...

    ]
}
```
