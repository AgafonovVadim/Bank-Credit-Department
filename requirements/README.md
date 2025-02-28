# Credit Processing System Specification

The document outlines the system’s requirements, user interview questions, user stories, use cases, error handling scenarios, regulatory mandates, and an analysis of the completeness of the requirements.

## Table of Contents

1. [User Interview Questions](#user-interview-questions)
2. [Functional and Non-Functional Requirements](#functional-and-non-functional-requirements)
3. [User Stories and Use Cases](#user-stories-and-use-cases)
4. [Error Handling Scenarios](#error-handling-scenarios)
5. [Regulatory Requirements](#regulatory-requirements)
6. [Analysis of Requirements Completeness](#analysis-of-requirements-completeness)
7. [Final Document / Application Value](#final-document--application-value)

## User Interview Questions

### General Questions
- **Main Issues:** What are the key problems with the current credit processing system?
- **Communication Channels:** Which channels (chat, SMS, email, social media) are prioritized for client interactions?
- **Integration:** How is integration with external systems (government agencies, other banks) managed?
- **Regulatory Requirements:** Which regulations (e.g., GDPR, AML, Federal Law 152-FZ) need to be taken into account?
- **Success Metrics:** What are the critical success metrics (e.g., processing speed, fraud reduction)?

### For Clients
- What actions should clients be able to perform in their personal account?
- Is there a need for a mobile version or dedicated application?
- How do clients prefer to receive notifications (SMS, email, push)?

### For Employees
- What tools are currently used for creditworthiness analysis?
- How should the notification system for managers operate?
- Are role-based access models required within teams?

### Technical Aspects
- What are the response time requirements (e.g., application loading ≤2 seconds)?
- What level of system availability is needed (e.g., 99.9% uptime)?

## Functional and Non-Functional Requirements

### Functional Requirements (FR)

#### Module 1: Application Processing
- **FR1.1:** Clients can complete an online application by providing personal data, credit purpose, and income sources.
- **FR1.2:** Integration with NBKI for credit history verification via API.
- **FR1.3:** Automatic validation of data completeness (e.g., email, TIN, passport).

#### Module 2: Scoring
- **FR2.1:** Calculation of credit scoring based on credit history, income, and demographic data.
- **FR2.2:** Generation of recommendations for specialists (e.g., “Approve”, “Reject”, “Manual Review”).

#### Module 3: Document Management
- **FR3.1:** Upload of documents in PDF, JPEG, PNG formats (maximum 10 MB).
- **FR3.2:** Verification of document authenticity using OCR and registry comparisons (FNS).

#### Module 4: Communication
- **FR4.1:** Chat support via Telegram and WhatsApp API.
- **FR4.2:** Automatic notifications on the application status (SMS, email, push).

### Non-Functional Requirements (NFR)
- **Performance:**
  - Application processing in ≤3 minutes under 5000 concurrent sessions.
  - Personal account loading in ≤1.5 seconds.
- **Security:**
  - Data encryption using TLS 1.3.
  - Two-factor authentication for employees.
- **Scalability:**
  - Support for horizontal scaling (e.g., Kubernetes).
- **Reliability:**
  - Regular backups every 6 hours.
  - System recovery in ≤15 minutes after a failure.
- **Compatibility:**
  - **Mobile OS:** Android (version 10+ with WebView 85+), iOS (version 14+).
  - **Browsers:** Google Chrome (90+), Mozilla Firefox (88+), Safari (14+), Microsoft Edge (91+).
  - **Screen Resolutions:** Responsive design from 320px (mobile) to 3840px (4K monitors).
  - **API:** RESTful API compatibility (version 2.0), support for JSON and XML formats.

## User Stories and Use Cases

### User Stories
- **Client:** Sign documents using an electronic signature to avoid visiting the bank.
- **Administrator:** Configure access rights for new employees to minimize data breach risks.
- **Analyst:** Export data to Excel for credit portfolio forecasting.
- **Legal Advisor:** Automatically generate contracts based on approved applications.
- **IT Specialist:** Monitor server load in real time to prevent failures.
- **Client:** Withdraw an application before processing to modify credit terms.

### Use Cases

#### Updating the Scoring Model
- **Actors:** Analytics Department, System.
- **Steps:**
  1. Analysts upload a new version of the ML model.
  2. The system performs A/B testing on 10% of the applications.
  3. If successful (accuracy >90%), the model is deployed for all applications.
  4. The old model is retained as a backup for 30 days.

#### Processing a GDPR Request
- **Actors:** Client, System, Administrator.
- **Steps:**
  1. The client submits a data deletion request through the personal account.
  2. The system verifies there are no active credits.
  3. Data is anonymized within 72 hours.
  4. The administrator confirms the completion of the request.

#### Integration with GIS GMP
- **Actors:** System, GIS GMP (state system).
- **Steps:**
  1. Upon credit approval, the system generates an electronic receipt.
  2. Data is automatically sent to GIS GMP via API.
  3. The system checks the payment processing status every 15 minutes.
  4. In case of integration errors, a manual verification process is initiated.

## Error Handling Scenarios

### Scenario 1: NBKI Integration Error
- **Condition:** API is unavailable for more than 30 seconds.
- **Actions:**
  1. Save the application with a “Pending” status.
  2. Notify technical support.
  3. Retry the request after 5 minutes (up to 3 attempts).
  4. Notify the client if the retries are exhausted: “The verification is taking longer than expected.”

### Scenario 2: Invalid Document
- **Condition:** An unreadable file is uploaded.
- **Actions:**
  1. Reject the document.
  2. Request the client to re-upload the file.

## Regulatory Requirements
- **GDPR:**
  - Explicit client consent for data processing.
  - Data deletion within 72 hours upon request.
- **AML/KYC:**
  - Client verification against sanctions lists (OFAC, EU).
  - Audit logging of employee actions.
- **Federal Law 152-FZ (RF):**
  - Data storage on servers within the Russian Federation.
  - Encryption when transmitting data outside the bank.
- **PCI DSS:**
  - Prohibition on storing CVV/CVC codes.
  - Annual security audits.

## Analysis of Requirements Completeness

### Strengths
- Comprehensive coverage of key roles (clients, employees, administrators).
- Detailed modules for scoring, document management, and communication.
- Inclusion of major regulatory requirements (GDPR, Federal Law 152-FZ).

### Weaknesses
- No requirements for auditing changes to applications.
- Data recovery procedures for hardware failures are not specified.

### Recommendations
- Add an audit log to track employee actions.
- Clarify integration details with messaging applications (e.g., WhatsApp Business API).
- Define SLAs for external API response times (maximum of 2 seconds).

## Final Document / Application Value

- **Improved Efficiency:** Automation is expected to accelerate application processing by 40%.
- **Risk Reduction:** Fraud risk is minimized through integration with AML services.
- **Regulatory Compliance:** The system adheres to GDPR and Federal Law 152-FZ, ensuring operational compliance in both the Russian Federation and the EU.
