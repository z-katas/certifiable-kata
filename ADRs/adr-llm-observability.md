# LLM Observability Tool Selection

## Status

Accepted

## Context

To ensure effective monitoring and evaluation of our LLM-based system at Certifiable Inc., we need an observability tool that meets our key criteria: accuracy, cost-effectiveness for self-hosting, alerting capabilities, PII and toxicity monitoring, strong community support, and frequent releases.

## Alternatives

1. **Langwatch**
2. **Langsmith**
3. **Langfuse**

## PrOACT Analysis

| Criteria               | Langwatch | Langsmith | Langfuse |
|-----------------------|-----------|-----------|-----------|
| **Accuracy**          | ● (5)     | ● (5)     | ◕ (4)     |
| **Trigger alerts**    | Email, Slack | Requires external integrations | N/A |
| **PII & Toxicity**    | Built-in evaluators | Built-in evaluators | Beta stage features |
| **Community support** | Github, Email, Discord | Slack | GitHub, Slack, Discord |
| **Release frequency** | Regular | Regular | Regular |
| **Charts & Filters**  | Advanced charting, but filters not reusable | Editable charts, reusable filters | Limited charting, no reusable filters |
| **Evaluations**       | No-code built-in | Code-based built-in | Custom setup required |
| **Integration**       | Python, JS/TS | Python, JS/TS | Python, JS/TS |
| **Export Traces**     | Yes | No | Yes |
| **Traces Retention**  | N/A | 400 days | N/A |
| **Model Providers**   | OpenAI, Azure OpenAI, Anthropic, Groq, Vertex AI, Cloudflare | 20+ models | 100+ models |

## Decision

After evaluating various tools, **Langwatch** is recommended for our use case due to its superior accuracy, built-in evaluators, advanced monitoring capabilities, and strong visualization features. It provides:

- **Comprehensive Data Visualization** with multiple charting options.
- **Feature-Rich Monitoring** with trace data export and alerting capabilities.
- **Alerts and Notifications** directly within the platform.
- **Robust Dashboarding** despite limitations in multiple dashboards.

## Tradeoffs - Mitigations

| Tradeoff | Mitigation |
|----------|------------|
| **Langwatch does not support multiple dashboards** | Use advanced charting options to compensate for limited dashboard flexibility. |
| **Langsmith offers better filter and dashboard management** | Prioritize Langwatch’s superior alerting, evaluations, and trace exports over these conveniences. |

## References

1. [Langwatch Documentation](https://docs.langwatch.ai/introduction)
2. [Langsmith Overview](https://www.langchain.com/langsmith)
3. [Langfuse Documentation](https://langfuse.com/docs)
4. [Langwatch vs. Langsmith vs. Langfuse Comparison](https://langwatch.ai/comparison)
