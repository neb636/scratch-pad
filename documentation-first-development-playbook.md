# Documentation-First Development Playbook

A playbook for building better APIs through structured planning, AI-assisted brainstorming, and documentation-first design. Write the docs, then build to spec — better end results for consumers, and a living reference that keeps AI aligned.

---

## Step 1: Brainstorm the API Design

````prompt
API brainstorming session.

## Problem
[What you're solving]

## Constraints
- Consumers: [Who uses this?]
- Patterns: [Codebase conventions]
- Integrates with: [Dependencies]

## Initial Idea (optional)
```typescript
function doSomething() {}
```

Explore 2-3 alternatives. For each: basic usage, pros/cons, edge case handling.
````

**Tip:** Push back. Ask "what are the tradeoffs?" and "how would this look optimized for X?"

---

## Step 2: Draft the Documentation

```prompt
Create a README.md for this API:

1. **Overview** - 2-3 sentences (concise)
2. **API Reference** - Signatures, params, returns, examples
3. **Code Usage Examples** - 2-3 real scenarios
```

Iterate with the LLM until the API design feels right.

---

## Step 3: Implement Against the Documentation

```prompt
Implement exactly as documented.

- Match signatures precisely
- Flag ambiguities rather than assuming
- Surface design flaws discovered during implementation
```

**Key:** If implementation wants to deviate, update docs first.

---

## Step 4: Critical Review

### 4a. Self-Critique

```prompt
Review this API critically:
- Ergonomics, consistency, flexibility, simplicity, naming

Suggest improvements ranked by impact.
```

### 4b. Hands-On Validation

Use the API realistically. Note friction points, unclear errors, "I wish it did X" moments. Refine accordingly.

---

## Step 5: Testing

Use the unit testing process as a chance to both validate docs AND hunt bugs.

```prompt
For: file-path/feature-name

Write unit tests that both validate the documentation and actively hunt for bugs.

1. Documentation Validation
- Test each documented behavior, edge case, and example
- Flag discrepancies: note if the *code* or *docs* are wrong
- Mark ambiguities with // TODO: clarify docs

2. Bug Hunting - Try to break the API using:
- Boundary values (empty, zero, negative, max)
- Invalid inputs (wrong types, null, malformed data)
- State abuse (out-of-order calls, double calls)
- Concurrency and resource exhaustion (if applicable)

For bug hunt tests, briefly note what you're trying to break and why it might fail.

Failing tests are acceptable when they expose real bugs and issues. Report discovered issues at the end for user verification.
```

**Results:**

- Failing validation → fix code or update docs?
- Failing bug hunt → fix root cause
- Unexpected passes → docs may understate robustness

---

## Step 6: Finalize

```prompt
List discrepancies between docs and implementation. For each: describe difference, recommend fix location.
```

Update docs with testing discoveries. Verify README still matches reality.

---

## Tips

- **Keep docs in context** — reference README in prompts
- **Start minimal** — easier to add than remove
- **Name for consumers** — domain terms, not implementation
- **Document the "why"** — rationale for non-obvious decisions
