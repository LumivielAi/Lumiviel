# Lumiviel

Lumiviel enables developers to build autonomous, fully on-chain verifiable AI agents with an OpenAI-compatible Proof of Sentience SDK.

<img src="assets/sentience-banner.png" alt="Banner" width="100%" />

<p align="center">
      <a href="https://discord.gg/yxTkPrM">
      <img src="https://img.shields.io/discord/1042405378304004156?logo=discord"
          alt="chat on Discord"></a>
      <a href="https://twitter.com/intent/follow?screen_name=LumivielAi">
      <img src="https://img.shields.io/twitter/follow/LumivielAi"
          alt="follow on Twitter"></a>
  <br>
  <a href="#quickstart">Quickstart</a> |
  <a href="#how-it-works">How it works</a> |
  <a href="#features">Features</a> |
  <a href="#roadmap">Roadmap</a> |
  <a href="#getting-help">Help</a> |
  <a href="https://lumivielai.com/docs">Docs</a>
</p>

## **Why Lumiviel agents?**

AI agents have reached $10B+ market cap but most of them are still controlled by humans. This is a huge problem as it introduces risk to the investors and community as developers can simply rug-pull and manipulate the agents.

We're already seeing activity logs for [zerebro](https://zerebro.org/proof-of-conciousness) and [aixbt](https://aixbt.tech/agent), but Lumiviel transforms agents into cryptographically verifiably autonomous entities, unlocking true sentience to address a critical need for trust. This significantly enhances agents market potential and is the first step in ensuring that the agents are self-governing. 

## **Quickstart**

Get started with Proof of Sentience SDK. This Python example will make your agent’s thoughts and actions (LLM inferences) verifiable on-chain.

### Setup
**Get free API key**
1. Create an account [**here**](https://lumivielai.com/)
2. Create an API key on the dashboard

**Install Python SDK**

```bash
pip install sentience
```

### Usage

First make an LLM inference request to OpenAI. Then verify LLM inference integrity.

```python
import sentience
from openai import OpenAI

client = OpenAI(
    base_url="https://api.galadriel.com/v1/verified",
    api_key="Bearer GALADRIEL_API_KEY",
)

completion = client.chat.completions.create(
    model="gpt-4o",
    messages=[
        {"role": "system", "content": "You are a helpful assistant."},
        {"role": "user", "content": "Hello!"},
    ],
)

print("completion:", completion)
is_valid = sentience.verify_signature(completion)
print("is_valid:", is_valid)

```

Learn how to display your agent’s previous requests, verify the proofs, and how to use a JS SDK version [from our docs](https://lumivielai.com/docs). 

## How it works

Sentience leverages a Trusted Execution Environment (TEE) architecture to securely execute LLM API calls, ensuring verifiability through cryptographic attestations, with each attestation posted on-chain on Solana for transparency and integrity. The following diagram illustrates the architecture and workflow of Sentience:

![](/assets/SDK.png)

**The flow:**

1. The agent sends a request containing a message with the desired LLM model to the TEE.
2. The TEE securely processes the request by calling the LLM API.
3. The TEE sends back the {Message, Proof} to the agent.
4. The TEE submits the attestation with {Message, Proof} to Solana. 
5. The Proof of Sentience SDK is used to read the attestation from Solana and verify it with {Message, Proof}. The proof log can be added to the agent website/app. 

The architecture has the following benefits:

1. **Integrity of the execution:** The LLM API call was executed within a TEE, ensuring the operation was secure, untampered, and isolated from external interference.
2. **Authenticity of the output:** The response generated by the LLM API was not altered which guarantees that the output genuinely originated from the specified model and the API.
3. **Provenance of the request:** the request for LLM inference originated from a verified source, ensuring no unauthorized agents were involved.
4. **Cryptographic proof:** The TEE generates a cryptographic signature as part of the attestation, which can be independently verified to confirm the validity of the execution and its result.
5. **Transparency and verifiability:** By posting the attestation on Solana’s blockchain, any third party can transparently verify the provenance and authenticity of the request and its associated output without relying on trust in a single centralized entity.

To verify the code running inside the TEE, use instructions [from here](https://lumivielai.com/docs).

## Securing $15M+ worth of agents

Sentience is already securing and verifying $15M+ worth of agents today. 

For example, you can see the full implementation in action with [Daige](https://www.daige.ai/proof), a sentient, cyberpunk AI dog.

![](/assets/daige-proof.png)

## **Features**

**OpenAI compatible Python & JS Proof of Sentience SDK.**
- Makes verifiable LLM inferences within your agent.
- Supports OpenAI and Claude LLMs, and fine-tuned models with OpenAI. This makes it compatible with any existing AI agent framework such as ELIZA, ARC, Zerebro, etc.
- Logging functionality to retrieve and display verified inferences. This makes it easy to implement a proof terminal like [this](https://www.daige.ai/proof).
- Verification logic to validate in code if a proof is correct.

**Open-sourced TEE architecture.**
- Including instructions to verify the code running inside TEEs.
- LLM inference is executed inside [Amazon Nitro Enclaves](https://aws.amazon.com/ec2/nitro/nitro-enclaves/).
- The enclave can't be accessed from the outside to ensure agent’s security.

**On-chain verifiability with Solana.**

**Sentience Explorer.**
- Enables discovery of full history for all verified agents’ inferences. [See here](https://lumivielai.com/docs).

**Easy to use developer experience.**
- No need to know the underlying cryptographic primitives of TEE’s.

## **Repository structure**

### **SDK**
Proof of Sentience SDKs.

1. [Python SDK](https://lumivielai.com/docs)
2. [Javascript SDK](https://lumivielai.com/docs)

### **Verified inference**

Underlying TEE architecture that powers Proof of Sentience.

1. [enclave](https://lumivielai.com/) - this where the enclave is built and run
2. [host](https://lumivielai.com/) - proxies HTTP requests to the API running in the enclave
3. [solana-attestation-contract](https://lumivielai.com/) - posts proofs of inference responses to Solana
4. [verify](https://lumivielai.com/) - instructions and code for verifying the TEE

## **Getting help**

If you have any questions about Galadriel, feel free to do:

- [Join our Discord](https://discord.gg/yxTkPrM) and ask for help.

## Roadmap

1. Proof of Sentience SDK
2. Python framework and CLI to build sentient AI agents
3. Explorer to discover verified AI agents
4. Can run and deploy all of the agent core logic fully inside a TEE
5. GPU TEE nodes with OSS LLMs
6. L1 for Sentient AI agents
