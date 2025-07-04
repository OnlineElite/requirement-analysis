# Requirement Analysis in Software Development

📘 Introduction

This repository serves as a foundational resource for understanding and applying Requirement Analysis in the context of software development. It contains documentation, examples, and practical insights into how to effectively gather, analyze, and manage software requirements throughout the development lifecycle.

# What is Requirement Analysis?

Requirement Analysis is a critical phase in the software development lifecycle (SDLC) where the project team gathers, analyzes, and defines the requirements of the software product to be developed. This process ensures that all stakeholders have a clear and mutual understanding of what the system should do and how it should perform

# Why is Requirement Analysis Important?

* Clarity and Understanding: It helps in understanding what the stakeholders expect from the software, reducing ambiguity.
* Scope Definition: Clearly defines the scope of the project, which helps in preventing scope creep.
* Basis for Design and Development: Provides a solid foundation for designing and developing the system.
* Cost and Time Estimation: Facilitates accurate estimation of project cost, resources, and time.
* Quality Assurance: Ensures that the final product meets the specified requirements, leading to higher customer satisfaction.

# Key Activities in Requirement Analysis

### 1. Requirement Gathering 🗂️
   - Interviews: Conducting interviews with stakeholders to gather detailed information about their needs and expectations.
   - Surveys/Questionnaires: Distributing surveys to collect requirements from a larger audience.
   - Workshops: Organizing workshops with stakeholders to discuss and gather requirements.
   - Observation: Observing end-users in their working environment to understand their needs.
   - Document Analysis: Reviewing existing documentation and systems to understand current functionalities and requirements.
### 2. Requirement Elicitation ✍️
   - Brainstorming: Conducting brainstorming sessions to generate ideas and gather requirements.
   - Focus Groups: Holding focus group discussions with selected stakeholders to gather detailed requirements.
   - Prototyping: Creating prototypes to help stakeholders visualize the system and refine their requirements.
### 3. Requirement Documentation 📚
   - Requirement Specification Document: Creating a detailed document that lists all functional and non-functional requirements.
   - User Stories: Writing user stories to describe functionalities from the user’s perspective.
   - Use Cases: Creating use case diagrams to show interactions between users and the system.
### 4. Requirement Analysis and Modeling 📊
   - Requirement Prioritization: Prioritizing requirements based on their importance and impact on the project.
   - Feasibility Analysis: Assessing the feasibility of requirements in terms of technical, financial, and time constraints.
   - Modeling: Creating models (e.g., data flow diagrams, entity-relationship diagrams) to visualize and analyze requirements.
### 5. Requirement Validation ✅
   - Review and Approval: Reviewing the documented requirements with stakeholders to ensure accuracy and completeness.
   - Acceptance Criteria: Defining clear acceptance criteria for each requirement to ensure they meet the expected standards.
   - Traceability: Establishing traceability matrices to ensure all requirements are addressed during development and testing.

# Types of Requirements

### 1. Functional Requirements

Functional requirements describe what the system must do or the specific actions and functionalities it should provide to users.

#### For the Hotel Management Service:
   - Hotel managers must be able to manage their hotel's related information.
   - Hotel managers must have a separate portal to access and update their hotel data.
#### For the Customer Service (Search + Booking):
   - Customers must be able to search for hotels.
   - Customers must be able to book a hotel.
   - The customer application must display content such as nearby hotels, recommendations, and offers.
   - The booking service must interact with a third-party payment service.
#### For the View Booking Service:
   - The system must show all current booking details to the user.
   - The system must show all old booking details to the user.
   - Both managers and customers must be able to use this service.
#### General Functionalities (Notifications):
   - The system must be able to send notifications to customers or managers.
   - For example, a notification must be sent to the manager whenever a customer books a hotel.
   - For example, if new offers become available, customers must be notified

### 2. Non-functional Requirements

Non-functional requirements describe how the system should perform its functions, focusing on qualities such as performance, reliability, security, scalability, and usability.

#### Performance, Scalability, and Availability:
   - The system must be able to handle a high amount of user traffic.
   - The system must provide a smooth flow from hotel listing to booking and payments.
   - The system must follow a micro-service architecture to divide tasks into small chunks for better management of high traffic.
   - The system must use load balancers to distribute requests efficiently to the desired servers.
   - The Hotel DB cluster must follow a master-slave architecture to reduce the load on the database.
     - The master database must be used for write operations.
     - Slave databases must be used for read operations only.
     - Data must sync from the master database to slave databases after every write operation.
   - A CDN (Content Delivery Network) must be used to ensure fast delivery of Internet content.
   - A caching system like Redis must be used to store temporary data. This should reduce the load on the database and reduce the API response time, and reduce the loading time on the app side.
#### Data Management and Consistency:
   - A Messaging Queue System (like Kafka or RabbitMQ) must be used for further data processing and inter-service communication.
   - The search service must retrieve data from Elasticsearch, which is a NoSQL Database optimized for its search engine functionality.
   - Cassandra (a NoSQL database) must be used for data archival, as it is good at handling a high volume of data that increases over time.
   - Any changes made in the database must be sent to the messaging queue for consumers to process and store in systems like Cassandra for archival.
#### Analytics Capabilities:
   - An Apache Streaming service must take data from the messaging queue and store it in Hadoop for Big Data analysis.
   - Big Data analysis must be used for purposes such as business analysis, finding potential customers, and audience categorizations.

# Use Case Diagrams

### What are Use Case Diagrams?
* Use case diagrams show how different users (actors) interact with the system to achieve specific goals (use cases).
### Creating Use Case Diagrams:
* Identify actors (e.g., guest, registered user, admin).
* Define use cases (e.g., search properties, book property, manage listings).
* Draw interactions between actors and use cases.
### Benefits of Use Case Diagrams:
* Provide a clear visual representation of system functionalities.
* Help in identifying and organizing system requirements.
* Facilitate communication among stakeholders and development team.

![image alt](https://github.com/OnlineElite/requirement-analysis/blob/main/alx-booking-uc.png?raw=true)

# Acceptance Criteria

Objective: Establishing clear criteria for feature completion.

### What is Acceptance Criteria?
* Acceptance criteria are conditions that a feature must meet to be accepted by the stakeholders.
### How to Define Acceptance Criteria:
* Be specific and measurable.
* Include functional and non-functional aspects.
* Example for Booking System: “Users should be able to select available dates, confirm booking, and receive a confirmation email within 2 minutes.”
### Benefits of Acceptance Criteria:
* Ensure all parties have a clear understanding of feature requirements.
* Provide a basis for testing and validation.
* Help in maintaining quality and meeting user expectations.

### Exemple : Feature: Payment Process and Booking Confirmation

#### Criterion 1: Successful Payment and Booking Confirmation
   - Given that a customer has selected a hotel, provided the necessary details, and reached the payment page.
   - When the customer enters valid payment information and the third-party payment service successfully processes the payment.
   - Then the system must:
     - Display a clear and detailed booking confirmation message to the customer (This functionality is implicit given the completion of a booking).
     - Record the booking in the booking database cluster.
     - Send a notification to the hotel manager regarding the new booking.
     - Ensure that the API response time for booking confirmation is minimal to guarantee a "smooth flow".
     - The booking data must be sent to the messaging queue for further processing and archival in Cassandra.

#### Criterion 2: Payment Failure
   - Given that a customer is on the payment page.
   - When the customer attempts to finalize the booking, but the third-party payment service returns a payment failure.
   - Then the system must:
     - Display a clear and informative error message to the customer, indicating the payment failure.
     - Not confirm the booking.
     - Not send a notification to the hotel manager regarding a new booking.

#### Criterion 3: Performance and Resilience of the Payment Page
   - Given a high amount of users simultaneously accessing the payment page.
   - When the system processes payment requests.
   - Then the system must:
     - Maintain a fast loading time for the payment page, utilizing a "caching system like Redis" to "store temporary data" to "reduce the load on the database", "reduce the API response time", and "reduce the loading time on the app side".
     - Effectively manage the "high amount of user traffic" by distributing requests via "load balancers" to the appropriate servers.
     - Ensure continuous availability of the payment service, even under high load.
