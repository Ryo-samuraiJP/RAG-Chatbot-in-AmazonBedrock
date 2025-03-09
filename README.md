# RAG Chatbot in AmazonBedrock

RAG (Retrieval Augmented Generation) chatbot is an AI chatbot with a technique that enhances AI language models by providing documentation as the data source, enabling the chatbot to provide accurate and up-to-date responses, even if the required information is latest and unavailable online. 

![instruct manual & funny episode](https://github.com/user-attachments/assets/9ad8b883-b3ec-4f5b-879f-e2393519f323)

## Table of Contents
- [Used Tools and Concepts](#used-tools-and-concepts)
- [Objective](#objective)
- [Workfkow](#workflow)
- [Document](#document)
- [Demo](#demo)

## Used Tools and Concepts: 
![AWS](https://img.shields.io/badge/AWS%20-%20?style=for-the-badge&logo=AmazonWebServices&logoColor=FF9900&logoSize=auto&color=232F3E)
![Amazon Bedrock](https://custom-icon-badges.demolab.com/badge/Amazon%20Bedrock%20-%20?style=for-the-badge&logo=amazon-bedrock&color=01a88d)
![Amazon S3](https://img.shields.io/badge/Amazon%20S3%20-%20?style=for-the-badge&logo=AmazonS3&logoColor=white&color=%23569A31)
![Amazon OpenSearch Service](https://custom-icon-badges.demolab.com/badge/Amazon%20OpenSearch%20Service%20-%20?style=for-the-badge&logo=amazon-opensearch&color=884df7)

AWS services I used in this project were Amazon Bedrock, S3, and OpenSearch Serverless. Key concepts include storing data in S3, creating a Knowledge Base, requesting access to AI models, how chatbot generates responses (i.e. AI models + Knowledge Base), and vector stores. 

## Objective
Since my best friend recently got engaged to his girlfriend, I wanted to give them a gift that is something unique, meaningful, and a little humorous. Then I decided to build an application integrated with a RAG chatbot that answers questions about him so that his fiancée can learn more about him in a fun way, helping them start their new life together with laughter and deeper understanding. 

## Workflow
1. **Store Data in S3** - Stored relevant documentation in **Amazon S3** as the chatbot's data source.
2. **Create a Knowledge Base** - Created a Knowledge Base in **Amazon Bedrock** to enable retrieval-based AI responses.
3. **Request Access to AI Models** - Selected and requested access to specific AI models, enabling the AI models to convert search results into human-like text.
4. **Configure Vector Store** - Used **OpenSearch Serverless** for vector-based search, allowing efficient retrieval of relevant information.
5. **Sync Knowledge Base** - Synchronized the data from **S3** to the **Knowledge Base** to ensure the following three keys:
   - **Ingesting**: Bedrock takes the data from S3.
   - **Processing**: Bedrock chunks and embeds the data.
   - **Storing**: Bedrock stores the processed data in the vector store (OpenSearch Serverless).

By following these flows, the AI chatbot is transformed into the **RAG chatbot**, significantly improving its ability to generate informed responses. 

## Document
Please reference a document to see more details. 

## Demo
![funny story with sauna](https://github.com/user-attachments/assets/6c449522-528a-4d63-ac66-45c07c5f2df1)
![type of student](https://github.com/user-attachments/assets/9bd851f9-662c-4c22-97d2-b2737630315a)
![type of boy](https://github.com/user-attachments/assets/d3858ef7-c355-478f-b3fa-e5ce73a5364f)
![when depressed](https://github.com/user-attachments/assets/7485b7fb-04af-4126-81f9-2e73f6498298)

