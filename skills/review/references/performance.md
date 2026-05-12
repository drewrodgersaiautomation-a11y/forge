# Performance Review Checklist

## Database

- [ ] No N+1 queries: loops that execute queries per iteration without batching
- [ ] Indexes exist for all columns used in WHERE, JOIN ON, and ORDER BY clauses in hot paths
- [ ] Queries fetch only the columns needed — no `SELECT *` in production code
- [ ] Large result sets are paginated — no unbounded queries
- [ ] Transactions are scoped appropriately — not wrapping operations that don't need atomicity

## Network & I/O

- [ ] External HTTP calls in request handlers are either async/non-blocking or moved to background jobs
- [ ] No blocking I/O (disk reads, synchronous HTTP, sleep) in paths that serve user-facing requests
- [ ] Repeated external calls within a request lifecycle are batched or cached where possible
- [ ] Timeouts are set on all outbound HTTP calls

## Memory

- [ ] No unbounded in-memory accumulation: collections that grow proportionally to dataset size
- [ ] Large objects or buffers are explicitly released when no longer needed
- [ ] Streaming is used for large file reads/writes instead of loading into memory

## Compute

- [ ] No O(n²) or worse algorithms in paths that operate on user-supplied data sizes
- [ ] Expensive computations run outside of request handlers (background jobs, caching)
- [ ] Regex patterns on user input are not catastrophically backtracking (ReDoS)

## Caching

- [ ] Cacheable data (reference data, computed aggregates) has an appropriate cache strategy
- [ ] Cache invalidation is correct — stale data cannot be served after writes
- [ ] Cache keys are deterministic and include all relevant dimensions
