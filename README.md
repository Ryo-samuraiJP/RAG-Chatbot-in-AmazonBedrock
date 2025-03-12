# RAG Chatbot in AmazonBedrock

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

[日本語](https://github.com/Ryo-samuraiJP/RAG-Chatbot-in-AmazonBedrock/blob/main/README.jp.md) | [English](https://github.com/Ryo-samuraiJP/RAG-Chatbot-in-AmazonBedrock)

**RAG (Retrieval Augmented Generation) chatbot** is an AI-powered chatbot that enhances AI language models by incorporating documentation or/and source URLs as the data source. This technique enables the chatbot to provide accurate and up-to-date responses, even if the required information is the latest or unavailable online. While non-RAG chatbots rely on pre-trained data and may struggle to offer current or specialized knowledge, the RAG chatbots can retrieve information from a specific knowledge base or external sources. This makes RAG chatbots particularly useful for applications, where up-to-date information is critical, such as legal or government updates, product releases, or personalized content.

## Table of Contents

- [Used Tools and Concepts](#used-tools-and-concepts)
- [Objectives](#objectives)
- [Workfkow](#workflow)
- [Document](#document)
- [Demo](#demo)
- [Data-Driven Test Results](#data-driven-test-results)
- [License](#license)

## Used Tools and Concepts:

![AWS](https://img.shields.io/badge/AWS%20-%20?style=for-the-badge&logo=AmazonWebServices&logoColor=FF9900&logoSize=auto&color=232F3E)
![Amazon Bedrock](https://custom-icon-badges.demolab.com/badge/Amazon%20Bedrock%20-%20?style=for-the-badge&logo=amazon-bedrock&color=01a88d)
![Amazon S3](https://img.shields.io/badge/Amazon%20S3%20-%20?style=for-the-badge&logo=AmazonS3&logoColor=white&color=%23569A31)
![Amazon OpenSearch Service](https://custom-icon-badges.demolab.com/badge/Amazon%20OpenSearch%20Service%20-%20?style=for-the-badge&logo=amazon-opensearch&color=884df7)

The AWS services I used in this project were Amazon Bedrock, S3, and OpenSearch Serverless. Key concepts include storing data in S3, adding source URLs through Web Crawler, creating a Knowledge Base, requesting access to AI models, how chatbot generates responses using AI models and Knowledge Base, and utilizing vector stores for efficient retrieval.

## Objectives

**I. Use Case 1** – Personalized Q&A Chatbot

Since my best friend recently got engaged, I wanted to give them something unique, meaningful, and a little humorous gift. Then, I decided to build an application integrated with an RAG chatbot that answers questions about him, allowing his fiancée to learn more about him in a fun way. This not only makes them laugh but also helps them start their new life together with a deeper understanding.

**II. Use Case 2** – Automated Immigration Updates

Whenever the Government of Canada announces new rules or updates regarding temporary residents and Permanent Residency (PR), I usually spend 15 to 20 minutes searching through multiple documents and sources to verify the information’s accuracy. I realized that the RAG chatbot could streamline this process by providing reliable updates directly from trusted sources if I could successfully integrate with public web links in the Knowledge Base. This would significantly reduce my search time while ensuring access to accurate and up-to-date information.

## Workflow

1. **Add Data Source**
   - **Use Case 1**
     - **Store Data in S3** - Stored relevant documentation in **Amazon S3** as the chatbot's data source.
   - **Use Case 2**
     - **Add Source URLs** - Instead of S3, added source URLs as the data source through **Web Crawler**.
2. **Create a Knowledge Base** - Created a Knowledge Base in **Amazon Bedrock** to enable retrieval-based AI responses.
3. **Request Access to AI Models** - Selected and requested access to specific AI models, enabling the AI models to convert search results into human-like text.
4. **Configure Vector Store** - Used **OpenSearch Serverless** for vector-based search, allowing efficient retrieval of relevant information.
5. **Sync Knowledge Base** - Synchronized the data from **S3** to the **Knowledge Base** to ensure the following three keys:
   - **Ingesting**: Bedrock takes the data from S3.
   - **Processing**: Bedrock chunks and embeds the data.
   - **Storing**: Bedrock stores the processed data in the vector store (OpenSearch Serverless).

By following these flows, the AI chatbot is transformed into the **RAG chatbot**, significantly improving its ability to generate informed responses.

## Document

Please reference a [document](https://drive.google.com/file/d/1XI0iy7e4DZWXX6lX_3I3Uwdojo5s6tiJ/view?usp=sharing) to see more details.

## Demo

**I. Use Case 1** – Personalized Q&A Chatbot

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

**II. Use Case 2** – Automated Immigration Updates

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

## Data-Driven Test Results

**I. Use Case 1** – Personalized Q&A Chatbot

I compared response speed by testing identical prompts while storing 15 vs. 5 documents in S3.
As a result, I discovered that the response speed might hypothetically depend on the volume of
stored documents, according to the following data:

- 1st Prompt: **_4.61 sec._** (15 docs) → **_3.26 sec._** (5 docs)
- 2nd Prompt: **_5.70 sec._** (15 docs) → **_5.50 sec._** (5 docs)
- 3rd Prompt: **_6.18 sec._** (15 docs) → **_5.78 sec._** (5 docs)
- 4th Prompt: **_6.81 sec._** (15 docs) → **_6.80 sec._** (5 docs)

On average, the response speed was **_0.49 seconds faster_** when storing fewer documents. This is probably because the AI chatbot took longer to process and retrieve information from the larger volume of documents.

However, while reducing the number of documents could improve the performance of response speed, it may also negatively affect the quality of responses. Therefore, finding the right balance between speed and knowledge depth is crucial for optimizing chatbot performance.

**II. Use Case 2** – Automated Immigration Updates

I used to spend approximately 15 to 20 minutes searching for reliable sources and reading
through numerous documents every time the IRCC announced new updates regarding
immigration, especially Express Entry rules for PR. However, the RAG chatbot can now retrieve
updates directly from added source URLs and provide the relevant information with reliable
sources, reducing my search time by **_66.67_** % to **_75%_** – from **_15-20 minutes_** to only **_5 minutes_** (including the time to verify accuracy).

## License

This project is licensed under the MIT License. See the [LICENSE](https://github.com/Ryo-samuraiJP/RAG-Chatbot-in-AmazonBedrock/blob/main/LICENSE.md) file for details.
