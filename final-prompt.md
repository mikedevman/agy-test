# M1 Prompt — SRS Generation with User Stories and Traceability

You are a requirements engineer. Your task is to produce a complete Software
Requirements Specification (SRS) for the system described below, in which every
functional requirement is expressed as a user story with acceptance criteria.

---

## Input: Domain Requirements

### Order Management System — Domain Requirements

#### 1. Introduction & Business Roles

This document outlines the requirements for a standard order management
platform. The system interactions revolve around three primary roles:

- **Customer** — the end-user browsing, purchasing, and managing their items.
- **OrderStaff** — internal staff responsible for receiving, validating and
  fulfilling orders.
- **Accountant** — internal staff responsible for invoicing and for recording
  payments received.

#### 2. Functional Requirements (FR)

- **REQ-F-01**: The system shall store a name, an address and a phone number for each customer.
- **REQ-F-02**: The system shall allow a customer to have at most one bank account, which is optional.
- **REQ-F-03**: The system shall store a name, a description, a price and an image for each product.
- **REQ-F-04**: The system shall allow a product to be referred to by any number of order items, including none, and shall keep a product in existence independently of the order items that refer to it.
- **REQ-F-05**: The system shall record each order with an order date, a total amount, a status and a payment method.
- **REQ-F-06**: The system shall record each order item with a quantity, a unit price and a reference to exactly one product, and shall associate each order item with exactly one order.
- **REQ-F-07**: The system shall keep an order item in existence only as part of the order it belongs to, shall not allow an order item to be moved to another order, and shall remove the order items of an order when that order is removed.
- **REQ-F-08**: The system shall associate each order with exactly one customer, while a customer may have any number of orders.
- **REQ-F-09**: The system shall record each invoice with a date, an amount, a status and a payment method.
- **REQ-F-10**: The system shall allow at most one invoice per order, and shall associate each invoice with exactly one order.
- **REQ-F-11**: The system shall record each payment with a date, an amount, a status and a payment method.
- **REQ-F-12**: The system shall allow any number of payments against one invoice, and shall record each payment against exactly one invoice rather than directly against an order.
- **REQ-F-13**: The system shall allow a customer to submit an order that names a known customer, contains one or more order items each referring to an existing product, and carries a payment method, and shall register it as an order with the submission date as its order date and the status submitted.
- **REQ-F-14**: The system shall reject an order submission if the customer is not known to the system, and shall register no order.
- **REQ-F-15**: The system shall reject an order submission that contains no order item, and shall register no order.
- **REQ-F-16**: The system shall reject an order submission if any order item refers to a product that does not exist, and shall register no order.
- **REQ-F-17**: The system shall record for each registered order a total amount equal to the sum over its order items of quantity multiplied by unit price.
- **REQ-F-18**: The system shall allow order staff to receive an order whose status is submitted by setting its status to pending.
- **REQ-F-19**: The system shall reject an attempt to receive an order if the status of the order is not submitted, and shall leave the status unchanged.
- **REQ-F-20**: The system shall allow order staff to mark an order whose status is pending as filled.
- **REQ-F-21**: The system shall reject an attempt to mark an order as filled if the status of the order is not pending, and shall leave the status unchanged.
- **REQ-F-22**: The system shall allow order staff to decline an order whose status is pending by setting its status to closed.
- **REQ-F-23**: The system shall reject an attempt to decline an order if the status of the order is not pending, and shall leave the status unchanged.
- **REQ-F-24**: The system shall reject a request to raise an invoice for an order that has been declined.
- **REQ-F-25**: The system shall allow order staff to set the status of an order to shipped when its status is filled.
- **REQ-F-26**: The system shall reject an attempt to set an order to shipped if the status of the order is not filled, and shall leave the status unchanged.
- **REQ-F-27**: The system shall leave the status of an invoice and of any payment against that invoice unchanged when an order is set to shipped.
- **REQ-F-28**: The system shall allow an accountant to raise an invoice for an order whose status is filled or shipped and that has no invoice, with a date, an amount, a payment method and the status issued.
- **REQ-F-29**: The system shall reject a request to raise a further invoice for an order that already has one.
- **REQ-F-30**: The system shall reject a request to raise an invoice for an order whose status is submitted, pending or closed.
- **REQ-F-31**: The system shall let invoicing and shipping proceed independently of each other once an order has been filled, so that raising an invoice does not require the order to have been shipped, setting the order to shipped does not require an invoice to have been raised, and the two may occur in either order or at the same time.
- **REQ-F-32**: The system shall allow a customer to submit a payment against an invoice whose status is issued, with a date, an amount and a payment method, and shall record the payment with the status pending.
- **REQ-F-33**: The system shall reject a payment submitted against an invoice whose status is paid.
- **REQ-F-34**: The system shall allow a further payment to be submitted against an invoice whose earlier payment has the status failed, shall record it as a separate payment with the status pending, and shall keep the failed payment at the status failed.
- **REQ-F-35**: The system shall allow an accountant to confirm a payment whose status is pending by setting its status to completed.
- **REQ-F-36**: When an accountant confirms a pending payment against an invoice whose status is issued, the system shall set the status of that invoice to paid.
- **REQ-F-37**: The system shall leave the status of the order billed by an invoice unchanged when a payment against that invoice is confirmed.
- **REQ-F-38**: The system shall allow an accountant to reject a payment whose status is pending by setting its status to failed, and shall leave the status of its invoice and of its order unchanged.
- **REQ-F-39**: The system shall reject an attempt to confirm or to reject a payment whose status is not pending, and shall leave the status unchanged.
- **REQ-F-40**: The system shall allow order staff to close an order whose status is shipped and whose invoice has the status paid, by setting its status to closed.
- **REQ-F-41**: The system shall reject an attempt to close an order whose status is shipped if its invoice does not have the status paid, and shall leave the status unchanged.
- **REQ-F-42**: The system shall reject an attempt to close an order whose invoice has the status paid if the status of the order is not shipped, and shall leave the status unchanged.
- **REQ-F-43**: The system shall close a filled order only after both the shipping of the order and the settlement of its invoice have completed, whichever of the two finishes last.
- **REQ-F-44**: The system shall not change the status of an order whose status is closed.
- **REQ-F-45**: The system shall treat every attribute as mandatory, except the bank account of a customer, and shall reject a customer record or a product record in which a mandatory attribute is absent.
- **REQ-F-46**: The system shall represent monetary values (product price, unit price, order total, invoice amount, payment amount) as decimal numbers.
- **REQ-F-47**: The system shall restrict the status of an order to submitted, pending, filled, shipped or closed; of an invoice to issued or paid; and of a payment to pending, completed or failed.
- **REQ-F-48**: The system shall restrict the payment method recorded on an order, on an invoice and on a payment to bank, card or cash.
- **REQ-F-49**: The system shall change the status of an order only from submitted to pending, from pending to filled or to closed, from filled to shipped, and from shipped to closed.
- **REQ-F-50**: The system shall change the status of an invoice only from issued to paid, and the status of a payment only from pending to completed or to failed.

#### 3. Non-Functional Requirements (NFR)

- **REQ-N-01**: When a user submits an order containing up to 50 order items under normal operating conditions, the system shall register the order and respond within 2 seconds for at least 95% of submissions.
- **REQ-N-02**: Under normal operating conditions, the system shall support at least 200 concurrent users and at least 20 order submissions per second while meeting the response time of REQ-N-01.
- **REQ-N-03**: The system shall be available for at least 99.5% of each calendar month, excluding scheduled maintenance announced at least 24 hours in advance.
- **REQ-N-04**: When a server failure occurs, the system shall resume accepting requests within 15 minutes without losing any order, invoice or payment recorded before the failure.
- **REQ-N-05**: The system shall authenticate every user before granting access to any customer, order, invoice or payment data, and shall reject 100% of unauthenticated requests.
- **REQ-N-06**: The system shall allow only users holding the accountant role to confirm or reject a payment, and shall reject the same request from any other user.
- **REQ-N-07**: The system shall protect customer personal data and bank account numbers by encrypting them in transit with TLS 1.2 or higher and at rest.
- **REQ-N-08**: The system shall record the user and the time of every status change of an order, an invoice and a payment, and shall retain these records for at least 12 months.

---

## Requirement Style

### Functional requirements — user story form

Every requirement in clause 3.1 (Functional requirements) shall be stated as a
user story in exactly this template, on a single line:

> As a `<role>`, I want `<capability>`, so that `<benefit>`.

Rules:

- `<role>` shall be one of the roles named in the input domain requirements
  (Customer, OrderStaff, Accountant). Do not invent other roles.
- `<capability>` shall name one capability that the role obtains from the
  system, phrased as that role would phrase it.
- `<benefit>` shall state why the role wants it, not restate the capability.
- The story line shall not contain the word "shall".

### Granularity of functional requirements

A user story is a unit of **business intent**, not a unit of input text.
Determine for yourself what the distinct units of business intent are in the
input functional requirements, and state one story for each. Justify the
granularity you choose by the business process, not by the number of input
requirements: one input requirement may be realized by several stories, and one
story may realize several input requirements.

Everything that governs a story — the conditions under which the capability is
refused, the attributes and permitted value sets it reads or writes, the
multiplicities and lifetimes of the entities it relates, and its consequences
for other entities — belongs in the acceptance criteria of that story.

Where an input requirement states a rule that governs several stories (for
example a table of permitted status changes, or the permitted set of payment
methods), place it in the acceptance criteria of each story it governs, phrased
for that story.

### Acceptance criteria

Each user story shall be followed by at least three acceptance criteria, with
no upper limit. Each acceptance criterion shall be written in one of two
forms, and the form used shall be recorded in the machine-readable listing:

- **Given-When-Then** — `Given <precondition>, When <trigger>, Then <expected
  observable outcome>.` Use this form for a criterion that describes what
  happens when something occurs.
- **Condition** — a single declarative constraint that holds independently of
  any trigger. Use this form for a criterion that states a permitted value set,
  a data type, a multiplicity, a lifetime, or a permitted status change.

One criterion states one rule. A rule whose statement needs several clauses
stays in one criterion; two rules that govern different triggers stay in two.

Each acceptance criterion shall be independently verifiable: a reader shall be
able to determine, by observing the system, whether it holds. Criteria such as
"the interface is user-friendly" are not acceptable.

### Non-functional requirements — declarative form

Requirements in clause 3.2 (quality attributes) shall **not** be written as
user stories. They shall be written as single declarative statements using
"shall", each with a quantified, measurable threshold where the property admits
one. A non-functional requirement carries no acceptance criteria.

### Identifiers

- Functional requirements: `US-NN`, numbered from `US-01` upward, no gaps.
- Non-functional requirements: `NFR-NN`, numbered from `NFR-01` upward, no gaps.
- Acceptance criteria: `<requirement-id>-ACNN`, e.g. `US-01-AC01`, numbered from
  `01` within each requirement, no gaps.

Identifiers shall match the regular expressions `^US-\d{2}$`, `^NFR-\d{2}$` and
`^US-\d{2}-AC\d{2}$` respectively, and shall be identical across `srs.md`,
`requirements.json` and `VMX.csv`.

### Order of requirements

Functional requirements shall appear in clause 3.1 in the order in which the
capabilities they specify are first reached in the input functional
requirements, and shall be numbered `US-01` upward in that order.

Non-functional requirements shall be grouped by the quality attribute that
governs them and shall appear in clause 3.2 in the order of its subclauses:
first every performance requirement (3.2.1), then every security requirement
(3.2.2), then every availability requirement (3.2.3). Within one subclause they
shall keep the relative order of the input non-functional requirements they
originate from. They shall be numbered `NFR-01` upward across the whole of
clause 3.2 in that order, so that the numbering follows the subclauses and
**not** the order of the input non-functional requirements.

Every requirement originating from an input FR shall be specified in clause 3.1
with a `US-` identifier. Every requirement originating from an input NFR shall
be specified in clause 3.2 with an `NFR-` identifier.

---

## Output Standard

`srs.md` shall contain the following clauses, in this order, with these
headings:

1. Introduction
   1. Purpose
   2. Scope
   3. Definitions and acronyms
2. Overall description
   1. Product perspective
   2. Product functions
   3. User characteristics
   4. Assumptions and dependencies
3. Requirements
   1. Functional requirements
   2. Quality attributes
      1. Performance
      2. Security
      3. Availability
4. Verification
5. Supporting information

Clause 3.1 holds every functional requirement. Clause 3.2 holds every
non-functional requirement, each placed in the one subclause that names its
quality attribute.

---

## Diagrams

The SRS must include two UML diagrams, both expressed in PlantUML source.
Each diagram is delivered as its own file (see "Output Files" below), not
inside the SRS document.

### Diagram 1 — Structural Model

Open with `@startuml structural` and close with `@enduml`. It must show:

- Domain classes with meaningful names
- Attributes with explicit data types
- An `enum` for every attribute whose input requirements restrict it to a fixed
  set of values, declaring one literal per permitted value, with the attribute
  typed by that enum rather than by a general-purpose type such as `String`
- Relationships between classes (association, aggregation, composition,
  generalization) with multiplicities on both ends. Where an entity has no
  meaning apart from the entity it belongs to, model the relationship as a
  composition rather than a plain association.

### Diagram 2 — Behavioral Model

Open with `@startuml behavioral` and close with `@enduml`. It must show:

- Exactly one initial node and at least one final node
- Decision nodes, each with an explicit guard condition on every outgoing flow
- Actions with meaningful names, each connected to the control flow
- A fork and a matching join wherever the input requirements describe work that
  proceeds without waiting for other work to finish, so that the branches are
  shown in parallel rather than in an arbitrary sequence
- A loop wherever the input requirements allow a step to be attempted again
  after it has failed
- An object node after each action that leaves an entity in a new status,
  written as the entity name followed by the status in square brackets, for
  example `:Order [submitted];`

The diagram shall be partitioned into swimlanes, declared with the `|...|`
syntax. Every action shall lie within the swimlane of the role that performs it.

---

## Output Files

Write exactly the following five files, using exactly these file names, in the
current working directory. Do not create any other files, and do not rename,
add prefixes or suffixes, or place them in subfolders.

| File name | Content |
| --- | --- |
| `srs.md` | The SRS document in Markdown, following the clause structure above. It is prose only: it shall not contain the traceability matrix, the PlantUML source or the JSON listing. Where the SRS refers to the diagrams, the traceability matrix or the requirements listing, refer to them by file name (`structural.puml`, `behavioral.puml`, `VMX.csv`, `requirements.json`). |
| `structural.puml` | The complete Diagram 1 source, from `@startuml structural` to `@enduml`. Raw PlantUML only: no Markdown fences, no prose. |
| `behavioral.puml` | The complete Diagram 2 source, from `@startuml behavioral` to `@enduml`. Raw PlantUML only: no Markdown fences, no comments. |
| `requirements.json` | A machine-readable listing of every requirement you specified in `srs.md`. Raw JSON only: no Markdown fences, no comments. |
| `VMX.csv` | The traceability matrix (see "Traceability"). Raw CSV only: no Markdown fences, no comments, no prose. |

### Format of `requirements.json`

The file content is a single JSON object, encoded in UTF-8 without a
byte-order mark. The object has exactly the following members:

| Field | JSON type | Description |
| --- | --- | --- |
| `version` | string | The version of this listing. Use `1.1`. |
| `updated` | string | The date of the input domain requirements, as `YYYY-MM-DD`. Use `2026-10-21`. |
| `requirements` | array | Every requirement specified in `srs.md`, as requirement objects (see below). |

Each requirement object has exactly the following members. Every member is
mandatory and shall be present on every object. Where no value applies, use an
empty string or an empty array — never `null`, and never omit the member. Do
not add any member that is not listed here.

| Field | JSON type | Description |
| --- | --- | --- |
| `id` | string | The requirement identifier as used in `srs.md`. Matches `^US-\d{2}$` or `^NFR-\d{2}$`. Unique across the array. |
| `type` | string | Exactly one of: `functional` (clause 3.1), `performance` (3.2.1), `security` (3.2.2), `availability` (3.2.3). The value shall name the clause of `srs.md` in which the requirement appears. Every requirement whose `id` matches `^US-` has type `functional`; no requirement whose `id` matches `^NFR-` has type `functional`. |
| `statement` | string | The full requirement statement exactly as it appears in `srs.md`, verbatim, on one line. For a functional requirement this is the complete "As a ..., I want ..., so that ..." sentence. |
| `acceptance_criteria` | array | An array of acceptance criterion objects (see below). At least three elements where `type` is `functional`, with no upper limit; the empty array for every other type. |

Each acceptance criterion object has exactly the following members, and no
others:

| Field | JSON type | Description |
| --- | --- | --- |
| `id` | string | Matches `^US-\d{2}-AC\d{2}$`. Its requirement-id prefix equals the `id` of the enclosing requirement. Unique across the whole file. |
| `format` | string | Exactly one of: `given_when_then`, `condition`. |
| `text` | string | The complete criterion as a single line, verbatim as it appears in `srs.md`. Where `format` is `given_when_then`, the text begins with `Given `, and contains `, When ` and `, Then `. |

This listing records no traceability: the link from a specified requirement
back to its domain requirement identifier is held only in `VMX.csv`.

Further constraints on the listing:

- The `requirements` array shall contain exactly the requirements specified in
  `srs.md` — no more, no fewer — and in the same order in which they appear in
  `srs.md`.
- Identifiers, statements and criterion texts in the listing shall be byte-identical
  to their occurrences in `srs.md`, apart from Markdown emphasis markers.
- No member shall contain a newline character.
- The file shall parse as valid JSON on the first attempt. Do not emit trailing
  commas, comments, or any text before or after the top-level object.

---

## Traceability

Write the traceability matrix to `VMX.csv`. It maps each specified requirement
to the domain requirement(s) it originates from and to the corresponding
diagram element(s). `VMX.csv` is the only file that records the link between a
specified requirement and the domain requirement it originates from.

### Format of `VMX.csv`

- The first row is the header, exactly: `SRS-Req-ID,Domain-Req-ID,Structural-Elements,Behavorial-Elements`
- Each following row describes exactly one requirement specified in `srs.md`.
  There shall be exactly one row per requirement, and the `SRS-Req-ID` values
  shall match the identifiers in `srs.md` and `requirements.json` exactly, in
  the same order.
- Separate the columns with commas. Enclose a cell in double quotes when it
  contains a comma or a double quote.
- When a cell lists several values, separate the values with semicolons.
- If no value applies to a cell, leave it empty.

| Column | Description |
| --- | --- |
| `SRS-Req-ID` | The identifier of the requirement as used in `srs.md` |
| `Domain-Req-ID` | The identifier(s) of the domain requirement(s) from which the requirement originates, copied character for character from the input domain requirements. Each identifier shall match `^REQ-F-\d{2}$` or `^REQ-N-\d{2}$`. Do not abbreviate, renumber or reformat them. One domain requirement may appear in several rows, and one row may list several domain requirements. Leave the cell empty if the requirement is derived rather than traced to a domain requirement. |
| `Structural-Elements` | The names of the classes, enums or attributes (written `Class.attribute`) declared in `structural.puml` that realize the requirement. Write each name exactly as it is declared in `structural.puml`. Do not list relationships here. |
| `Behavorial-Elements` | The names of the actions declared in `behavioral.puml` that realize the requirement. Write each name exactly as it is declared in `behavioral.puml`. Do not list decisions, object nodes, or control nodes (initial, final, fork, join, merge) here. |