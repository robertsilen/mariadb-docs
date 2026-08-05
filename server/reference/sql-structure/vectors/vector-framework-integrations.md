---
description: >-
  MariaDB Vector integrations with popular AI, web and ORM frameworks.
---

# Vector Framework Integrations

{% include "https://app.gitbook.com/s/GxVnu02ec8KJuFSxmB93/~/reusable/pBQsCgBA6SJpi0m3pZuk/" %}

{% include "../../../.gitbook/includes/vectors-are-available-from-....md" %}

MariaDB Vector has integrations in several frameworks. For a general overview of MariaDB Vector — feature summary, benchmarks, tutorials, and demos — see the [MariaDB Vector project page](https://mariadb.org/projects/mariadb-vector/). MariaDB is not yet part of the [VectorDBBench](https://github.com/zilliztech/VectorDBBench) comparison suite.

Integrations differ in how much they cover, and in where the code lives. The support column uses these values:

- **Yes** — MariaDB Vector is supported by the framework itself.
- **Via package** — supported through a separate package the framework does not maintain.
- **Partial** — the framework covers part of it; a package covers the rest.
- **MariaDB project** — maintained by MariaDB; not a third-party framework integration.
- **Open request** — an issue asking for the integration is open, but no code has been merged yet.
- **Submitted, not merged** — a contributor built and submitted an integration, but it was not merged.
- **—** — no MariaDB Vector support, and no open request that we know of.

Each table lists supported frameworks first, then those without an integration.

## AI Frameworks

| Framework | Language | MariaDB Vector support | Covers |
| --- | --- | --- | --- |
| [LangChain](https://docs.langchain.com/oss/python/integrations/vectorstores) ([PyPI](https://pypi.org/project/langchain-mariadb/)) | Python | Via package | Store, index, similarity search. The `langchain-mariadb` package is maintained by MariaDB at [mariadb-corporation/langchain-mariadb](https://github.com/mariadb-corporation/langchain-mariadb) |
| [LangChain.js](https://www.npmjs.com/package/@langchain/community) | Node.js | Via package | `MariaDBStore`, exported from `@langchain/community` as `@langchain/community/vectorstores/mariadb`. Not currently listed in the LangChain JavaScript docs |
| [LangChain4j](https://docs.langchain4j.dev/integrations/embedding-stores/mariadb/) | Java | Yes | `MariaDbEmbeddingStore` in the `dev.langchain4j:langchain4j-mariadb` module |
| [LlamaIndex](https://developers.llamaindex.ai/python/framework-api-reference/storage/vector_store/mariadb/) | Python | Yes | Vector store in the LlamaIndex repository; synchronous API only |
| [Spring AI](https://docs.spring.io/spring-ai/reference/api/vectordbs/mariadb.html) | Java | Yes | `MariaDBVectorStore` with Spring Boot auto-configuration via `spring-ai-starter-vector-store-mariadb` |
| [MariaDB MCP server](https://github.com/mariadb/mcp) | Python | MariaDB project | SQL access and vector search for AI agents |
| [MariaDB skills for AI coding agents](https://github.com/MariaDB/skills) | — | MariaDB project | Guidance for agents writing MariaDB Vector SQL |
| [Haystack](https://haystack.deepset.ai/integrations?type=Document+Store) | Python | Open request | RFC opened during a MariaDB hackathon: [haystack-core-integrations#2340](https://github.com/deepset-ai/haystack-core-integrations/issues/2340) |
| [MindSQL](https://github.com/Mindinventory/MindSQL) | Python | Submitted, not merged | A complete integration was submitted in [PR #34](https://github.com/Mindinventory/MindSQL/pull/34) |
| [Semantic Kernel](https://learn.microsoft.com/en-us/semantic-kernel/concepts/vector-store-connectors/) | .NET, Python, Java | — | No MariaDB connector; connectors exist for other databases |
| [LangGraph](https://langchain-ai.github.io/langgraph/) | Python | — | No direct MariaDB support; agentic workflows reuse LangChain vector stores |
| [DB-GPT](https://github.com/eosphoros-ai/DB-GPT) | Python | — | No MariaDB vector store; private LLM, vector search and text2sql ([integration docs](http://docs.dbgpt.cn/docs/installation)) |

## Web Frameworks and ORMs

| Framework | Language | MariaDB Vector support | Covers |
| --- | --- | --- | --- |
| [Laravel](https://laravel.com/docs/13.x/migrations#column-method-vector) with [laravel-mariadb-vector](https://packagist.org/packages/devilsberg/laravel-mariadb-vector) | PHP | Partial | Laravel core provides vector columns and indexes — `$table->vectorIndex('embedding')` compiles to a MariaDB `VECTOR INDEX` with `M=6 DISTANCE=cosine` ([#60334](https://github.com/laravel/framework/pull/60334)). Similarity search in Laravel's query builder is PostgreSQL-only, so the package supplies the Eloquent casts and search macros |
| [Hibernate ORM](https://hibernate.atlassian.net/browse/HHH-18900) | Java | Yes | MariaDB vector type, since Hibernate ORM 7.0 |
| [TypeORM](https://typeorm.io/docs/drivers/mysql/) | TypeScript / Node.js | Yes | MariaDB vector columns, since TypeORM 0.3.28 |
| [SQLAlchemy](https://docs.sqlalchemy.org/en/20/core/types.html) with [mariadb-vector](https://pypi.org/project/mariadb-vector/) | Python | Via package | VECTOR type and distance functions for SQLAlchemy and SQLModel. The `mariadb-vector` package is community-maintained at [kwon-evan/mariadb-vector](https://github.com/kwon-evan/mariadb-vector) |
| [Doctrine ORM](https://www.doctrine-project.org/projects/doctrine-dbal/en/current/reference/types.html) | PHP | Open request | [doctrine/dbal#6703](https://github.com/doctrine/dbal/issues/6703), open since January 2025 |
| [Django](https://docs.djangoproject.com/en/stable/ref/models/fields/) | Python | — | Django ships no vector field for any database. MariaDB Vector is native to the server, so this is client-side work only: a Django field mapping to the `VECTOR` type |
| [Prisma](https://www.prisma.io/docs/orm/prisma-schema/data-model/models) | TypeScript / Node.js | — | Supports MariaDB as a database, but has no vector type for it. Prisma has vector support for other databases; see the general [First class Vector support](https://github.com/prisma/prisma/issues/26546) request |
| [Drizzle ORM](https://orm.drizzle.team/docs/guides/vector-similarity-search) | TypeScript / Node.js | — | Vector similarity search is PostgreSQL only. MariaDB is not supported as a dialect at all — see the open request [drizzle-orm#2007](https://github.com/drizzle-team/drizzle-orm/issues/2007) |
| [jOOQ](https://www.jooq.org/doc/latest/manual/sql-building/column-expressions/) | Java | — | No built-in vector type for any database; a similar request for pgvector was closed as "won't fix" ([jOOQ#16220](https://github.com/jOOQ/jOOQ/issues/16220)) |

For a worked example of picking an embedding model for MariaDB Vector in a Laravel application, see [MariaDB Vector in Laravel: insights on choosing an embedding model](https://mariadb.org/mariadb-vector-in-laravel-insights-on-choosing-an-embedding-model/).

## Low-Code and No-Code AI Platforms

These platforms ship vector-store connectors for other databases, but none for MariaDB yet. Each link goes to the platform's own vector-store documentation, where you can see which databases it currently supports.

- [Dify — vector database configuration](https://docs.dify.ai/)
- [n8n — vector store nodes](https://docs.n8n.io/integrations/builtin/cluster-nodes/root-nodes/n8n-nodes-langchain.vectorstorepgvector)
- [Flowise — vector stores](https://docs.flowiseai.com/integrations/langchain/vector-stores)
- [Langflow — vector store components](https://docs.langflow.org/components-vector-stores)
- [Open WebUI — retrieval and vector databases](https://docs.openwebui.com/features/chat-conversations/rag/)

## Contributing an Integration

A dash in the support column means there is no MariaDB Vector integration and, as far as we know, no open request for one. Entries marked *Open request* link to an existing issue — adding your support there is often the most useful first step. Each framework name links to its own vector documentation, so you can see which databases it currently supports.

If you have built or found an integration that is not listed here, tell us through the MariaDB Ecosystem Hub's [Get Involved page](https://ecohub.mariadb.org/get-involved) or at [foundation@mariadb.org](mailto:foundation@mariadb.org). For the full, continuously updated catalog of AI frameworks, platforms, and tools that work with MariaDB, see the [AI & Application Development category of the MariaDB Ecosystem Hub](https://ecohub.mariadb.org/ai-application-development).

<sub>_This page is licensed: CC BY-SA / Gnu FDL_</sub>

{% @marketo/form formId="4316" %}