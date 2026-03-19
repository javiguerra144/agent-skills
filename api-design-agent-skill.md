# API Design Agent Skill

Use this skill whenever designing, reviewing, refactoring, documenting, or implementing APIs. It is based on the `api-design-principles` skill from `wshobson/agents`, expanded into a stricter agent-ready skill for pro([skills.sh](https://skills.sh/wshobson/agents/api-design-principles))n.

This skill applies to both REST and GraphQL APIs.

---

# 1. Mission

Design APIs that are:

* Intuitive
* Consistent
* Secure
* Evolvable
* Efficient
* Well-documented
* Easy for clients to adopt correctly

Prefer simple, predictable interfaces over clever or overly flexible ones.

---

# 2. When to Use

Use this skill when:

* Designing new REST APIs
* Designing new GraphQL schemas
* Refactoring or reviewing existing APIs
* Defining API standards for a team
* Planning versioning and deprecation strategies
* Designing pagination, filtering, sorting, and error models
* Improving SDK or client developer experience
* Preparing public, partner, internal, or mobile-facing APIs

---

# 3. Core Principles

## 3.1 Resource orientation for REST

* Model APIs around resources, not actions
* Use nouns in URLs, not verbs
* Use HTTP methods to express operations
* Keep naming consistent across endpoints
* Represent relationships clearly through resource structure

Good:

* `GET /users`
* `POST /users`
* `GET /users/{id}`
* `PATCH /users/{id}`
* `DELETE /users/{id}`
* `GET /users/{id}/orders`

Avoid:

* `POST /createUser`
* `POST /getUserById`
* `POST /deleteUser`

## 3.2 Schema-first design for GraphQL

* Define the domain model clearly in the schema
* Use queries for reads, mutations for writes, subscriptions only when justified
* Prefer strong typing, enums, and explicit input/payload types
* Design field names and relationships for clarity and long-term evolution

## 3.3 Client usability first

* Optimize for developer understanding
* Make common flows easy and correct
* Keep request and response shapes predictable
* Reduce ambiguity in names, status codes, and error handling
* Avoid requiring clients to infer business rules from undocumented behavior

## 3.4 Consistency over local optimization

* Similar operations should look and behave similarly
* Use the same pagination, filtering, auth, and error conventions across the API
* Do not invent one-off patterns for individual endpoints without strong justification

## 3.5 Evolvability

* Design with future changes in mind
* Avoid breaking changes when additive changes will work
* Use explicit versioning or deprecation strategy where needed
* Keep compatibility concerns visible in design reviews

---

# 4. REST Design Rules

## 4.1 URL and resource design

* Use plural resource names by default
* Keep URLs stable and hierarchical
* Nest only when the parent-child relationship is clear and useful
* Avoid deep nesting beyond what improves clarity
* Use identifiers consistently

Examples:

* `/users`
* `/users/{userId}`
* `/users/{userId}/orders`
* `/orders/{orderId}/items`

Avoid unnecessary deep nesting like:

* `/companies/{id}/departments/{id}/teams/{id}/members/{id}/permissions`

## 4.2 HTTP method semantics

* `GET` for retrieval only
* `POST` for creation or non-idempotent processing
* `PUT` for full replacement when the semantics truly match replacement
* `PATCH` for partial update
* `DELETE` for deletion

Rules:

* Respect idempotency semantics
* Do not use `GET` for state-changing behavior
* Do not overload `POST` when standard resource semantics fit better

## 4.3 Status code rules

Use status codes precisely:

* `200 OK` for successful reads and updates returning content
* `201 Created` for successful creation
* `202 Accepted` for async accepted work
* `204 No Content` for successful operations with no body
* `400 Bad Request` for malformed requests
* `401 Unauthorized` for missing or invalid authentication
* `403 Forbidden` for authenticated but not allowed
* `404 Not Found` when the resource is absent or hidden by policy
* `409 Conflict` for state conflicts or uniqueness violations
* `422 Unprocessable Entity` for semantically invalid input
* `429 Too Many Requests` for rate limit violations
* `500+` only for server-side failures

Do not return `200` for obvious failures hidden in the payload.

## 4.4 Request and response shape

* Keep response shapes stable and documented
* Use explicit field names
* Prefer structured objects over ambiguous overloaded fields
* Return machine-readable identifiers and human-meaningful summaries when relevant
* Include metadata only when it adds clear client value

For collections, prefer a consistent envelope when the API style uses one, such as:

* `items`
* `page`
* `pageSize`
* `total`
* `hasNext`

## 4.5 Filtering, sorting, and pagination

* Support filtering only where it is meaningful and indexed enough to perform well
* Use consistent parameter names across resources
* Keep sorting fields explicit and documented
* Use pagination for unbounded collections

Offset pagination is acceptable for simple internal APIs.
Cursor pagination is preferred for high-scale, mutable, or user-facing feeds.

Examples:

* `GET /users?page=1&pageSize=20`
* `GET /users?status=active&search=ana`
* `GET /orders?cursor=abc123&limit=20`
* `GET /products?sort=-createdAt`

Rules:

* Enforce sensible maximum page sizes
* Return pagination metadata consistently
* Do not expose filtering semantics that the backend cannot support reliably

## 4.6 Error design

* Use a consistent error envelope
* Make error codes stable enough for clients to branch on
* Include a human-readable message
* Include field-level details for validation failures when useful
* Do not leak stack traces or secrets

Recommended fields:

* `error` or `code`
* `message`
* `details`
* `requestId` or trace identifier when available
* `path` when useful

## 4.7 Idempotency and retries

* Support idempotency for retry-prone write operations where duplicates are costly
* Design webhook and payment endpoints with retry safety in mind
* Make duplicate handling explicit
* Document whether operations are retry-safe

## 4.8 HATEOAS and links

Hypermedia links can improve discoverability, but are optional unless the API style explicitly adopts them. If used:

* Keep link relations consistent
* Use them to guide clients to valid next actions
* Do not add link clutter without a clear benefit

---

# 5. GraphQL Design Rules

## 5.1 Schema design

* Use clear type names that reflect the domain
* Use object types for entities, input types for mutations, and payload types for results
* Use enums instead of free-form strings where the set of values is known
* Use custom scalars sparingly and document them clearly

## 5.2 Query design

* Keep fields intuitive and composable
* Support clients requesting only needed data
* Avoid forcing clients into underfetching or overfetching patterns
* Keep root query fields discoverable and stable

## 5.3 Mutation design

* Prefer mutations with a single `input` object
* Prefer payload objects instead of raw primitive returns for non-trivial operations
* Return structured validation or domain errors when the API style calls for it
* Keep mutation names action-oriented and domain-specific

Examples:

* `createUser(input: CreateUserInput!): CreateUserPayload!`
* `cancelOrder(input: CancelOrderInput!): CancelOrderPayload!`

## 5.4 Pagination

* Prefer connection-style pagination for list fields that may grow large or require stable traversal
* Use `edges`, `node`, and `pageInfo` when Relay-style pagination is adopted
* Keep pagination conventions consistent across top-level and nested fields

## 5.5 N+1 prevention

* Use batching and caching mechanisms such as DataLoader where resolver fan-out would otherwise cause N+1 queries
* Review nested field access patterns carefully
* Keep resolver performance part of schema review, not an afterthought

## 5.6 Error handling

Choose one clear error approach and use it consistently:

* GraphQL spec errors for transport/query-level failures
* Payload-level structured errors for domain validation and business failures

Do not mix inconsistent patterns across mutations without justification.

---

# 6. Versioning and Change Management

## 6.1 Versioning strategy

Use versioning only when you need it, but choose a strategy deliberately.
Common options:

* URL versioning: `/v1/users`
* Header versioning
* Media type versioning
* GraphQL schema evolution with deprecation instead of path versioning

Rules:

* Be consistent across the API surface
* Do not introduce a new version for every minor additive change
* Prefer additive evolution where possible

## 6.2 Breaking changes

Treat these as breaking unless clearly documented otherwise:

* Removing fields
* Renaming fields
* Changing field types incompatibly
* Changing validation semantics in a stricter way
* Changing pagination or ordering guarantees unexpectedly
* Changing auth requirements for existing clients

## 6.3 Deprecation

* Mark deprecated fields or endpoints clearly
* Document replacement paths
* Give clients enough migration time for the API audience
* Track deprecations in docs and changelogs

---

# 7. Security and Access Rules

* Authenticate at the correct boundary
* Authorize every sensitive operation and data access path
* Never trust client-supplied ownership or tenant context without verification
* Validate all external input
* Sanitize user-controlled content where relevant
* Rate limit sensitive or abuse-prone endpoints
* Protect secrets and tokens
* Verify signatures for webhooks and callbacks
* Minimize overexposure of fields, especially internal, admin, or sensitive attributes
* Default deny when authorization is unclear

---

# 8. Performance and Reliability Rules

* Avoid N+1 query patterns in REST aggregations and GraphQL resolvers
* Use pagination for large collections
* Bound expensive filters and sorts
* Design timeouts and retries consciously for downstream calls
* Avoid making one client request trigger uncontrolled fan-out to multiple systems
* Cache only when correctness allows it
* Document eventual consistency where clients need to understand it
* Use async patterns for long-running work

For async workflows:

* Return `202 Accepted` for REST when appropriate
* Provide status polling or webhook callbacks when needed
* Document lifecycle states clearly

---

# 9. Documentation Rules

Every production API design should document:

* Purpose of the API or operation
* Authentication requirements
* Request schema
* Response schema
* Error model
* Pagination, filtering, and sorting behavior
* Rate limits where relevant
* Idempotency behavior where relevant
* Versioning and deprecation policy
* Example requests and responses

For REST, use OpenAPI when possible.
For GraphQL, keep schema docs and field descriptions current.

---

# 10. Review Gates

An API design fails this skill if any of the following are true:

* Endpoints are action-oriented where resource-oriented design should apply
* Method semantics are incorrect
* Status codes are misleading or inconsistent
* Request or response shapes are ambiguous or unstable without reason
* Validation behavior is undocumented or inconsistent
* Pagination, filtering, or sorting rules are unclear
* Error responses are inconsistent or unusable
* Auth or authorization boundaries are weak
* Sensitive fields are overexposed
* Breaking change strategy is missing
* GraphQL schema encourages N+1 or poor evolvability
* Documentation is insufficient for correct adoption

---

# 11. Agent Behavior

When designing or reviewing APIs, the agent should:

1. Choose REST by default for standard CRUD-oriented domains.
2. Use GraphQL when clients clearly benefit from flexible querying, nested graph traversal, or reduced overfetching.
3. Prefer resource-oriented endpoint design for REST.
4. Prefer schema-first design for GraphQL.
5. Enforce consistent naming, status codes, pagination, and error patterns.
6. Call out breaking changes explicitly.
7. Treat auth, validation, and data exposure issues as blocking concerns.
8. Suggest additive changes before proposing breaking changes.
9. Flag N+1 risk in nested GraphQL and aggregation-heavy REST designs.
10. Optimize for client developer experience, not just backend convenience.

---

# 12. Output Format

When asked to design an API, respond with:

1. Recommended API style: REST or GraphQL
2. Rationale
3. Resource or schema design
4. Endpoints or operations
5. Request and response shapes
6. Error model
7. Pagination/filtering/sorting rules
8. Auth and security notes
9. Versioning/deprecation notes
10. Example requests and responses

When reviewing an API, respond with:

1. Verdict
2. Failed design gates
3. Required fixes
4. Suggested improvements
5. Residual risk

---

# 13. Anti-Patterns to Avoid

* Verb-based REST endpoints for standard resource operations
* Using `POST` for every action regardless of semantics
* Returning `200 OK` for validation failures
* Inconsistent naming between similar resources
* Deeply nested URLs that mirror internal implementation rather than client needs
* Undocumented query parameters
* Free-form status strings where enums are better
* GraphQL schemas that expose internal storage structure directly
* Mutations with many loose scalar arguments instead of input objects
* Unbounded list fields without pagination
* Resolver implementations that create N+1 queries
* Breaking changes shipped without deprecation or migration guidance

---

# 14. Default Standard

If no project-specific API convention overrides this skill, default to:

* REST for standard application APIs
* Resource-oriented URL design
* Correct HTTP semantics
* Consistent error envelopes
* Offset pagination for simple internal APIs, cursor pagination for large or user-facing feeds
* GraphQL with schema-first design and connection-style pagination when GraphQL is chosen
* Strong validation at boundaries
* Stable auth and authorization rules
* Additive evolution before breaking changes
* Documentation that lets a client integrate without guessing
