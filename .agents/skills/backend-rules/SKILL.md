---
name: backend-rules
description: Use this skill when implementing or reviewing backend API/service code, including schema contracts, input validation, DB pooling, timeout/deadline control, bounded retries, and latency/request logging requirements.
---

# Backend Rules

## When To Use
- Use for backend API or service implementation/review tasks.
- Do not use for frontend-only work.

## Rules
- Must define explicit request/response schemas for APIs;
  do not return ad-hoc untyped payloads.
- Must validate and sanitize all external inputs at boundary layers.
- Must use process-wide DB connection management with pooled clients;
  avoid per-request connection creation.
- Must ensure all queries and external calls use explicit timeouts, cancellable context, and explicit deadlines;
  no unbounded waits.
- Must retry only transient failures with bounded exponential backoff and jitter;
  never retry non-idempotent operations unless idempotency is guaranteed;
  must cap retries with `max_retries=3` by default unless the user explicitly requests otherwise;
  must log the final failure reason and total retry elapsed time when `max_retries` is exhausted.
- Must use async for FastAPI request handlers and I/O-bound paths;
  blocking calls in the event loop are prohibited;
  blocking I/O must be offloaded to thread pools;
  CPU-bound work must be offloaded to process pools (or background workers).
- Must record end-to-end request latency in milliseconds for every endpoint;
  must separately measure DB latency and external-call latency (including timeout counts).
- Must log request/response content for every endpoint.
