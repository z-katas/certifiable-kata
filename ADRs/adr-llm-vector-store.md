# Vector Store Decision

Date: [2025-02-14]

## Status

Accepted

## Context

The platform needs a vector store to efficiently store and retrieve vectorized candidate and job description data. The vector store will be used for fast similarity searches, enabling key features such as candidate matching, bias analysis, and semantic retrieval. The solution must balance scalability, query performance, integration ease, and the ability to handle a growing dataset of anonymized candidate information.

### Alternatives

1. **ChromaDB**: A vector store designed for high-performance, open-source, and easy integration, with specialized support for retrieval-augmented generation (RAG) and semantic search.
2. **FAISS**: A popular, open-source library by Facebook for fast similarity search and clustering of dense vectors, well-suited for large-scale datasets but lacks native cloud capabilities.
3. **Pinecone**: A fully managed, cloud-native vector store with high scalability and fast similarity search, but with higher operational costs and reliance on external services.


![vector store](/assets/vector-store.png "vector store")

### PrOACT

**Problem**: Choose the most appropriate vector store to store and retrieve vectors efficiently, ensuring low-latency, high-accuracy searches, and support for scaling needs.

**Objectives**:

- Ensure fast, low-latency similarity search for semantic candidate matching.
- Minimize complexity and overhead in setup and operations.
- Support large-scale datasets and real-time updates as new candidates are added.
- Maintain privacy and security for sensitive candidate information.

| **Component**   | **ChromaDB**                                                                                       | **FAISS**                                                                                                              | **Pinecone**                                                                                            |
| --------------- | -------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------- |
| **Latency**     | Moderate latency, optimized for retrieval-augmented tasks.                                         | Low latency for large datasets, highly optimized for performance.                                                      | Very low latency, cloud-native infrastructure provides fast search speeds.                              |
| **Computation** | Moderate computational overhead; good balance between speed and resource usage.                    | High computational power required, especially for large datasets; highly performant but resource-intensive.            | Low computational overhead due to managed cloud infrastructure, with optimization for high performance. |
| **Cost**        | Low cost, open-source with self-hosting options; some potential scaling costs with large datasets. | Low cost as it's open-source, but operational costs can increase with the need for complex infrastructure and scaling. | High cost, as it's a fully managed service with premium features for scalability and performance.       |

## Decision

We will adopt **ChromaDB** as the vector store. ChromaDB provides the best balance of flexibility, ease of integration, and performance, especially for retrieval-augmented tasks. While scaling considerations will need to be revisited as data grows, the open-source nature of ChromaDB allows for custom optimizations without incurring high operational costs. It also aligns well with privacy and security needs, as it can be managed on-premises or in private cloud environments.

## Tradeoffs - Mitigations

- **Scalability**: ChromaDB might need further optimizations as data scales. To mitigate this, we will monitor the platform’s performance and integrate with distributed indexing solutions if necessary.
- **Complexity**: ChromaDB’s setup is simpler, but we will still need to ensure it is optimized for use case. We will address this by leveraging ChromaDB’s community and documentation for best practices.
- **Cost**: ChromaDB, being open-source, offers lower operational costs compared to others. We will mitigate potential hidden scaling costs by proactively monitoring usage patterns and preparing for custom scaling solutions if necessary.
- **Performance**: While FAISS offers slightly better performance in large-scale environments, we expect ChromaDB’s optimizations for retrieval-augmented generation to meet needs. Regular performance benchmarking will ensure we stay on target.
- **Data Privacy**: ChromaDB allows on-premises or private cloud deployment, mitigating concerns about third-party data storage, which is crucial for handling sensitive candidate information.