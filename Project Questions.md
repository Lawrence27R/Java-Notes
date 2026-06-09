**Tell me about yourself**



Good morning, sir. My name is Lawrence Rodriques, and I am currently working as a Software Developer at Aurionpro Solutions. I have over 2 years of experience in developing enterprise-grade banking applications using Java, Spring Boot, Microservices, PostgreSQL and Angular.



I completed my Bachelor's degree in Computer Engineering from Fr. C. Rodrigues Institute of Technology, with Honors in Cyber Security, and graduated with a GPA of 9.13.



At Aurionpro, I work on Corporate and Transaction Banking platforms for clients such as STC Bank and SAIB Bank. My primary responsibilities include designing and developing RESTful APIs, implementing business requirements using Java and Spring Boot, working with Microservices architecture, and managing database interactions using PostgreSQL.



In addition to backend development, I have also contributed to Angular-based frontend modules development, production support, issue analysis and resolution, requirement gathering and development of CR's, and coordination with QA and business teams during testing and release activities.



Over the course of my experience, I have developed strong problem-solving skills, particularly in debugging production issues, optimizing application performance, and delivering reliable solutions in a fast-paced environment.



Currently, I am looking for an opportunity where I can work on scalable applications, learn modern system design and architecture, solve challenging technical problems, and continue growing my skills as a software engineer.



**Explain about your project and project architecture:**

**WPS Payroll**

Currently, I am working on a Corporate and Transaction Banking platform at Aurionpro for clients such as STC Bank and SAIB Bank.



Our product was (iCashpro) it is a platform, corporate customers to perform banking operations such as payment processing, transaction management, user management, approval workflows, and trade finance activities through a secure web application.

Various modules of our project include corporate onboarding, Payment(Own Account Transfer, Local Bank Payments, Quick Transfer), Beneficiary Creation, Bulk Payment, WPS Payroll, Bill Payment, Government Bill Payments

The application is built using Java, Spring Boot, Microservices, PostgreSQL, and Angular.



The flow of our application is

Corporate onboarding: Corporate clients such as Tata/Mahindra used to get onboarded on our platform, KYC of the onboarded corporate was handled by bank third party

In corporate onboarding, corporate can onboard Corporate User the KYC of the corporate user was handled bank third party.

The corporate can assign role to the user of modules which he can access also decide whether that corporate user is maker/checker/selfauth user

Our application mainly followed maker-checker where maker user use to create a transaction and checker user use to authorize the transaction.

So suppose a corporate has to make a payment to a Ex corporate maker user use to initiate the payment and checker user use to authorize the payment through listing.

This was the flow for most of the modules.



My primary responsibilities include developing REST APIs, implementing business requirements, database interactions, production support, bug fixing, and collaborating with QA and business teams during releases.



I have worked extensively on payment-related modules where users can initiate transactions, validate requests, authorize payments, and track transaction status. I have also been involved in resolving production issues, analyzing logs, and implementing fixes to ensure smooth banking operations.



The frontend is developed using Angular and communicates with backend services through REST APIs.



The backend follows a Microservices architecture where each service is responsible for a specific business domain.

Corporate Authentication Service

Corproate Admin Service (Set Up code)

Commons

Corporate Payments Service (Payment related code)

Payments

Corporate Report Service (Report Generation Code)

Corporate Trade Service (Bank Grantee, LC amendment, Trade Bill Payment)

Kafka Consumer (For sending Notification and Posting payment for bulk payment)

Kafka Producer



Bank Side

Bank Admin

Bank Payment

Bank Trade



Each service contains its own business logic and communicates through REST APIs. PostgreSQL is used for persistent data storage, while Kafka can be used for asynchronous communication and event processing where required.



Authentication and authorization are implemented using Spring Security and JWT tokens to ensure secure access to banking operations.



**What are your responsibilities at Aurionpro?**

My key responsibilities include:



Developing and enhancing REST APIs using Java and Spring Boot.

Implementing business requirements and change requests in banking modules such as Payments and Trade Finance.

Working with PostgreSQL databases for data storage, query writing, and performance optimization.

Collaborating with frontend developers and integrating Angular applications with backend APIs.

Investigating and resolving production issues by analyzing logs, debugging code, and providing fixes.

Participating in requirement discussions, impact analysis, and solution design with business and QA teams.

Performing unit testing and supporting integration testing and release activities.

Coordinating with clients to understand issues, provide updates, and ensure timely resolution.





**Explain a production issue you solved.**

**Production Issue 1: Role Update Not Working for Self-Authorized Users**



One production issue I worked on involved user role management in our Corporate Banking application.



We had two types of users:



Self-Authorized Users

Maker-Checker Users



The issue was that when a Self-Authorized User attempted to update their role, the update was not getting reflected in the system, and the user continued to retain their previous role.



I was assigned to investigate the issue. Initially, I checked the backend APIs, business logic, and database updates, but everything appeared to be functioning correctly.



I then analyzed the request payload being received by the backend and compared it with the payload generated from the frontend. During this analysis, I discovered that a specific widget on the frontend was not sending a required field in the request payload for Self-Authorized Users.



Because the backend was not receiving the updated role information, it was processing the request using the existing role value.



After identifying the root cause, I coordinated with the frontend team, the payload mapping was corrected, and we thoroughly tested the fix across different user types.



As a result, role updates started working correctly for Self-Authorized Users in production.



What this demonstrates

Debugging skills

API analysis

Frontend-backend integration knowledge

Cross-team collaboration



**Production Issue 2: Report Generation Failure in Production**

QC - schema wise so all user used to get access

Prod - user wise there were 2-3 db users in prod so we needed to give access to that users

Another critical issue occurred in the reporting module.



Users were unable to generate certain reports in the Production environment, while the same functionality was working successfully in QC and UAT environments.



Since the issue was environment-specific, I started by comparing application logs and database configurations across environments.



After investigation, I found that the report query was accessing a particular database table, but the Production database user did not have the required privileges on that table.



Our Production environment uses schema-based database access with different users and permissions, whereas QC and UAT had broader access privileges.



Due to the missing GRANT permission, the report query failed during execution in Production.



I documented the issue, coordinated with the DBA team, and requested the necessary database privileges for the application user.



Once the permissions were granted, the reports were generated successfully without any code changes.



This issue reinforced the importance of verifying environment-specific configurations and database permissions during production troubleshooting.



What this demonstrates

SQL and database knowledge

Production troubleshooting

Environment comparison

Working with DBAs and infrastructure teams







**HLD**

HLD describes the overall architecture of the system and how major components interact.

System architecture

Services/Microservices

Database selection

API communication

Scalability

Load balancing



**LLD**

LLD focuses on the internal implementation of components.

LLD focuses on the internal implementation of components.(modules)

Classes

Objects

Interfaces

Design Patterns

Relationships



**Questions to asked:**

**Is your advertising platform similar to Google AdSense**

**What cloud technologies does the company primarily use? Do you provide cloud-based solutions to clients, or is the cloud mainly used for your internal infrastructure?**

**Do you use Machine Learning or AI in your ad-serving platform?**





**How Google AdSense Works (Simple Explanation)**



Google AdSense is a platform that allows website owners, bloggers, and app developers to earn money by displaying ads on their websites or apps.



Step 1: Website Owner Joins AdSense



A publisher (website owner) signs up for Google AdSense and adds a small JavaScript code snippet to their website.



Step 2: User Visits the Website



When a user opens the website, the AdSense code sends a request to Google's ad servers asking:



What page is being viewed?

Who is the user? (location, device, interests, etc.)

What ad spaces are available?

Step 3: Advertisers Bid for the Ad Space



Advertisers using Google Ads want to show their ads to relevant users.



Google runs a Real-Time Bidding (RTB) auction in milliseconds:



Advertiser A bids ₹10

Advertiser B bids ₹15

Advertiser C bids ₹12



The best ad (based on bid + quality) wins.



Step 4: Ad is Displayed



The winning advertisement is shown to the user on the website.



Step 5: Publisher Earns Money



The website owner earns money when:



A user clicks the ad (CPC - Cost Per Click)

A user views the ad (CPM - Cost Per Thousand Impressions)



Google keeps a percentage of the revenue and pays the rest to the publisher.

