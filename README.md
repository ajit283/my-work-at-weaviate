# My Work at Weaviate

## Developer Growth Team

### Web Application Demos

These web applications aim to show developers what is possible with Weaviate and to provide a starting point for their own projects.

I used React and Next.js (using React Server Components + Server Actions) for both projects.

- [QuoteFinder](https://quotefinder.weaviate.io/)
- [Emoji Search](https://emoji.weaviate.io/)

### Jupyter Notebooks

I wrote several notebooks demonstrating several advanced RAG (Retrieval-Augmented Generation) techniques using Weaviate and related libraries:

- [Binary Quantization with Weaviate + Cohere](https://www.kaggle.com/code/ajitmistry/binary-quantization-with-weaviate-cohere)
- [Chat with your Code: Advanced RAG with Weaviate and LlamaIndex](https://lightning.ai/weaviate/studios/chat-with-your-code-advanced-rag-with-weaviate-and-llamaindex)

## Applied Research Team

Weaviate uses several vector distance functions (Dot, L2, Hamming) to determine semantic similarity. During indexing (insertion into the HNSW graph) and querying these are called many times and thus contribute strongly to the overall performance of Weaviate. When using Binary Quantization, the Hamming distance generally used as a distance metric. I implemented an SIMD accelerated version of this for several architectures:

- AVX256
- AVX512 (newer Intel CPUs such as Sapphire, Emerald Rapids)
- ARM NEON

links to PRs:

- https://github.com/weaviate/weaviate/pull/4678
- https://github.com/weaviate/weaviate/pull/4630

Weaviate 1.25 was released recently and includes these improvements. They reduce the runtime of the distance function itself by 90% (depending on vector dimensionality) and reduce overall indexing time by 30%.

Currently, I am also implementing other distance functions with SIMD, e.g. for 8-bit scalar quantization:

- https://github.com/weaviate/weaviate/pull/4756 (Dot Product, Byte Quantization, ARM NEON)
- https://github.com/weaviate/weaviate/pull/4797 (Dot Product, SVE for AWS Graviton CPUs)

Additionally, I read several papers related to performance improvements for vector databases, e.g.:

- [Locally-Adaptive Quantization for Streaming Vector Search](https://arxiv.org/abs/2402.02044)
- [ACORN: Performant and Predicate-Agnostic Search Over Vector Embeddings and Structured Data](https://arxiv.org/abs/2403.04871)

to participate in implementation discussions and code reviews.
