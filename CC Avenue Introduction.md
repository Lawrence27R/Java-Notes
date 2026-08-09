**CC Avenue Introduction:**

Good evening, my name is Lawrence Rodriques, and I am currently working as a Software Developer at Aurionpro Solutions with over 2 years of experience in developing enterprise and transaction banking applications using Java, Spring Boot, Microservices, PostgreSQL, and Angular.



I completed my Bachelor's degree in Computer Engineering with Honors in Cyber Security from Fr. C. Rodrigues Institute of Technology and graduated with a GPA of 9.13.



At Aurionpro, I work on Corporate and Transaction Banking platforms for clients such as STC Bank and SAIB Bank in Saudi Arabia. My responsibilities include developing REST APIs, implementing business requirements and change requests, providing production support, resolving critical issues, and collaborating with QA teams, business stakeholders, and clients.



I have primarily worked on payment-related modules for STC Bank, including local payments, bill payments (SADAD integration), beneficiary management, WPS payroll processing, trade finance, and approval workflows. Through these modules, I have gained a strong understanding of payment processing lifecycles, bill payment workflows, maker-checker authorization, transaction validation, reconciliation concepts, and overall banking operations.



I also have knowledge of payment rails such as NEFT and IMPS, along with transaction processing flows, cut-off timings, settlement concepts, end-of-day processing, transaction status management, and how payment instructions move securely between corporate systems, banks, and payment networks.



Apart from development, I have extensive experience in production support, where I analyze application logs, troubleshoot critical production issues, identify root causes, coordinate with cross-functional teams, and deliver timely fixes to ensure uninterrupted banking operations.



Additionally, I have worked on integrating AI capabilities into enterprise applications using Spring AI and Large Language Models (LLMs), giving me exposure to modern AI technologies alongside backend development.



Currently, I am looking for an opportunity where I can work on large-scale payment systems, deepen my understanding of financial technology and system design, and contribute to building reliable, secure, and scalable payment and banking solutions.



**How Bill Payment Works?**

Customer

Customer logs into Internet Banking. Visit The SADAD Bill Payment Module

&#x20;   │

&#x20;   ▼

Internet Banking / Mobile Banking

&#x20;   │

&#x20;   ▼

Bill Payment Module

Customer selects biller (Saudi Electricity/Telecom/Water Authority)

&#x20;   │

&#x20;   ▼

Validate Customer

Fetch the Bill by Consumer Number/Mobile Number

From the Bank Interface Bill details use to get fetch and displayed

Amount Due

Due Date

Customer Name

Bill Number

&#x20;   │

&#x20;   ▼

Customer Confirms Payment

Select the account from which amount to be debited on selection of the account balance used to get fetch and displayed

Now application performs validations

Account Active?

Balance Available?

Transaction Limit?

Beneficiary Valid?

&#x20;   │

&#x20;   ▼

Maker-Checker / Authorization

&#x20;   │

&#x20;   ▼

Core Banking Account Debit

&#x20;   │

&#x20;   ▼

Payment Gateway / Bill Aggregator

(SADAD / BBPS / NPCI)

&#x20;   │

&#x20;   ▼

Biller

(Electricity, Water, Telecom)

&#x20;   │

&#x20;   ▼

Payment Response

Notify the customer

&#x20;   │

&#x20;   ▼

Update Transaction Status

&#x20;   │

&#x20;   ▼

Receipt Generation



**What is MCP (Model Context Protocol)?**

MCP is an open protocol that allows AI models to securely access external tools and data.

Think of it as a standard interface between AI and external systems.

Instead of only answering from its internal knowledge, the AI can:

Read files

Query databases

Access APIs

Retrieve documents



Retrieval-Augmented Generation (RAG), vector databases



**Develop Chat App using Spring AI:**

To build a chat application using Spring AI, the frontend sends the user's message to a Spring Boot REST API. The controller forwards the request to a service, which uses Spring AI's ChatClient to construct a prompt and send it to an LLM such as OpenAI or Gemini. Spring AI manages authentication, request formatting, and response parsing. The generated response is returned to the frontend and displayed to the user. For enterprise applications, we can extend this by adding chat memory to preserve conversation context, Retrieval-Augmented Generation (RAG) to answer questions using company documents, and tool calling so the AI can invoke backend services or databases to provide real-time, personalized responses.

