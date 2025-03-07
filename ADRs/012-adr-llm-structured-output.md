# ADR-012: Enforcing Structured LLM Outputs

Date:  [2025-02-20]

## Status

Accepted

## Context

Our Automatic Grading System requires LLM responses to follow strict structured formats (e.g., JSON) for reliable downstream processing. Several approaches exist to enforce structure, including native output parsers, schema validation libraries, and instruction-based methods. This ADR compares these options in a concise table and recommends the best option.

## Alternatives Comparison

| Approach                               | Pros                                                                                       | Cons                                                                                    |
| -------------------------------------- | ------------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------- |
| LangChain Output Parsers               | Seamless integration with current orchestration; mature and community-supported            | Reactive parsing; may require additional tuning for complex outputs                     |
| Pydantic-Based Schema Validation       | Robust, strict schema enforcement; strong type checking                                    | Requires extra steps to transform raw LLM output; increases integration complexity      |
| Standalone LLM Output Parser Libraries | Tailored for LLM outputs; specialized error handling                                       | Limited documentation/community; may need additional glue code                          |
| Custom Parser Implementation           | Maximum control and customization                                                          | High development/maintenance overhead; increased time-to-market                         |
| Instructor Framework (Instructor.ai)   | Proactive, instruction-based guidance; explicit prompts reduce variability; example-driven | Newer framework with less real-world validation; relies on effective prompt engineering |

## PrOACT

• Problem: Ensure LLM outputs consistently adhere to a defined structure  
• Objectives: Proactively enforce structured outputs to minimize post-processing and integration issues  
• Alternatives Considered: LangChain Output Parsers, Pydantic-Based Schema Validation, Standalone Libraries, Custom Parser, Instructor Framework  
• Constraints: Must integrate with our Python-based ecosystem, utilize limited engineering resources, and allow flexibility for schema evolution

## Decision

We recommend adopting the [Instructor framework](https://github.com/instructor-ai/instructor). Its instruction-based approach proactively guides LLM responses to the desired structured format and minimizes downstream processing issues. This solves many challenges inherent in reactive parsing and custom validation while maintaining integration simplicity with our existing system.

## Tradeoffs - Mitigations

### Maturity and Community Support

- Mitigation: Implement an abstraction layer for output processing to allow substituting or augmenting Instructor with other methods if needed.

### Integration Complexity and Prompt Engineering

- Mitigation: Begin with a prototyping phase to optimize prompt design and document best practices; combine with fallback validation (e.g., LangChain or Pydantic) if necessary.

This approach leverages the innovative benefits of the Instructor framework to achieve consistent, structured LLM outputs while allowing for future flexibility and mitigation of identified risks.
