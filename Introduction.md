**Tell Me About Yourself:**

Good evening, My name is Lawrence Rodriques, and I am currently working as a Software Developer at Aurionpro Solutions with over 2 years of experience in developing enterprise and transaction banking applications using Java, Spring Boot, Microservices, PostgreSQL, Angular.

I completed my Bachelor's degree in Computer Engineering with Honors in Cyber Security from Fr. C. Rodrigues Institute of Technology and graduated with a GPA of 9.13.



In AurionPro, I work on Corporate and Transaction Banking platform for clients such as STC Bank and SAIB Bank of Saudi Region. My responsibilities include developing REST APIs, implementing business requirements and developing change requests, production support, issue resolution, and collaborating with QA, business teams, and clients.



I have primarily worked on payment-related modules with STC Bank including local payments, beneficiary management, WPS payroll processing, trade finance, and approval workflows. Through these modules, I have gained a good understanding of payment processing lifecycles, maker-checker workflows, transaction authorization, reconciliation concepts, and banking operations.



I also have knowledge of payment rails such as NEFT and IMPS, including transaction processing flows, cut-off timings, settlement concepts, end-of-day processing, transaction status management, and how payment instructions move between corporate systems, banks, and payment networks.



Apart from development, I have extensive experience in production support where I analyze logs, troubleshoot critical issues, identify root causes, coordinate with multiple teams, and deliver timely fixes to ensure uninterrupted banking operations.

(Currently, I am looking for an opportunity where I can deepen my understanding in financial technology, and contribute to building reliable and scalable banking solutions.)

Currently, I am looking for an opportunity where I can work on large-scale payment systems, deepen my understanding of system design and financial technology, and contribute to building reliable and scalable banking solutions.`



**Project Explanation (Interview Version):**

Currently, In AurionPro I am working on Corporate and Transaction Banking platform with STC Bank.



Where we provide a web-based banking application used by corporate customers to perform various banking operations such as payments, transaction management, beneficiary management, user management, approval workflows, payroll processing, trade finance, and report generation.



The application follows a maker-checker workflow where one user creates a transaction and another authorized user approves it before it is processed by the bank. This provides better control and security for corporate banking operations.



Some major modules in our application include:



• Corporate Onboarding

• User and Role Management

• Beneficiary Management

• Local Payments

• Own Account Transfers

• Bulk Payments

• WPS Payroll

• Bill Payments

• Government Payments

• Bank Guarantee

• Letter of Credit (LC) Amendments

• Trade Finance



From a technical perspective, the frontend is developed using Angular and communicates with backend services through REST APIs.



The backend follows a Microservices Architecture where different services are responsible for different business domains.



Major services include:



• Authentication Service

• Corporate Administration Service

• Payment Service

• Trade Service

• Reporting Service

• Common Utility Services

• Kafka Producer and Consumer Services



On the bank side, there are separate services for Bank Administration, Payments, and Trade operations.



PostgreSQL is used for data persistence, while Kafka is used for asynchronous processing such as notifications, bulk payment processing, and event-driven communication.



Authentication and authorization are implemented using Spring Security and JWT tokens.



**My primary responsibilities include:**



• Developing REST APIs using Java and Spring Boot

• Implementing new business requirements and CRs

• Database development and query optimization

• Production support and issue resolution

• Code reviews and testing support

• Bank Interface Creation and Integration

• Working closely with QA and business teams

• Participating in requirement discussions and impact analysis



I have worked extensively on payment workflows where users create payment instructions, authorize transactions, validate business rules, process payments, track transaction statuses, and generate reports.



**Local Transfer Module:**

In the Local Transfer module, the user first selects the debit account from which the amount needs to be transferred. Once the account is selected, the available balance is displayed.

The user can then either select an existing beneficiary or create a runtime beneficiary. After selecting the beneficiary, the user enters the transfer amount and an optional payment note.

Before proceeding, the system validates the user's daily transaction limit. If the amount is within the allowed limit, the user clicks Continue, where the applicable transaction charges are calculated and the total debit amount is displayed.

On clicking Submit, the system performs validations such as OTP verification and balance verification. If all validations are successful, the transaction is created.

If the user is a Self-Authorized user, the transaction is processed directly to the bank. If the user is a Maker, the transaction is sent to the Checker for authorization. Once the Checker authorizes the transaction, OTP and balance validations are performed again, and if successful, the transaction is finally processed to the bank.



**WPS Payroll Module:**

WPS (Wage Payment System) Payroll is used by corporate customers to process employee salary payments. Before using this service, the corporate must first register for WPS Payroll with the bank.

Once registered, the corporate uploads a salary file in a predefined Excel format. The file contains employee details such as Iqama number (employee ID), employee name, account details, and salary amount.

The file upload is processed asynchronously, so after uploading, the file appears in the listing with a Processing status. A background process validates each record by checking employee details, fetching the corresponding account information, validating salary data, and identifying any errors. If a record has validation issues, the corresponding error is displayed for that specific employee, while valid records continue to be processed.

After the file is processed successfully, the salary transactions are created. Depending on the user's authorization type, if the user is Self-Authorized, the transactions are processed directly to the bank. If the user follows the Maker-Checker process, the transactions are sent to the Checker for approval. Once approved, the salary payments are processed, and the salary amounts are credited to the employees' bank accounts.



"Since a payroll file can contain hundreds or even thousands of employee records, processing it synchronously would keep the user waiting for a long time. Therefore, we process the file asynchronously in the background, update the processing status, and notify the user once the processing is complete."



**Production Issue (Strong Banking Support Example):**

One critical production issue I handled was related to payment transaction processing.



Users reported that multiple payment transactions were remaining in a PENDING state even though the transactions had already been processed successfully by the bank.



Since this was a production issue affecting customer payments, it was treated as high priority.



My first step was to analyze the application logs and transaction records. I verified that the payment requests were successfully sent from our Payment Service and that the bank had processed the transactions.



However, the transaction status in our system was not getting updated from PENDING to SUCCESS.



I then traced the complete transaction flow and checked Kafka event processing. During the investigation, I found that a consumer service responsible for processing payment status updates had failed because of an unexpected message format change in one of the downstream events.



As a result, the status update event was not being consumed successfully, and transactions remained in a PENDING state.



After identifying the root cause, I implemented the required fix, reprocessed the affected messages, and validated the status updates in the database.



I also added additional logging and monitoring to detect similar failures earlier in the future.



The issue was resolved successfully, pending transactions were updated correctly, and normal payment processing resumed.



This incident demonstrated my production troubleshooting skills, log analysis capability, understanding of asynchronous systems, Kafka-based event processing, and ability to coordinate with multiple teams during critical incidents.

