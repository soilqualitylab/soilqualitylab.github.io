# Best Practices In Context Engineering

**Key Points:**
- Context engineering involves curating and structuring information to optimize large language model (LLM) performance, going beyond simple prompt crafting.
- It seems likely that effective context engineering enhances LLM reliability by providing relevant data, tools, and formats, though challenges like token costs and context degradation persist.
- Research suggests practices like structured state management, compression, and multi-agent systems improve outcomes, but there’s ongoing debate about balancing technical and organizational needs.
- The term "context engineering" is gaining traction over "prompt engineering," reflecting its broader scope, though some argue it overlaps with intent or communication engineering.

**What is Context Engineering?**
Context engineering is the practice of designing and managing the information provided to LLMs to ensure they can effectively perform tasks. Unlike prompt engineering, which focuses on crafting specific instructions, context engineering involves dynamically assembling relevant data, tools, and formats to create a comprehensive context window. This process is critical for complex AI applications, such as agentic systems, where LLMs need to handle long-running tasks or integrate with external tools.

**Why It Matters**
As LLMs become more powerful, their ability to process and utilize context determines their effectiveness. Poorly managed context can lead to irrelevant or incorrect outputs, while well-engineered context can transform an LLM into a highly capable assistant. This is particularly important in industrial applications where tasks require specific, often organizationally unique, information.

**Core Practices**
- **Track Token Usage**: Monitor and manage token consumption to optimize costs and performance.
- **Structure Context**: Use schemas to organize data, ensuring only relevant information is included.
- **Compress Data**: Summarize outputs from tools to keep context manageable.
- **Implement Memory**: Use simple memory systems to track and update agent states.
- **Leverage Multi-Agent Systems**: Employ multiple agents for parallel tasks to enhance efficiency.
- **Dynamic Context Assembly**: Build systems that adaptively fetch and format context from various sources.

**Relevant Research**
Recent studies, such as those on arXiv, explore scaling context lengths and attributing model outputs to specific context parts, offering tools to refine context engineering practices. These findings suggest that with proper data engineering, LLMs can handle extended contexts, improving their utility in real-world applications.

---

### Comprehensive Overview of Context Engineering Best Practices

Context engineering has emerged as a pivotal discipline in the development of AI applications, particularly those leveraging large language models (LLMs). It encompasses the strategic curation, structuring, and management of information provided to LLMs to optimize their performance across diverse tasks. This section provides a detailed exploration of best practices, drawing from recent discussions, research papers, and industry insights, including those referenced in the provided document by Lance Martin and related X posts.

#### Defining Context Engineering
Context engineering is the art and science of building dynamic systems that supply LLMs with the right information and tools in an appropriate format to accomplish tasks effectively. As articulated by Andrej Karpathy in an X post on June 25, 2025 ([Karpathy's Post](https://x.com/karpathy/status/1937902205765607626)), it involves filling the LLM’s context window with task descriptions, few-shot examples, retrieval-augmented generation (RAG) data, multimodal inputs, tools, state, and history. This process requires balancing the amount and relevance of information to avoid performance degradation or excessive costs, blending scientific precision with an intuitive understanding of how LLMs process context.

The LangChain blog post on June 23, 2025 ([The Rise of Context Engineering](https://blog.langchain.com/the-rise-of-context-engineering/)), further defines context engineering as distinct from prompt engineering, emphasizing its focus on assembling dynamic data rather than just crafting instructions. It highlights that context engineering is becoming the most critical skill for AI engineers as applications evolve from single prompts to complex, agentic systems.

#### Best Practices in Context Engineering
The following best practices are synthesized from the document by Lance Martin ([Context Engineering](https://rlancemartin.github.io/2025/06/23/context_engineering/)), X posts, and related resources, providing actionable strategies for effective context engineering.

1. **Instrumentation for Token Management**
   - **Description**: Tracking token usage is essential to identify and mitigate excessive consumption, particularly from tool calls, which can inflate costs and degrade performance.
   - **Implementation**: Use monitoring tools to track token usage and isolate token-heavy operations. This sets the stage for optimizing context engineering efforts.
   - **Reference**: Hamel’s blog on evaluations ([Evals Blog](https://hamel.dev/blog/posts/evals/)) emphasizes the importance of instrumentation in managing LLM performance.

2. **Structured State Management**
   - **Description**: Define a well-structured state schema to control the information exposed to the LLM, avoiding bloated message lists that can overwhelm the model.
   - **Implementation**: Use frameworks like Pydantic to create structured schemas. For example, Anthropic’s research system saves research plans for future use, ensuring consistent context ([Anthropic’s Multi-Agent System](https://www.anthropic.com/engineering/built-multi-agent-research-system)).
   - **Example**: A state schema might include fields for task objectives, user preferences, and recent interactions, ensuring only relevant data is included.

3. **Compression at Tool Boundaries**
   - **Description**: Summarize outputs from token-heavy tool calls to prevent context growth, maintaining efficiency.
   - **Implementation**: Use a smaller LLM with straightforward prompting to compress tool outputs. For instance, Claude Code auto-compacts context at 95% of the context window ([Claude Code Best Practices](https://www.anthropic.com/engineering/claude-code-best-practices)).
   - **Benefit**: Reduces token costs and maintains model focus on relevant information.

4. **Simple Memory Systems**
   - **Description**: Implement basic memory systems to track and update agent states, enhancing context continuity.
   - **Implementation**: Use file-based memory to store preferences or states, updated via LLM based on human feedback. An example is an email assistant tracking user preferences ([LangChain Agents](https://github.com/langchain-ai/agents-from-scratch)).
   - **Tools**: Frameworks like Letta, Mem0, LangGraph, Zep, or Neo4J can facilitate memory management.

5. **Multi-Agent Systems for Parallel Tasks**
   - **Description**: Employ multiple agents for tasks that can be parallelized, improving efficiency but requiring careful coordination.
   - **Implementation**: Anthropic’s multi-agent researcher outperformed single-agent systems by 90.2%, though it used 15× more tokens ([Anthropic’s Multi-Agent System](https://www.anthropic.com/engineering/built-multi-agent-research-system)).
   - **Challenge**: Coordination in multi-agent systems can be complex, requiring robust context isolation strategies.

6. **Dynamic Context Assembly**
   - **Description**: Build systems that dynamically fetch and format context from multiple sources, such as user inputs, previous interactions, Juno, tool outputs, and external data.
   - **Implementation**: Use retrieval systems to dynamically insert relevant information into prompts, as discussed in the LangChain blog ([The Rise of Context Engineering](https://blog.langchain.com/the-rise-of-context-engineering/)).
   - **Example**: An agent might fetch user preferences from a database and combine them with real-time tool outputs.

7. **Format and Structure Optimization**
   - **Description**: The format of context significantly impacts LLM performance. Clear, consistent formatting enhances pattern recognition.
   - **Implementation**: Ensure consistent formatting of examples and instructions, as noted in a Reddit post on in-context learning ([Reddit Post](https://www.reddit.com/r/LLMDevs/comments/1g8uio9/prompt_engineering_best_practices_for_incontext/)). For example, order examples from simple to complex or place the most relevant ones last.
   - **Insight**: @omarsar0 on X emphasizes structuring inputs/outputs, including schema definitions, to improve clarity ([Omar's Post](https://x.com/omarsar0/status/1938239935770763727)).

8. **Evaluation and Iteration**
   - **Description**: Continuously evaluate whether the context enables the LLM to plausibly accomplish the task, iterating as needed.
   - **Implementation**: Use observability tools like LangSmith to trace agent calls and identify context-related issues ([LangSmith](https://smith.langchain.com/)).
   - **Question**: As per the LangChain blog, ask, “Can it plausibly accomplish the task?” to diagnose context deficiencies.

#### Challenges in Context Engineering
- **Context Degradation Syndrome**: Overloading the context window with irrelevant data can reduce performance, as noted by Karpathy ([Karpathy's Post](https://x.com/karpathy/status/1937902205765607626)).
- **Token Costs**: Deep research agents can consume significant tokens (e.g., >500k tokens per run), increasing costs ([Context Engineering](https://rlancemartin.github.io/2025/06/23/context_engineering/)).
- **Coordination in Multi-Agent Systems**: Ensuring seamless interaction among agents requires careful context isolation, such as using schemas or sandbox environments.

#### Relevant Research from arXiv
Recent research on arXiv provides valuable insights into context engineering:

- **[Data Engineering for Scaling Language Models to 128K Context](https://arxiv.org/abs/2402.10171)**:
  - **Findings**: Lightweight continual pretraining with 500M to 5B tokens of balanced, domain-diverse data enables LLMs to handle 128K-token contexts. Domain balance and length upsampling are critical for optimal performance.
  - **Implication**: Context engineering for long contexts requires careful data engineering to maintain model capabilities across extended inputs.
  - **Code**: Available at [Long Context Data Engineering](https://github.com/FranxYao/Long-Context-Data-Engineering).

- **[ContextCite: Attributing Model Generation to Context](https://arxiv.org/abs/2409.00729)**:
  - **Findings**: ContextCite is a scalable method to pinpoint which context parts influence specific model outputs, aiding in verification, context pruning, and poisoning detection.
  - **Implication**: Tools like ContextCite enhance context engineering by ensuring outputs are grounded in relevant context, improving reliability.
  - **Code**: Available at [ContextCite GitHub](https://github.com/MadryLab/context-cite).

#### Additional Insights from Industry
- **Organizational Context**: Ethan Mollick on X emphasizes that context engineering involves aligning LLMs with organizational operations, including reports, processes, and tone ([Mollick's Post](https://x.com/emollick/status/1937952769513517328)). This cross-functional approach ensures AI outputs reflect company identity.
- **Tool Integration**: Tools like LangGraph and LangSmith facilitate context engineering by providing control over agent workflows and observability ([LangGraph](https://github.com/langchain-ai/langgraph), [LangSmith](https://smith.langchain.com/)).
- **Community Perspectives**: X posts highlight diverse views, such as @virtualmilin’s use of unique code and app flow context for a 95% success rate in root cause analysis ([Virtualmilin's Post](https://x.com/virtualmilin/status/1937970191193018455)), and @ankrgyl’s note on the pervasive challenge of engineering every stack layer ([Ankrgyl's Post](https://x.com/ankrgyl/status/1913766591910842619)).

#### Practical Example

# Example Context Engineering Workflow

## Objective
Create an LLM-based email assistant that responds to customer inquiries with relevant product information.

## Context Components
- **User Preferences**: Stored in a JSON file, updated based on feedback.
  ```json
  {
    "user_id": "123",
    "preferred_tone": "professional",
    "language": "English"
  }
  ```
- **Product Data**: Retrieved via RAG from a product database.
  ```json
  {
    "product_id": "456",
    "name": "Widget X",
    "features": ["Feature A", "Feature B"],
    "price": "$99.99"
  }
  ```
- **Conversation History**: Summarized to maintain context continuity.
  ```text
  Customer asked about Widget X features on 2025-06-25.
  ```
- **Instructions**: Clear, structured prompt.
  ```text
  You are a professional email assistant. Respond to the customer's inquiry about Widget X using the provided product data and user preferences. Maintain a professional tone.
  ```

## Workflow
1. **Retrieve Context**: Fetch user preferences and product data.
2. **Summarize History**: Compress conversation history to fit context window.
3. **Format Prompt**: Combine instructions, preferences, data, and history in a structured format.
4. **Evaluate**: Check if the context enables a plausible response; adjust if necessary.
5. **Generate Response**: Pass the context to the LLM for response generation.

## Expected Output
A professional email response detailing Widget X’s features, tailored to the user’s preferences.


#### Conclusion
Context engineering is a multifaceted discipline that enhances LLM performance by ensuring the right information, tools, and formats are provided. By implementing best practices like instrumentation, structured state management, and dynamic context assembly, developers can create robust AI applications. Ongoing research and tools like LangGraph and ContextCite continue to advance the field, addressing challenges like token costs and context degradation. As LLMs evolve, context engineering will remain a cornerstone of effective AI development, bridging technical precision with organizational needs.

**Key Citations:**
- [Karpathy’s X Post on Context Engineering](https://x.com/karpathy/status/1937902205765607626)
- [The Rise of Context Engineering by LangChain](https://blog.langchain.com/the-rise-of-context-engineering/)
- [Boris Tane’s Blog on Context Engineering](https://boristane.com/blog/context-engineering/)
- [Data Engineering for Scaling Language Models to 128K Context](https://arxiv.org/abs/2402.10171)
- [ContextCite: Attributing Model Generation to Context](https://arxiv.org/abs/2409.00729)
- [Hamel’s Blog on Evaluations](https://hamel.dev/blog/posts/evals/)
- [Anthropic’s Multi-Agent Research System](https://www.anthropic.com/engineering/built-multi-agent-research-system)
- [LangChain Agents from Scratch](https://github.com/langchain-ai/agents-from-scratch)
- [Claude Code Best Practices by Anthropic](https://www.anthropic.com/engineering/claude-code-best-practices)
- [Reddit Post on In-Context Learning Best Practices](https://www.reddit.com/r/LLMDevs/comments/1g8uio9/prompt_engineering_best_practices_for_incontext/)
- [Omar’s X Post on Context Engineering Components](https://x.com/omarsar0/status/1938239935770763727)
- [Mollick’s X Post on Organizational Context](https://x.com/emollick/status/1937952769513517328)
- [Virtualmilin’s X Post on Seer System](https://x.com/virtualmilin/status/1937970191193018455)
- [Ankrgyl’s X Post on Context Engineering Challenges](https://x.com/ankrgyl/status/1913766591910842619)
- [LangGraph GitHub Repository](https://github.com/langchain-ai/langgraph)
- [LangSmith Observability Platform](https://smith.langchain.com/)
- [Long Context Data Engineering GitHub](https://github.com/FranxYao/Long-Context-Data-Engineering)
- [ContextCite GitHub Repository](https://github.com/MadryLab/context-cite)