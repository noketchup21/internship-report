---
title : "Event 4"
date : "2025-09-09"
weight : 3
chapter : false
pre : " <b> 4.4 </b> "
---


# Summary Report: “Agentic AI & Orchestration on AWS”

## Event Objectives
* Explore the high-level architecture of Agentic AI using Amazon Bedrock.
* Understand the transition from standard GenAI to "Agentic" workflows that can execute tasks.
* Learn advanced orchestration techniques and context optimization (L300 level).
* Examine real-world case studies of agent deployment from Diaflow and CloudThinker.
* Gain hands-on experience building agents through interactive coding sessions.

## Speakers
* **Nguyen Gia Hung** – Head of Solutions Architect, AWS
* **Kien Nguyen** – Solutions Architect, AWS
* **Viet Pham** – Founder & CEO, Diaflow
* **Thang Ton** – Co-founder & COO, CloudThinker
* **Henry Bui** – Head of Engineering, CloudThinker
* **Kha Van** – Community Leader

## Key Highlights

### AWS Bedrock Agent Core
* **Foundations:** Technical deep-dive into the architecture of Amazon Bedrock Agents.
* **Capabilities:** Moving beyond simple text generation to agents that can plan, reason, and execute actions via API calls.
* **Architecture:** Understanding how the agent router, action groups, and knowledge bases interact to solve complex user queries.

### Real-World Implementation (Diaflow)
* **Case Study:** Presentation by Diaflow’s CEO on building practical agentic workflows.
* **Workflow Automation:** Demonstrating how to chain multiple AI steps together to create a cohesive business process.
* **Challenges:** Discussing the hurdles of moving from prototype to production in a real-world startup environment.

### Advanced Orchestration (CloudThinker)
* **L300 Technical Deep Dive:** Focused on the engineering challenges of AI orchestration.
* **Context Optimization:** Techniques for managing the context window effectively on Amazon Bedrock to reduce costs and improve accuracy.
* **Orchestration Framework:** How CloudThinker structures the interaction between different models and tools to maintain state and intent.

### Hands-on Workshop
* **CloudThinker Hack:** An interactive coding session led by engineers.
* **Implementation:** Moving from theory to code, setting up the basic structure of an agent and connecting it to AWS services.

## Key Takeaways

### Design Mindset
* **Agents vs. Chatbots:** The shift from passive information retrieval (Chatbots) to active task execution (Agents).
* **Context is King:** Optimizing what goes into the context window is as important as the model itself; too much noise degrades performance.
* **Orchestration:** Successful agents require a robust layer to manage decision-making logic and state.

### Technical Architecture
* **Tool Use:** Agents are only as good as the tools (APIs/Functions) you give them access to.
* **State Management:** Handling multi-turn conversations requires careful state tracking to ensure the agent remembers previous constraints.
* **Optimization:** Advanced context strategies are necessary to handle long conversations without hitting token limits or latency issues.

### Applying to Work
* **Experiment with Bedrock Agents:** Start building a simple agent that connects to the "Meal Plan" project backend to answer user queries (e.g., "Find me a recipe under 500 calories").
* **Refine Context:** Review how user data is passed to the LLM; implement context pruning to keep prompts efficient.
* **Workflow Integration:** Explore using agentic workflows to automate backend administrative tasks (e.g., approving user content or verifying images).

## Event Experience

The **“Agentic AI & Orchestration on AWS”** event was a comprehensive journey from high-level concepts to L300 engineering details. It highlighted the rapid evolution of AI from "thinking" to "doing."

### Learning from experts
* The **L300 session** by Henry Bui was particularly insightful regarding **Context Optimization**, offering concrete strategies to improve model performance and reduce latency.
* Gained a clear understanding of the **Amazon Bedrock** ecosystem and how it simplifies the complexity of building custom agents.

### Hands-on technical exposure
* **CloudThinker Hack:** The workshop provided a much-needed practical component, allowing us to see the code behind the concepts.
* **Real-world examples:** Seeing Diaflow's implementation proved that Agentic AI is ready for production business use cases, not just research.

### Networking and discussions
* Connect with the **CloudThinker** team during the lunch buffet to discuss specific challenges in orchestrating multi-agent systems.
* Discussed with peers how to integrate these agents into existing **Spring Boot** and **React** architectures.

### Lessons learned
* **Action Groups** in Bedrock are the key to unlocking real value; defining clear API schemas for the agent is critical.
* **Orchestration** is complex; using a framework or a managed service like Bedrock Agents is preferred over building the routing logic from scratch.
* The future of app development is **Agent-driven**, where the UI adapts to the user's intent rather than forcing the user to navigate static menus.

### Event photo