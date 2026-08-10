# OccuCare Security Advisory

Security advisory for a missing authentication vulnerability discovered in OccuCare.

## Missing Authentication for Critical Function

**Tracking ID:** CAN-2026-2035499  
**CWE:** CWE-306 – Missing Authentication for Critical Function  
**Researcher:** J4n4z4 - Ahmed Alshammari  
**Status:** Reported to MITRE CNA-LR

---

## Summary

A missing authentication vulnerability was identified in the OccuCare
web-based API Check functionality.

The affected functionality was accessible without an authenticated user
session and allowed an unauthenticated remote user to trigger server-side
calls to production API services.

During testing, the application successfully returned live production claim
records containing sensitive employee, patient, claim, and medical-related
information.

The issue is caused by insufficient authentication enforcement on the
affected functionality.

---

## Affected Product

- **Vendor:** OccuCare
- **Product:** OccuCare
- **Affected Component:** API Check / External API Call
- **Affected Version:** Unknown / version information was not available during testing
- **Platform:** Web Application / API

---

## Vulnerability Classification

- **CWE:** CWE-306 – Missing Authentication for Critical Function
- **Attack Vector:** Network
- **Attack Complexity:** Low
- **Authentication Required:** No
- **Privileges Required:** None
- **User Interaction:** None

---

## Impact

An unauthenticated remote attacker can access the affected API Check
functionality and trigger server-side requests to production API services.

During testing, the affected functionality returned live production claim
information without requiring an authenticated user session.

The exposed response contained sensitive information, including:

- Beneficiary names
- Employee identifiers
- Mobile numbers
- Hospital information
- Claim information
- Admission and discharge information
- Medical-related information
- Nature of illness
- Relationship information
- Geographic information

This results in unauthorized disclosure of sensitive employee, patient,
claim, and medical-related information.

---

## Technical Details

The affected API Check functionality was accessible without authentication.

During testing, an unauthenticated request to the affected functionality
successfully triggered a server-side call to a production API service.

The application returned:

`HTTP Status Code: 200 OK`

The response contained live claim records.

Observed response fields included:

- `AGE`
- `BENEFICIARY_NAME`
- `CLAIM_TYPE`
- `DATE_OF_INTIMATION`
- `DT_OF_ADMISSION`
- `DT_OF_DISCHARGE`
- `DT_OF_FILE_RECD`
- `EMPLOYEE_NO`
- `GRADE`
- `HOSPITAL_NAME`
- `INTIMATION_NO`
- `MESSAGE`
- `MOBILE_NO`
- `NATURE_OF_ILLNESS`
- `NETWORK_CITY`
- `PROPOSER_NAME`
- `RELATION`
- `STATE`
- `TPA_CARD_NO`
- `TYPE_OF_INTIMATION`

No authenticated user session was required to access the affected
functionality during testing.

Exact endpoint parameters, IP addresses, personal information, medical
information, and other sensitive values are intentionally withheld from
this public advisory.

---

## Proof of Concept

The vulnerability was reproduced by accessing the affected API Check
functionality without an authenticated user session.

The exposed functionality allowed a server-side production API call to be
triggered successfully.

The server returned:

`HTTP 200 OK`

The response contained multiple live claim records and sensitive
employee, patient, and medical-related information.

A redacted screenshot demonstrating the observed behavior is provided below.

![Redacted Proof of Concept](evidence/occucare-poc-redacted.png)

Sensitive personal information, medical information, IP addresses,
endpoint parameters, identifiers, and other potentially sensitive values
have been redacted from the publicly available evidence.

---

## Reproduction Summary

The issue can be summarized as follows:

1. Access the affected API Check functionality without an authenticated
   user session.
2. Trigger the exposed server-side API call functionality.
3. The application processes the request without requiring authentication.
4. The server responds with HTTP 200.
5. Live production claim records containing sensitive information are
   returned.

Detailed endpoint parameters and request values are intentionally omitted
to reduce the risk of abuse.

---

## Expected Behavior

Access to functionality capable of invoking production API services and
retrieving sensitive claim information should require authentication and
appropriate authorization.

Unauthenticated users should not be able to invoke the affected
functionality or retrieve production records.

---

## Observed Behavior

The affected functionality could be accessed without an authenticated user
session.

An unauthenticated request successfully triggered a production API call and
returned live sensitive records.

---

## Security Impact

The vulnerability may result in:

- Unauthorized access to sensitive information
- Exposure of employee information
- Exposure of patient information
- Exposure of claim information
- Exposure of medical-related information
- Unauthorized invocation of server-side production API functionality

The demonstrated impact is primarily a loss of confidentiality.

---

## Remediation

The affected functionality should require authentication before processing
any request.

Recommended remediation includes:

- Enforce authentication on the affected API Check functionality.
- Enforce server-side authorization for all sensitive API operations.
- Prevent unauthenticated users from invoking production API calls.
- Restrict development and diagnostic functionality from public access.
- Apply least-privilege access controls to backend API integrations.
- Review application and API logs for previous unauthorized access.
- Review whether similar API Check or diagnostic functionality exists
  elsewhere in the application.
- Avoid returning sensitive production information through development,
  diagnostic, or testing interfaces.

---

## CVSS

The vulnerability was assessed using CVSS v4.0.

**Vector:**

`CVSS:4.0/AV:N/AC:L/AT:N/PR:N/UI:N/VC:H/VI:N/VA:N/SC:N/SI:N/SA:N`

**Base Score:** 8.7 (High)

The primary demonstrated security impact is unauthorized disclosure of
confidential information.

---

## CVE Status

A CVE ID request has been submitted to MITRE CNA-LR.

**MITRE Request Tracking ID:** `CAN-2026-2035499`

> **Important:** CAN-2026-2035499 is a request tracking identifier and is
> not a CVE ID.

This advisory will be updated if a CVE identifier is assigned.

---

## Disclosure

This advisory is published for vulnerability coordination and CVE reference
purposes.

Potentially sensitive exploitation details, including exact endpoint
parameters and unredacted production data, have intentionally been omitted.

The public proof of concept contains only redacted evidence sufficient to
demonstrate the observed security issue without intentionally exposing
sensitive personal or medical information.

---

## Credit

Discovered and reported by:

**J4n4z4 - Ahmed Alshammari**

Security Researcher / Penetration Tester
