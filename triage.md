# From candidate to proven finding

A candidate is a shape that looks wrong. A finding is a candidate with a runnable proof and a named impact. The steps between them are where most reports are won or lost.

## 1. Read the siblings

Before you commit to a hypothesis, read every sibling function. Auditors fix one path and leave the next one. A check present in one handler and missing in the next is the most reliable source of real findings.

## 2. Check the project's own record

Search the repository for `security/`, `AUDIT`, `KNOWN_ISSUES`, and closed issues. A finding that already appears in the project's audit trail is a duplicate and will not be rewarded. Note it and move on, unless the surviving code still has the gap.

## 3. Build the smallest failing case

Fork the chain at the deployed block, or run the unit tests the project already has. Then write the test that fails on the current code and passes on the fix. A test that needs a mainnet transaction is a test you cannot run; prefer a local fork.

## 4. Name the money path

Write down, in one sentence, how value moves from the victim to the attacker. If you cannot, the finding is a defence-in-depth gap, and that is what you should say. Rating a gap as a theft is how reports get dismissed.

## 5. Rate it against the program

Match the class to the program's own severity table, not to your enthusiasm. Then read the out-of-scope list. Rate limiting, best-practice gaps, and known issues are usually ineligible.

## 6. Write the report

Title, affected component, severity, summary, root cause, reproduction, impact, fix. Send it privately. Keep the proof attached. Then stop: no public post, no thread, until the maintainer confirms a fix.
