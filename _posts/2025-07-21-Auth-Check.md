---
layout: post
title: "Auth Check function SAP" 
date: 2025-07-21 12:00:00 -0600
categories: Learning daily SAP
---

I had to configure a validation for what to show in a specific report. To perform this validation, I needed to use the `AUTHORITY-CHECK` function. But how does this function actually work?

## How to Use the `AUTHORITY-CHECK` Function

First of all, we need to know which authorization object we want to check. Here's a basic example:


```abap
 AUTHORITY-CHECK OBJECT 'S_CARRID'
    ID 'CARRID' FIELD carr
    ID 'ACTVT'  FIELD '03'.
```

This is the syntax of the function. In this example, we’re checking whether the current user has authorization for a specific `CARRID`. After executing the check, the system sets the sy-subrc variable with the result, which we can use to handle different cases:

| sy-subrc  | Meaning                       |
| --------- | ----------------------------- |
| 0         | User is authorized.          |
| 4         | User is not authorized.     |

The ACTVT field refers to an activity code from the TACT table in the SAP database.

You can also validate multiple fields like this:

```abap
 AUTHORITY-CHECK OBJECT 'S_CARRID'
    ID 'CARRID' FIELD carr
    ...
    ID 'CARRID' FIELD carr2
    ...
    ID 'OBJID' FIELD obj
    ID 'ACTVT'  FIELD '03'.
```

## Where Should You Use the `AUTHORITY-CHECK` Function?

At first, I thought I could validate the user's authorization after fetching the data—just filter the result table before displaying the report. But... it’s actually better to check the authorization before querying the data—right when the user tries to run the report.

In code, this means placing the AUTHORITY-CHECK inside the AT SELECTION-SCREEN block. For example:

```abap
at selection-screen.

select * into table tb_carr
from carr.

AUTHORITY-CHECK OBJECT 'S_CARRID'
    ID 'CARRID' FIELD tb_carr-carr
    ID 'ACTVT'  FIELD '03'.

IF sy-subrc <> 0.
    MESSAGE 'No authorization' TYPE 'E'.
  ENDIF.
```

> :memo: **Take note**
> The field values must be in uppercase to be validated correctly!