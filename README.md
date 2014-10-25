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
* Authorization
* Content-type: application/json

The body of the POST is a JSON stream with the following structure:

    {"Type": 0 or 1,            # 0 is bank-to-bank, 1 is bank-to-mobile
    "CompanyId": GUID           # ID of company, assigned by Chase Bank
    "Remarks": "My Testing",    # Comment on this batch.

    "OrderLines": [
        {"Payee": "Name Name",      # Not checked.
        "PrimaryAccountNumber": "1116031422",   # phone # or account # of recipient
        "Amount": 3000,             # in ksh
        "BankCode": "30011",        # Identifies the bank. Required for bank-to-bank transfers. Omit for bank-to-mobile transfers.
        "Reference": "Salary1",     # Internal reference for your own purposes.
        }, ...]
    }


