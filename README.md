Local Environment for RAGFlow

## Introduction

This repository contains an exercise project designed to guide you through the process of setting up a local version of [RAGFlow](https://github.com/infiniflow/ragflow), an open-source, state-of-the-art framework for Retrieval-Augmented Generation (RAG). RAGFlow combines sophisticated search and language generation to provide efficient and high-quality responses by integrating retrieved information seamlessly into generative models.

The purpose of this exercise is to introduce you to the foundational components of RAGFlow, focusing on configuring, running, and enabling advanced features in a local environment. By completing this hands-on exercise, you will gain deeper insights into the internal mechanics and architecture of RAGFlow, enabling easier customization and optimization for future use cases.

This exercise is structured as a step-by-step guide that includes defining the computing environment, setting up services with Docker Compose, configuring the RAGFlow system.

## Overview of the Lab Exercise

The lab exercise is designed to be beginner-friendly, with clear instructions to help you successfully complete each step. Below is an outline of the main topics covered in this project:

1. **Define the Environment**:
   Set up a local environment suitable for running RAGFlow, including installing necessary tools, libraries, and dependencies.

2. **Start Required Services Using Docker Compose**:
   Deploy RAGFlow's core services and dependencies in a seamless manner using Docker Compose.

3. **Configure the RAGFlow System**:
   Customize RAGFlow's configuration files for your use case and ensure all necessary options are properly set.

By the end of the exercise, you will have a fully functioning local instance of RAGFlow and a solid understanding of its core components. This knowledge will prepare you for exploring more advanced capabilities or deploying RAGFlow in production-ready environments.

---

## Prerequisites

Before starting this exercise, ensure you have the following installed on your local machine:

- **Docker**: Version 20.10 or newer  
  [Download Docker](https://www.docker.com/products/docker-desktop/)
- **Docker Compose**: Version 2.x or newer  
  [Install Docker Compose](https://docs.docker.com/compose/install/)
- **Python**: Version 3.8 or newer  
  [Get Python](https://www.python.org/downloads/)
- **A Text Editor or IDE**: Any editor (VS Code, PyCharm, etc.) with YAML and Python syntax support.

Additionally, the exercise assumes a basic understanding of Docker, Python, and YAML configuration files.

---

## Local Setup

In the following steps we will be configuring and launching the RAGFlow system.

We will be using `ragflow:v0.20.3-slim`, which is the RAGFlow Docker image without embedding models. We will be connecting RAGFlow to OpenAI models.


# Step 1: Clone the Repository
The first step of this exercise is to set up the foundational files for the RAGFlow system by cloning the repository to your local machine. Cloning the repository gives you access to all the necessary configuration files, scripts, and setup tools that you’ll use throughout the exercise.

First, clone this repository to your local machine:

```bash
git clone  https://github.com/AdvancedNLP/lab-ragflow.git
cd lab-ragflow
```

---

## Conclusion of the Step
Congratulations! You’ve successfully completed the first step. You now have a local copy of the RAGFlow repository, which contains all the files you’ll need for this exercise. With this, you’re ready to move on to the next step and begin defining the environment for your RAGFlow setup. Let’s continue!

---

# Step 2: Starting Required Services with Docker Compose

RAGFlow depends on several backend services to function properly, including a database for document storage, a vector search engine, an object storage service, and the main RAGFlow server itself. Instead of installing and running each service individually, we will use Docker Compose to quickly and easily start all the required services in isolated containers.

Docker Compose is a tool that lets you define and run multi-container Docker applications. It simplifies managing and networking between services, saving you time and effort.

This step ensures that your local environment is up and running with all the necessary services before we proceed with configuring and using RAGFlow.

1. **Navigate to the `docker` Directory**:  
The RAGFlow project provides a pre-configured `docker-compose.yaml` file located in the `docker/` directory. Open your terminal and change into this directory as follows:

```bash
cd docker
```

2. **Start All Services**:  
Use the `docker-compose` command to bring up all the services defined in the `docker-compose.yaml` file:
```bash
docker-compose up -d
```
The `-d` flag ensures the containers run in the background.


3. **Verify the Running Services**:  
After the services start, check that they are all running by viewing the active containers:
```bash
docker ps
```

   Look for the following services in the output:
- **Elasticsearch**: This is used as the search and retrieval engine.  
- **MySQL**: This service stores and manages RAGFlow's database.  
- **Minio**: This is an object storage service used to store and retrieve large datasets, files, or blobs.  
- **RAGFlow Server**: This is the core RAGFlow API service that interacts with other components to serve requests.

  Confirm that the services are up and running without any errors in their logs. You can check a container's logs with the command:
  ```bash
  docker logs <container_name>
  ```

---

## Conclusion of the Step

Well done! At this point, all the necessary backend services for RAGFlow should be running on your local machine. By using Docker Compose, you’ve taken advantage of a robust tool to manage multiple services effortlessly. You’re now one step closer to having a fully functional RAGFlow setup. On to the next step: configuring the RAGFlow system.


# Step 3: Registering and Logging In

In this step, you will interact with the RAGFlow system for the first time by accessing its user interface. The registration and login process allows you to create an account in your local environment and securely interact with RAGFlow's features.

Since this exercise is being run locally, the signup and login process is entirely secure and isolated to your local setup. None of the information or credentials you provide here will be shared online. This step ensures that you’re ready to utilize the RAGFlow interface for additional configuration and interaction.

---

1. **Access the RAGFlow Interface**:  
   Open your browser and navigate to the following address:
   ```
   http://localhost:8080/
   ```
   This is the default port where the RAGFlow interface should be accessible. If the page does not load, ensure all services are running as described in the previous step.

2. **Create a New Account (Sign Up)**:  
   In the RAGFlow interface, look for the "Sign Up" option. Follow these steps to create a new account:
   - Provide a username, email address, and password in the signup form.
   - Submit the form, and your account will be created.  
   
   _Note: Since this is a local exercise, your credentials will be stored locally and are not accessible online. You can use any valid email and password combinations you prefer._

3. **Log In to Your Account**:  
   Once your account is created, use the "Log In" option on the interface to enter your username and password and gain access to RAGFlow. If the login is successful, you will be redirected to the RAGFlow dashboard or main interface.

---

## Conclusion of the Step

You’ve successfully signed up and logged into your RAGFlow instance. At this point, you have full access to the RAGFlow user interface and are ready to explore its features further. With these credentials, you can now start configuring and testing RAGFlow in the upcoming steps. Let's keep going!

# Step 4: Model Setup

In this step, you’ll configure the models that RAGFlow will use to perform its retrieval-augmented generation tasks. RAGFlow supports a wide array of model providers, but for the purpose of this exercise, we’ll be working with OpenAI’s models. 

You’ll need to set up your OpenAI API key within the RAGFlow interface and choose specific models for both the chat and embedding components. This setup allows RAGFlow to utilize OpenAI's models to generate responses and perform embedding operations.

---

1. **Access the Model Providers Section**:  
   Navigate to the Model Providers settings by following these steps:  
   - Log in to the RAGFlow interface (if you haven’t already). 
   - Go to the **Profile** page and click on the **Model Providers** tab.  
   Alternatively, you can directly go to this URL:  
   ```
   http://localhost:8080/user-setting/model
   ```

2. **Choose a Model Provider**:  
   You’ll see a list of available model providers. Locate and select the **OpenAI Models** option because that’s the provider we’ll be using for this exercise.

3. **Add a Model**:  
   Click on the **Add Model** button to configure OpenAI as your model provider.

4. **Enter Your OpenAI API Key**:  
   You’ll need to provide your OpenAI API key.  
   - Generate an API key by logging into your OpenAI account and navigating to the API Key settings at the following link:  
     [https://platform.openai.com/settings/organization/api-keys](https://platform.openai.com/settings/organization/api-keys)  
   - Copy the generated API key and paste it in the required field within the RAGFlow interface.
   - Leave the Base-URL empty
   - Save the configuration once you’ve entered the key.

5. **Set Default Models**:  
   Once you’ve added the OpenAI API key, you’ll need to configure the default models for both the chat responses and the embedding functionality:
   - In the **Model Providers** section, click on the **Set Default Models** button located in the top-right corner of the page.
   - For the **Chat Model**, select `gpt-4.1` from the dropdown menu.
   - For the **Embedding Model**, select `text-embedding-3-small`.  
   Click **Save** to confirm your changes.

---

## Conclusion of the Step

Fantastic! You’ve successfully configured your RAGFlow instance to use OpenAI’s advanced GPT-based models for generating responses and embeddings. With `gpt-4.1` set as the chat model and `text-embedding-3-small` as the embedding model, your RAGFlow system is now ready to perform its primary functions.  

With your models set up and ready, let’s proceed to the next step of the setup process!

# Step 5: Creating a Knowledge Base  

A knowledge base is the core component of RAGFlow's retrieval-augmented generation system. It serves as the repository where relevant documents are stored, processed, and indexed. In this step, you’ll create a knowledge base, upload a document, and trigger its ingestion. The ingestion process breaks the document into smaller, manageable chunks, which are then indexed for efficient retrieval. By the end of this step, you’ll have a functional knowledge base ready for RAGFlow to use.  

---

1. **Access the RAGFlow Dashboard**:  
   Navigate back to the main RAGFlow page by visiting:  
   ```
   http://localhost:8080/
   ```

2. **Create a New Knowledge Base**:  
   - On the RAGFlow interface, click on the **"Dataset"** button located in the main menu.  
   - Select the **"Create knowledge base"** option.  
   - Provide a name for your knowledge base (e.g., “My First Knowledge Base”).  
   - Hit the **"Save"** button to create the knowledge base.

3. **Upload a PDF File to the Knowledge Base**:  
   - Inside your newly created knowledge base, click on the **"Add file"** button.  
   - Choose a small PDF file from your local machine and upload it.  

4. **Ingest the Document**:  
   - After uploading the file, you’ll see it listed in the document table. Find the **"Play button"** located next to the file entry and click it to start the ingestion process.  
   - The document will be split into smaller chunks and processed for retrieval purposes.  

5. **Monitor the Ingestion Process**:  
   - While the ingestion process runs, monitor the status by hovering your mouse over the small colorful dot next to the document name.  
   - The time required for ingestion depends on the document size and your hardware resources.

6. **View the Processed Document**:  
   - Once the ingestion is complete, click on the document's name in the list to view the chunk results. This will show you the segmented parts of the document that RAGFlow has indexed and is ready to use for retrieval.

---

## Conclusion of the Step  

Excellent! You’ve now created your first knowledge base and successfully ingested a document into RAGFlow. The document's processed chunks are now searchable, forming the foundation for the retrieval-augmented generation functionality. You’re ready to move forward in exploring and optimizing your RAGFlow setup. Onward to the next step!


# Step 6: Creating a Chat to Interact with the Knowledge Base  

In this final step, you’ll set up a chat interface in RAGFlow to interact with the knowledge base you created earlier. This feature allows you to ask questions about the documents you’ve ingested and receive responses powered by the retrieval-augmented generation process. By connecting a chat to your knowledge base, you can test and experience how RAGFlow retrieves relevant information and generates meaningful responses.  

---

1. **Access the RAGFlow Dashboard**:  
   Navigate back to the RAGFlow landing page:  
   ```
   http://localhost:8080/
   ```

2. **Create a New Chat**:  
   - In the RAGFlow interface, click on the **"Chat"** tab from the main menu.  
   - Press the **"Create chat"** button.  
   - Provide a name for your new chat (e.g., “My First Chat”) and click **Save**.  

3. **Configure the Chat Settings**:  
   - Once your chat is created, locate the **"Chat settings"** window on the right-hand side of the chat interface.  
   - Find the **"Knowledge bases"** option in the settings menu.  
   - Use the dropdown or selection box to choose the knowledge base you created in the previous step.  
   - Click **Save** to apply the changes and link the chat with your chosen knowledge base.

4. **Start a New Chat**:  
   - In the main menu on the left-hand side, click on the **"+" button** to initiate a new chat session.  

5. **Ask Your Question**:  
   - With the new chat session running, type a question related to the document(s) you uploaded into your knowledge base.  
   - The chatbot will process your query, retrieve relevant chunks from your knowledge base, and provide a response synthesized using the configured OpenAI models.  

---

## Conclusion of the Step  

Congratulations! You’ve now successfully created a chat and linked it to your knowledge base. Your RAGFlow system is fully set up and ready to interact with, allowing you to query your uploaded documents dynamically. This marks the end of the setup process, and your RAGFlow instance is good to go.  

Feel free to experiment with different questions, upload new documents, or tweak model and chat settings. If you encounter any issues or have additional questions, revisit the relevant step or refer to the troubleshooting section of this guide.  

Thank you for completing this exercise and taking the time to explore the RAGFlow system! Happy querying!