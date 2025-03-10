# RAG Chatbot in AmazonBedrock

**RAG (Retrieval Augmented Generation) chatbot** is an AI-powered chatbot that enhances AI language models by incorporating documentation as a data source. This technique enables the chatbot to provide accurate and up-to-date responses, even if the required information is the latest or unavailable online. While non-RAG chatbots rely on pre-trained data and may struggle to offer current or specialized knowledge, the RAG chatbots can retrieve information from a specific knowledge base or external sources. This makes RAG chatbots particularly useful for applications, where up-to-date information is critical, such as legal or government updates, product releases, or personalized content.

<table>
  <tr>
    <!-- Left Side -->
    <td style="vertical-align: top; width: 50%;">
      <img src="https://github.com/user-attachments/assets/53763376-8553-4a0e-ad1b-76f29390e48c" width="100%" />
    </td>
    <!-- Right Side -->
    <td style="vertical-align: top; width: 50%;">
      <img src="https://github.com/user-attachments/assets/95fbb0cd-c9d9-4756-9e9e-2175cfce71b3" width="100%" />
    </td>
  </tr>
</table>

       
## Table of Contents
- [Used Tools and Concepts](#used-tools-and-concepts)
- [Objectives](#objectives)
- [Workfkow](#workflow)
- [Document](#document)
- [Demo](#demo)
- [Test Results](#test-results)
- [License](#license)

## Used Tools and Concepts: 
![AWS](https://img.shields.io/badge/AWS%20-%20?style=for-the-badge&logo=AmazonWebServices&logoColor=FF9900&logoSize=auto&color=232F3E)
![Amazon Bedrock](https://custom-icon-badges.demolab.com/badge/Amazon%20Bedrock%20-%20?style=for-the-badge&logo=amazon-bedrock&color=01a88d)
![Amazon S3](https://img.shields.io/badge/Amazon%20S3%20-%20?style=for-the-badge&logo=AmazonS3&logoColor=white&color=%23569A31)
![Amazon OpenSearch Service](https://custom-icon-badges.demolab.com/badge/Amazon%20OpenSearch%20Service%20-%20?style=for-the-badge&logo=amazon-opensearch&color=884df7)

The AWS services I used in this project were Amazon Bedrock, S3, and OpenSearch Serverless. Key concepts include storing data in S3, creating a Knowledge Base, requesting access to AI models, how chatbot generates responses using AI models and Knowledge Base, and utilizing vector stores for efficient retrieval.


## Objectives
**Use Case 1** – Helping my best friend’s fiancée learn more about him

Since my best friend recently got engaged, I wanted to give them something unique, meaningful, and a little humorous gift. Then, I decided to build an application integrated with an RAG chatbot that answers questions about him, allowing his fiancée to learn more about him in a fun way. This not only makes them laugh but also helps them start their new life together with a deeper understanding.

**Use Case 2** – Getting reliable information about new updates on PR from IRCC

Whenever the Government of Canada announces new rules or updates regarding temporary residents and Permanent Residency (PR), I usually spend 15 to 30 minutes searching through multiple documents and sources to verify the information’s accuracy. I realized that the RAG chatbot could streamline this process by providing reliable updates directly from trusted sources if I could successfully integrate with public web links in the Knowledge Base. This would significantly reduce my search time while ensuring access to accurate and up-to-date information. 


## Workflow
1. **Add Data Source**
   - **Use Case 1**
     - **Store Data in S3** - Stored relevant documentation in **Amazon S3** as the chatbot's data source.
   - **Use Case 2** 
     - **Add Source URLs** - Instead of S3, selected **Web Crawler** as the data source and added source URLs.
3. **Create a Knowledge Base** - Created a Knowledge Base in **Amazon Bedrock** to enable retrieval-based AI responses.
4. **Request Access to AI Models** - Selected and requested access to specific AI models, enabling the AI models to convert search results into human-like text.
5. **Configure Vector Store** - Used **OpenSearch Serverless** for vector-based search, allowing efficient retrieval of relevant information.
6. **Sync Knowledge Base** - Synchronized the data from **S3** to the **Knowledge Base** to ensure the following three keys:
   - **Ingesting**: Bedrock takes the data from S3.
   - **Processing**: Bedrock chunks and embeds the data.
   - **Storing**: Bedrock stores the processed data in the vector store (OpenSearch Serverless).

By following these flows, the AI chatbot is transformed into the **RAG chatbot**, significantly improving its ability to generate informed responses. 


## Document
Please reference a [document](https://drive.google.com/file/d/1XI0iy7e4DZWXX6lX_3I3Uwdojo5s6tiJ/view?usp=sharing) to see more details. 


## Demo
**Use Case 1** - Wedding

<table>
   <tr>
      <!-- Left Side -->
      <td style="vertical-align: top; width: 50%;">
         <img src="https://github.com/user-attachments/assets/d93f0aa7-f96c-44b5-b744-cdaae4ee0f1e" width="100%" />
         <img src="https://github.com/user-attachments/assets/d4971f5b-3d81-4f96-b3eb-a7b11df66e94" width="100%" />
      </td>
      <!-- Right Side -->
      <td style="vertical-align: top; width: 50%;">
         <img src="https://github.com/user-attachments/assets/0caef54c-5e57-407a-b311-90f9f2980793" width="100%" />
         <img src="https://github.com/user-attachments/assets/bfaecd97-1d23-4181-aea3-0a2b45dc9f54" width="100%" />
      </td>
   </tr>
</table>

**Use Case 2** - IRCC updates

<table>
   <tr>
      <!-- Left Side -->
      <td style="vertical-align: top; width: 50%;">
         <img src="https://github.com/user-attachments/assets/0d5fb84d-5812-44f4-9616-f097740063da" width="100%" />
      </td>
      <!-- Right Side -->
      <td style="vertical-align: top; width: 50%;">
         <img src="https://github.com/user-attachments/assets/39b7d623-857e-4f52-bb6d-d8479b48b419" width="100%" />
      </td>
   </tr>
</table>


## Test Results
**Use Case 1** - Wedding 

Since their wedding is still upcoming and the application would be a surprise, I haven’t shown it to them yet. I initially stored only 5 documents, and the responses generated by the chatbot were insufficient. This is probably because the chatbot summarized the information too much, resulting in overly brief responses. After storing up to 15 documents, this issue was resolved, and the responses were well-written. However, I noticed that the response time for the same prompt increased as below: 

- 1st Prompt: **_3.26 sec_** for 5 documents → **_4.61 sec_** for 15 documents.
- 2nd Prompt: **_5.50 sec_** for 5 documents → **_5.70 sec_** for 15 documents.
- 3rd prompt: **_5.78 sec_** for 5 documents → **_6.18 sec_** for 15 documents.
- 4th prompt: **_6.80 sec_** for 5 documents → **_6.81 sec_** for 15 documents.

The average increase in response time is 0.49 seconds. This happened probably due to the larger volume of documents the AI chatbot had to process and review. Therefore, the response time might hypothetically depend on the volume of documents in S3, meaning that reducing the number of documents could improve the performance of response time. 

**Use Case 2** – IRCC updates

Previously, I spent approximately 15 to 30 minutes searching reliable sources and reading through numerous documents every time the IRCC announced new updates regarding temporary residents and PR. However, the RAG chatbot was able to provide the relevant information with reliable sources, which I spent only 5 minutes in total to verify whether the provided information was reliable. This significantly reduced my search time by **_10 to 25 minutes_**, resulting in time savings of about a minimum of **_33.33%_** to a maximum of **_83.33%_**. 


## License
This project is licensed under the MIT License. See the [LICENSE](https://github.com/Ryo-samuraiJP/RAG-Chatbot-in-AmazonBedrock/blob/main/LICENSE.md) file for details.
