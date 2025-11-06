# 🚀 Deploying GPT-4o from Azure OpenAI 

This guide explains how to **deploy a GPT-4o model using Azure OpenAI Service** and make it accessible for your applications via API calls or LangChain integration.

---

## 🧠 Overview

Azure OpenAI provides access to OpenAI models (like `gpt-4o`, `gpt-4`, and `gpt-3.5-turbo`) hosted on Microsoft Azure’s secure cloud infrastructure.  
You can deploy these models, manage access, and integrate them into your apps using the Azure portal or SDKs.

---

## 🪜 Step 1: Create an Azure OpenAI Resource

1. Sign in to the [Azure Portal](https://portal.azure.com/).  
2. Click **Create a resource  → Azure OpenAI**.  

Once deployed, you’ll have access to your **Azure OpenAI resource**.

---

## 🤖 Step 2: Deploy a Model (e.g., GPT-4o)

1. Go to your Azure AI Foundry.
2. Go to Azure OpenAI
3. go to Azure AI foundry portal (**explore Azure AI Foundry portal**)
4. Select **Model deployments** → **Create new deployment**.  
5. Under **Model**, select `gpt-4o`.  
6. Click **Deploy**.

It will appear in your list of deployed models.  
This deployment name will be used later in your API calls.

---

## 🔐 Step 3: Get Your API Keys and Endpoint

1. From the same Azure OpenAI resource, open the **Keys and Endpoint** tab.  
2. Copy:
- **Endpoint** → looks like `https://<your-resource-name>.openai.azure.com/`
- **API Key** → used to authenticate your requests

Keep these secure! 🔑

---

## 💻 Step 4: Test the Deployment via Python in your VS Code.

Run the below commands 


```bash
# 1. Create a new isolated virtual environment named 'env'
python -m venv env

# 2. Activate the virtual environment (for Windows)
env\Scripts\activate

# 3. Install the core libraries
# python-dotenv: for loading secret keys from a .env file
# langchain: the main framework for orchestrating LLM workflows
pip install python-dotenv langchain

# 4. Install the specific LangChain package for connecting to OpenAI and Azure OpenAI models
pip install langchain-openai
```
---

---
<img width="778" height="572" alt="image" src="https://github.com/user-attachments/assets/09455df7-2088-4d80-b7ec-2124416d94ef" />

<img width="1175" height="363" alt="image" src="https://github.com/user-attachments/assets/14cfc4b8-7dbe-4463-a13d-d8496b5aa767" />

<img width="1146" height="357" alt="image" src="https://github.com/user-attachments/assets/a720cecf-264d-4027-8c88-1e82dec243d7" />

---
# Next step 

- go to https://docs.langchain.com/oss/python/integrations/chat/azure_chat_openai

and copy the below 

<img width="1383" height="807" alt="image" src="https://github.com/user-attachments/assets/99a191d1-061b-496c-874f-aee8ad8bd1bd" />

- Create a new file for your chat.py
- and a new file for .env
- go to your .env file and add the below values
<img width="921" height="250" alt="image" src="https://github.com/user-attachments/assets/107470a4-9155-4e14-90e8-bb9a9f58bb98" />


- Next, update the Python code you copied from the LangChain documentation as follows.

```python
from dotenv import load_dotenv
from langchain_openai import AzureChatOpenAI
from langchain.prompts import ChatPromptTemplate

# 1. Load environment variables from .env file
# This securely loads credentials like AZURE_OPENAI_ENDPOINT and AZURE_OPENAI_API_KEY
load_dotenv()

# 2. Initialize the Azure OpenAI LLM
# This creates a client object to interact with your specific model deployment
llm = AzureChatOpenAI(
    azure_deployment="gpt-4o",       # <-- Replace with your deployment name
    api_version="2024-02-01" # <-- Use a valid Azure OpenAI API version
)

# 3. Get user input from the command line
user_input = input("You: ")

# 4. Create a prompt template
# This structures the conversation for the model, defining system and human roles
prompt = ChatPromptTemplate.from_messages([
    ("system", "You are a helpful AI assistant. Please assist the user with their query."),
    ("human", "{user_input}")
])

# 5. Create a chain to combine the prompt and the LLM
# This is a more modern and flexible way to handle the flow in LangChain
chain = prompt | llm

# 6. Invoke the chain with the user's input
# LangChain handles formatting the prompt and calling the model
response = chain.invoke({"user_input": user_input})

# 7. Print the model's reply
# The actual text content is in the `content` attribute of the response
print("AI:", response.content)

```


- the next step is to give the following command


```python
python chat.py
```


  
# 🤖  happy chatting !!!


<img width="1158" height="1024" alt="image" src="https://github.com/user-attachments/assets/94d48873-0d1a-4c6f-bc9b-e1daca26574e" />
