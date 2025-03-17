# ADR-018: Vector Store Storage Strategy

## Status
**Proposed**

## Context
Our system needs to store and retrieve embeddings for different entity types, including:
- Test 1 MCQs
- Test 1 Short Answer Questions
- Test 1 Short Answer References
- Test 2 Case Study Questions
- Test 2 Case Study Section-wise References
- General Architecture Knowledge

Efficient storage and retrieval of these embeddings are crucial for optimizing search performance, ensuring relevance, and reducing computational overhead. The two primary strategies under consideration are:

## Alternatives
### 1. Single-Collection Strategy
- Store all embeddings in a single collection with metadata tags to differentiate entity types.
- Queries filter results based on metadata.
- Simplifies data management but may introduce inefficiencies in retrieval performance.

### 2. Multi-Collection Strategy
- Store embeddings in separate collections based on entity type.
- Queries target the relevant collection, reducing filtering overhead.
- More complex data management but offers potential performance benefits.

## PrOACT
### Problem Definition
Determine the optimal strategy for storing embeddings to balance retrieval efficiency, storage scalability, and system maintainability.

### Objectives
- Ensure efficient retrieval of embeddings based on entity type.
- Minimize storage redundancy and query execution time.
- Support scalability as new entity types are introduced.

### Alternatives
Discussed above.

### Consequences
#### Single-Collection Strategy
- Increased filtering complexity during retrieval.
- Potential query latency due to large collection size.
- Easier management with a unified indexing approach.

#### Multi-Collection Strategy
- Faster queries since only relevant collections are searched. 
- Higher maintenance effort due to multiple collections.
- Potential storage inefficiencies if embeddings overlap across collections.
- Storing different section references in different collections will help achieve less context window during section wise evaulation in case study grading.

### Tradeoffs
- Query performance vs. management complexity.
- Scalability for new entity types vs. initial setup effort.
- Metadata filtering overhead vs. collection-based separation.

## Decision
We will adopt a **multi-collection strategy** to optimize query performance and retrieval efficiency. Each entity type will have its own collection, reducing filtering overhead and enabling targeted retrieval.

## Tradeoffs - Mitigations
| **Risk** | **Tradeoff** | **Mitigation** |
|----------------------------------------|-------------------------------------------------|--------------------------------------------|
| **Higher Maintenance Effort** | Managing multiple collections requires extra setup | Automate collection creation and indexing |
| **Potential Storage Redundancy** | Some embeddings might appear in multiple collections | Deduplicate embeddings across collections |
| **Scalability for New Entity Types** | Adding new entities requires creating new collections | Implement dynamic collection provisioning |
| **Cross-Entity Queries Complexity** | Queries spanning multiple entity types require more logic | Implement intelligent query routing |

By implementing the multi-collection strategy, we ensure efficient, scalable, and maintainable retrieval of embeddings, optimizing the system for both current and future data needs.