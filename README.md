# go-cortex 🧠  
**A Provider-Agnostic AI SDK for Go**

`go-cortex` is an **open-source, provider-agnostic AI SDK for Go**, designed to offer a **unified, extensible, and idiomatic Go interface** over multiple AI/LLM platforms such as OpenAI, Gemini, Claude, DeepSeek, and others.

The goal is simple:

> **Let Go developers integrate AI capabilities without locking themselves to a single provider.**

---

## Why go-cortex?

Most AI platforms ship **provider-specific SDKs**, each with:
- Different APIs
- Different auth models
- Different request/response formats
- Different streaming semantics

This leads to:
- Tight vendor lock-in
- Hard-to-test code
- Painful migrations when models or providers change

**go-cortex solves this by introducing a clean abstraction layer** that separates:
- **What your application wants to do**
- from **how a specific AI provider does it**

---

## Design Principles

- **Provider Agnostic** – Switch AI providers with minimal or zero application changes
- **Go-First API** – Idiomatic Go, contexts everywhere, no magic
- **Composable** – Small interfaces, easy to extend
- **Explicit over Implicit** – No hidden defaults or global state
- **Enterprise-Ready** – Suitable for regulated and air-gapped environments

---

## Supported / Planned Providers

| Provider         | Status |
| ---------------- | ------ |
| OpenAI           | Planned |
| Gemini           | Planned |
| Claude           | Planned |
| DeepSeek         | Planned |
| Azure OpenAI     | Planned |
| Self-hosted LLMs | Planned |

> ⚠️ Initial releases will focus on **core abstractions** before adding provider implementations.

---

## Core Concepts

### 1. Unified Client Interface

A single interface to interact with different AI platforms:

```go
type LLM interface {
    Generate(ctx context.Context, req GenerateRequest) (GenerateResponse, error)
    Stream(ctx context.Context, req GenerateRequest) (<-chan StreamChunk, error)
}
````

---

### 2. Pluggable Providers

Each provider implements the same interface:

```go
llm := cortex.New(
    cortex.WithProvider(openai.New(openai.Config{
        APIKey: os.Getenv("OPENAI_API_KEY"),
    })),
)
```

Switching providers does **not** change application logic.

---

### 3. Strongly Typed Requests & Responses

No raw `map[string]interface{}` chaos.

```go
resp, err := llm.Generate(ctx, cortex.GenerateRequest{
    Model: "gpt-4.1",
    Messages: []cortex.Message{
        cortex.User("Explain Go interfaces"),
    },
})
```

---

### 4. Context-Driven by Default

All operations accept `context.Context` for:

* Cancellation
* Timeouts
* Tracing
* Request scoping

---

## Planned Feature Roadmap

### Phase 1 – Foundation

* Core abstractions
* Request/response models
* Provider interfaces
* OpenAI provider (reference implementation)

### Phase 2 – Advanced Capabilities

* Streaming APIs
* Tool / Function calling abstraction
* Token usage & cost tracking
* Retry & backoff strategies

### Phase 3 – AI-Native Systems

* MCP (Model Context Protocol) support
* RAG-friendly interfaces
* Agent execution primitives
* Multi-model orchestration

---

## Non-Goals (By Design)

* ❌ No UI frameworks
* ❌ No opinionated agent frameworks (yet)
* ❌ No hidden prompt engineering magic
* ❌ No provider-specific feature leakage

go-cortex focuses on **infrastructure primitives**, not end-user apps.

---

## Installation

```bash
go get github.com/rahulsidpatil/go-cortex
```

---

## Project Structure (Planned)

```
go-cortex/
├── cortex/          # Core interfaces & models
├── providers/
│   ├── openai/
│   ├── gemini/
│   └── claude/
├── middleware/      # retries, logging, metrics
├── examples/
└── docs/
```

---

## Who Is This For?

* Go developers building AI-enabled services
* Platform & infrastructure engineers
* Cloud-native teams avoiding vendor lock-in
* Enterprises with compliance constraints
* Educators and researchers exploring AI-native SDLC

---

## Relationship to Other Projects

`go-cortex` is:
* **Not a SaaS**
* **Not a wrapper around one SDK**

It is intended to become a **long-term open-source foundation** for:

* AI-native Go applications
* Agentic systems
* Context-aware software architectures

---

## Contributing
Contributions are welcome—especially in:
* API design reviews
* Provider implementations
* Documentation & examples
* Testing & benchmarking

Please open an issue before submitting large changes.

---

## License

MIT License

---

## Author

**Rahul S. Patil**
Software Architect • Go & Cloud Native • AI Systems
GitHub: [https://github.com/rahulsidpatil](https://github.com/rahulsidpatil)

