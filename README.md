# AutoPolicy AI – AI-Powered Auto Insurance Assistant

## Project Overview

AutoPolicy AI is a proposed web application that uses artificial intelligence to help customers better understand their auto insurance policies and manage the initial steps of filing an insurance claim.

The problem this application addresses is that auto insurance policies can be difficult to understand. They often contain complicated terminology and lengthy explanations about coverage, deductibles, liability and exclusions. Customers may have trouble finding answers to basic questions or understanding what steps they need to take after an accident.

AutoPolicy AI will provide a conversational AI assistant that allows customers to ask questions in everyday language and receive clear answers based on their actual insurance policy documents. The goal is to make insurance information easier to understand, improve the customer experience and reduce the time customers spend searching through policy documents.

## Use Case and Workflow

The primary users of this application will be individuals who have auto insurance and need help understanding their policies or preparing to file a claim.

A typical workflow begins when a customer creates an account and uploads their auto insurance policy document. The application processes the document and makes its information searchable. The customer can then ask questions such as "Does my policy cover rental cars?" or "What is my collision deductible?" The AI assistant searches the uploaded policy for relevant information and generates an answer based on what it finds.

If the customer wants to report an accident, the application can also collect important details such as the accident date, vehicle information, accident location and a description of the damage. The AI then organizes this information into a structured claim summary that the customer can review.

This process improves the customer experience by making it easier to access insurance information without having to read through an entire policy document. The application will help organize information but will not make final claim approval or coverage decisions.

## AI Features to Be Implemented

### Prompt Engineering

I will create specific instructions that guide the AI assistant to respond in simple language and answer questions using the customer's policy documents. The AI will also be instructed not to make up information that is not included in the policy. If information is missing or unclear it will explain that and recommend contacting an insurance representative when necessary. This will help make responses more consistent and reliable.

### Structured Outputs

I will use Pydantic models to make sure the AI returns information in a predictable format. For example, when collecting accident information the application will organize details such as the customer's name, policy number, vehicle information, accident date, accident location, accident description and vehicle damage into specific fields.

Structured outputs will make it easier to validate, store and display information in the application without relying on unpredictable text responses.

### Retrieval-Augmented Generation and Vector Databases

I will implement Retrieval-Augmented Generation, also known as RAG, so the AI assistant can answer questions using information from the customer's actual insurance policy.

When a customer uploads a policy document the application will extract its text and divide the information into smaller sections called chunks. These sections will be converted into vector embeddings and stored in a searchable vector database. When the customer asks a question the application will retrieve the most relevant sections and provide them to the AI model to generate an answer.

I plan to use PostgreSQL with pgvector to store and search document embeddings. RAG is important because it helps ensure that responses are based on the customer's actual policy rather than general information or assumptions.

### Evaluation Frameworks

I will use LangSmith to evaluate the quality and reliability of the AI assistant. I will create a collection of sample insurance questions and expected answers to test the system.

I will evaluate whether the answers are accurate and whether the application retrieves the correct policy information. I will also check whether the AI avoids providing unsupported information and returns structured claim details in the correct format.

This will help me identify mistakes and improve the system over time.

### Observability Tools

I will use LangSmith tracing to monitor how the application processes questions and what information the retrieval system finds. I will also monitor how the AI generates responses along with response times, API errors, token usage and usage patterns.

Observability is important because it will help me troubleshoot problems and understand how the application performs. It will also help me identify areas that need improvement. Sensitive customer information will be protected and excluded from unnecessary logging.

## Technical Approach

I plan to build AutoPolicy AI using Python as the primary programming language for the backend and AI functionality. I will use the Gemini API to generate responses and process customer questions. I will also use the Google GenAI Python SDK to connect the application to Gemini.

Pydantic will be used to create structured outputs and validate the information returned by the AI. FastAPI will be used to build the backend API while React will provide the customer-facing web interface. PostgreSQL will store customer and application information. I will use pgvector to store and search the document embeddings needed for RAG.

LangSmith will help evaluate AI responses and monitor application performance. I also plan to use Cursor as a development tool to help write and debug code. GitHub will be used to store and manage the project.

At a high level the customer will interact with the application through a web interface built with React. The frontend will communicate with the Python backend through FastAPI. When a customer uploads a policy document the backend will extract and process the text before storing searchable information in PostgreSQL and pgvector.

When a customer asks a question the RAG system will retrieve relevant sections of the policy and send them to the Gemini API. Gemini will generate an answer using the retrieved information. Pydantic will validate structured responses when the application collects claim information. The final response will be sent back to the customer through the web interface. LangSmith will track and evaluate the AI operations throughout this process.

## Example Prompts and Expected Outputs

### Insurance Policy Question

**User Prompt**

Does my auto insurance policy cover damage to my vehicle if I hit another car?

**AI Instructions**

Act as an auto insurance assistant. Use only the information provided in the retrieved policy sections to answer the customer's question. Explain the relevant coverage in simple language. If the policy does not provide enough information clearly state that you cannot determine the answer and recommend contacting an insurance representative.

**Expected Output**

Your policy indicates that collision coverage may cover damage to your vehicle resulting from a collision. This is subject to your policy terms and deductible. Your listed collision deductible is $500. Please review your policy or contact your insurance representative to confirm how coverage applies to your specific accident.

The actual response will depend on the information retrieved from the customer's policy.

### Organizing an Insurance Claim

**User Prompt**

I was involved in an accident on November 2, 2026. Another car hit the passenger side of my vehicle in a parking lot. My car has damage to the passenger door.

**AI Instructions**

Extract the accident information from the customer's description. Return the information using the required structured format. Do not invent missing information. Use null for fields that the customer has not provided.

**Expected Structured Output**

json
{
  "accident_date": "2026-11-02",
  "location": "Parking lot",
  "description": "Another vehicle hit the passenger side of the customer's vehicle",
  "damage": "Damage to the passenger door",
  "vehicle_information": null,
  "claim_status": "Not yet submitted"
}

Using structured outputs will make it easier to save claim information in the application's database and display it in a consistent format.

## Evaluation Strategy

I will evaluate AutoPolicy AI by creating a test dataset containing common auto insurance questions and sample policy documents. The dataset will include questions about collision coverage, comprehensive coverage, deductibles, liability coverage, rental car coverage and accident reporting procedures.

I will use LangSmith to compare the AI's responses against expected answers and evaluate how accurately the application retrieves and uses information from the policy documents.

Some of the main evaluation metrics will include answer accuracy, retrieval accuracy, faithfulness to the retrieved documents, structured output validity, response time and error rate.

I will also manually review a sample of AI responses to identify mistakes and improve prompts. These evaluations will help ensure that customers receive useful answers supported by their insurance policy information.

## Observability Plan

I will use LangSmith to monitor and trace the AI application throughout development and testing. Each AI interaction will be tracked so I can understand how the application processes customer questions and generates responses.

I will monitor the quality of inputs and outputs, the information retrieved from the vector database, API errors, failed requests, response times, token usage and estimated API costs. I will also track how frequently the application is unable to answer a customer's question.

These traces will help me identify whether problems are caused by the prompts, document retrieval process or the language model itself. I can use this information to make improvements as the application develops. Customer policy documents and personal information will be handled securely with appropriate access controls and data minimization.

## Project Scope and Future Improvements

The initial version of AutoPolicy AI will focus on three main capabilities. These include allowing customers to upload and search their auto insurance policy documents, answering questions using RAG and Gemini, and collecting and organizing accident information into structured claim summaries.

I plan to begin by developing a basic version using sample insurance policy documents and test data. Once the main features are working I would like to expand the application by adding insurance company integrations, customer claim status tracking, support for multiple insurance policies, multilingual customer support and a dashboard that allows insurance representatives to review customer-submitted claim information.

Future versions could also include secure connections to insurance company databases. These improvements would require additional security, privacy and compliance considerations.

## Conclusion

AutoPolicy AI will demonstrate how artificial intelligence can be used to solve a real-world problem by making auto insurance information easier to understand and access.

By combining prompt engineering, structured outputs, Retrieval-Augmented Generation, vector databases, evaluation frameworks and observability tools the application will provide a practical example of how AI can be integrated into a real web application.
