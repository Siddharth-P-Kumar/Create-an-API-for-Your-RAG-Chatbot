<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Create an API for Your RAG Chatbot

**Project Link:** [View Project](http://learn.nextwork.org/projects/ai-rag-api)

**Author:** siddharthpk nextwork  
**Email:** siddharthpknextwork@gmail.com

---

## How I Built an API for My RAG Chatbot

![Image](http://learn.nextwork.org/mischievous_red_fierce_pony/uploads/ai-rag-api_r4s5t6u7)

---

## Introducing Today's Project!

In this project, I will demonstrate how to build an API for a RAG chatbot using Amazon Bedrock and Amazon S3. I'm doing this project to learn how to make my chatbot accessible to any application, moving beyond the AWS Console or terminal, and to understand how to store knowledge in S3, set up the chatbot's brain with Bedrock and AI models, build a web API, and secure/test it.

### Tools and concepts

The services I used were FastAPI for API creation, Amazon Bedrock for the RAG chatbot functionality and direct AI model interaction, Amazon S3 for storing data for the Knowledge Base, AWS IAM for managing access keys and permissions, and AWS CLI for interacting with AWS services. Key concepts I learnt include creating and extending APIs with different endpoints (/bedrock/query and /bedrock/invoke), the difference between Retrieval-Augmented Generation (RAG) and direct AI model communication, the role of Knowledge Bases in Bedrock, using environment variables for secure configuration, and troubleshooting common API errors.

### Project reflection

This project took me approximately 2 hours. The most challenging part was troubleshooting the missing MODEL_ID environment variable for the new API endpoint, which initially prevented direct AI model communication. It was most rewarding to successfully resolve that error and then validate the new endpoint by querying it directly, seeing the API work as intended.

I chose to do this project today because I wanted to deepen my understanding of how to extend API functionality beyond basic RAG, specifically by implementing direct AI model communication. This project allowed me to explore making my chatbot more versatile for various applications. Something that would make learning with NextWork even better is providing more advanced 'Secret Missions' that encourage deeper technical exploration and independent problem-solving, similar to the troubleshooting challenges I encountered with environment variables.

---

## Setting Up The Knowledge Base

To set up my Knowledge Base, I used S3 to store the documents and information that my chatbot will learn from. The documents I uploaded contain information about the training materials for my chatbot, which will serve as the source of knowledge for its responses.

Amazon Bedrock is an AWS service that gives you access to AI models to bring into your applications. I created a Knowledge Base in Bedrock to act as my chatbot's personal library, storing all the information it needs to answer questions.

My chatbot also needs access to two AI models to convert the raw search results from the Knowledge Base into human-like text responses. I then synchronized my data from S3 to the Knowledge Base because this process loads the data, converts my documents into embeddings, and makes them searchable for the chatbot.

![Image](http://learn.nextwork.org/mischievous_red_fierce_pony/uploads/ai-rag-api_1u2v3w4x)

---

## Running CLI Commands Locally

---

## Running Bedrock Commands

When I first ran a Bedrock command, I ran into a ValidationException error because I needed to provide values for the knowledge_base_id and model_arn.

To find the required values, I had to find the Knowledge Base ID from the console and run a command in Local terminal to find the Model ARN. The Bedrock command ran successfully and showed me the chatbot's response to my query.

---

## Creating an API

An API (Application Programming Interface) is like a restaurant menu – it lists all the ways other applications can interact with your service. The API I'm creating will connect my chatbot to Amazon Bedrock and allow me to test it through web requests. This will be helpful for opening up endless possibilities for how others can interact with my chatbot, such as building a web interface, adding it to a mobile app, or integrating it with other platforms.

The API code has three main sections: setting up the Python development environment, configuring the connection to Amazon Bedrock using environment variables, and defining the query endpoint to interact with the chatbot.

![Image](http://learn.nextwork.org/mischievous_red_fierce_pony/uploads/ai-rag-api_w7x8y9z0)

---

## Installing Packages

To run the API, I had to install requirements like fastapi, boto3, dotenv, and os from the requirements.txt file. These packages are important because fastapi is the web framework for building the API, boto3 is the AWS SDK for Python used to connect to AWS services like Bedrock, and dotenv and os are used for loading environment variables.

![Image](http://learn.nextwork.org/mischievous_red_fierce_pony/uploads/ai-rag-api_a8b9c0d1)

---

## Testing the API

When I visited the root endpoint, I saw {"message": "Welcome to your RAG chatbot API"}. This confirms that my API is running and accessible.

![Image](http://learn.nextwork.org/mischievous_red_fierce_pony/uploads/ai-rag-api_i6j7k8l9)

---

## The Query Endpoint

The query endpoint connects an app with your Amazon Bedrock Knowledge Base. I tested the query endpoint by visiting http://127.0.0.1:8000/bedrock/query?text=What%20is%20NextWork in my browser. The response was a Parameter validation failed error, indicating that my API is not correctly configured with the Knowledge Base ID and Model ARN.

Looking at the API code, I can see that the API calls for environment variables because it uses the os package to import sensitive information like the Knowledge Base ID and Model ARN. This is a better practice than hardcoding these values directly into the code, as it keeps them secure and allows for easier configuration changes. To resolve the error in my query endpoint, I need to create a .env file in my project directory and add the AWS_REGION, KNOWLEDGE_BASE_ID, and MODEL_ARN to it, replacing the placeholders with my actual values.

![Image](http://learn.nextwork.org/mischievous_red_fierce_pony/uploads/ai-rag-api_r4s5t6u7)

---

## Extending the API

In a project extension, I decided to extend my API by adding a new endpoint that allows direct communication with the AI model, bypassing the Knowledge Base. This enables my chatbot to answer general knowledge questions, making the API more versatile for other applications. Changes to the API code include running a modified version of the API to facilitate this direct AI model interaction and updating environment variables to support this new functionality.

I initially ran into an error with the new endpoint because the MODEL_ID environment variable was missing. This variable is crucial for the API to communicate directly with the AI model without using the Knowledge Base. Once I fixed it by adding the MODEL_ID to my .env file, I validated the new endpoint by re-running the API and successfully querying it directly, receiving a correct response from the AI model.

When I use /bedrock/query, the chatbot utilizes Retrieval-Augmented Generation (RAG). This means it first searches my Knowledge Base for relevant information and then uses the AI model to generate a response based on that retrieved information. This makes the chatbot's answers accurate and grounded in my specific documents. But when I use /bedrock/invoke, the chatbot bypasses the Knowledge Base and communicates directly with the AI model. In this mode, the chatbot answers questions based on its general knowledge, without referencing my specific documents, which can sometimes lead to less accurate or unexpected responses if the question is specific to the content in my Knowledge Base.

![Image](http://learn.nextwork.org/mischievous_red_fierce_pony/uploads/ai-rag-api_u8d9e0f1)

---

---
