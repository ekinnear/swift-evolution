# The Swift Networking Workgroup Evolution Process

This document describes how the Swift Networking Workgroup (NWG) applies the [Swift evolution process](https://github.com/swiftlang/swift-evolution/blob/main/process.md) to changes it governs. It is an addendum, not a replacement: everything in the main process applies unless explicitly noted here. Substantial changes to this document require approval from the Core Team or the overseeing steering group.

If you are proposing a change and are not sure whether it falls under the NWG, contact a workgroup member on the [Swift forums](https://forums.swift.org/c/development/networking/129) or the [workgroup Slack channel](https://swift-open-source.slack.com/archives/C0BJMU6842G).

## Scope

The Networking Workgroup governs the evolution of the packages and APIs called out in the [Networking Vision](https://github.com/swiftlang/swift-evolution/blob/main/visions/networking.md), including:

- Shared **currency types** for the networking stack (for example, IP addresses, ports, endpoints, and HTTP types).
- **HTTP client and server APIs**, and the abstractions they build on.
- A **unified networking stack**: transport, TLS, protocol composition, and read/write abstractions.
- Related packages transferred to or created under `swiftlang` on the NWG's behalf.

Anything that the Core Team has not placed under the NWG's authority is not covered by this document. When a proposal touches another evolution area as well, such as the language or the standard library, the NWG works with that area's evolution workgroup to decide how the proposal is reviewed.

### Design, not implementation

The process applies to the **design** of a feature, not to its implementation or its documentation. Implementation and documentation work is open source and goes through the normal code review process on the relevant repository; see [Contributing to Swift](https://www.swift.org/contributing/). Bug fixes, optimizations, performance work, and test improvements can be contributed at any time without evolution review.

There is one important exception: a patch that changes a design the workgroup has already reviewed should not be merged without the approval of the NWG. This includes a bug fix, if the bug allows additional things to be expressed or if it changes user-visible behavior. A bug that has not yet been released can be fixed freely. If you are not sure which side of the line a change falls on, please ask the workgroup before merging it.

### Experimental features

The process does not cover **experimental features**, which may be added, changed, or removed at any time through the normal code review process. Packages under the NWG put these behind an explicit opt-in, such as an experimental package trait, so that they cannot be used by accident. An experimental feature is unstable by definition: there are no source compatibility guarantees for it, and there is no commitment that it will ever ship.

Experimental status is a staging area, not a destination. When an API is ready to become part of a package's stable, supported surface, it goes through the full process described below, starting with a pitch. An experimental feature with no clear path to that point should be removed rather than left in place indefinitely. Each package's `CONTRIBUTING.md` covers the day-to-day mechanics of working behind the experimental opt-in.

### Tools

As in the main Swift evolution process, the design of tools falls outside the evolution process. This includes IDEs, debuggers, profilers, packet capture and analysis tools, and documentation generators. The workgroup may offer guidance or recommendations for these tools, but that guidance is not reviewed, and recommendations for tools that are developed outside the Swift project are not binding.

## Roles

- **Author(s)** — Propose ideas, write the proposal, respond to feedback, and revise as needed.
- **Review Manager** — Appointed by the NWG for each proposal to shepherd it through review, relay workgroup feedback, open the review thread, and communicate the decision. The review manager is a workgroup member and is not one of the authors.
- **Networking Workgroup** — Approves visions and roadmaps, appoints review managers, and makes decisions on proposals within its scope.
- **Community** — Anyone may pitch, discuss, and review. Feedback may be public on the forums or sent privately to the review manager.

The current workgroup roster is maintained on the [Swift Networking Workgroup page](https://www.swift.org/networking-workgroup/).

## Document types

The NWG uses the three document types from the main process:

- **Vision** — A high-level design for a broad topic. Requires workgroup approval but does not go through open review; approving a vision endorses its basic ideas, not any specific proposal that comes out of it. The [Networking Vision](https://github.com/swiftlang/swift-evolution/blob/main/visions/networking.md) is the workgroup's anchor.
- **Roadmap** — A planning document that breaks a large change into individually reviewable proposals. Does not itself go through review. The NWG expects roadmaps for large multi-proposal efforts so the community can see the sequence and each proposal that follows can stay focused.
- **Proposal** — A specific proposed change; goes through open review.

Every proposal should link the vision (and roadmap, if any) it derives from in its header, so the chain from vision to shipped change stays visible.

## Where discussion happens

- **Pitches**: the [Evolution > Pitches](https://forums.swift.org/c/evolution/pitches/5) category on the Swift forums, tagged `networking`.
- **Reviews**: the [Evolution > Proposal Reviews](https://forums.swift.org/c/evolution/proposal-reviews/15) category on the Swift forums, tagged `networking`. The review manager opens the thread.
- **General discussion, questions, and design conversations**: the [Networking category](https://forums.swift.org/c/development/networking/129).
- **Real-time / informal**: the [workgroup Slack channel](https://swift-open-source.slack.com/archives/C0BJMU6842G).
- **Workgroup meetings**: roughly bi-weekly public meetings, announced on the forums. Meetings are for discussion and alignment; decisions still happen on the forums so people who cannot attend a specific timeslot can participate fully.

## Where proposals live

NWG proposals live in the shared [`swiftlang/swift-evolution`](https://github.com/swiftlang/swift-evolution) repository under `proposals/networking/`, using the prefix **`SN-`**.

This follows the pattern the Testing Workgroup already uses (`proposals/testing/`, `ST-` prefix) and keeps NWG proposals in the same place the community already watches for evolution activity. Reviews, templates, and tooling are shared with the rest of Swift Evolution.

## Stages of the process

The NWG uses **full evolution review** — pitch and open review are separate, explicit steps.

### 1. Pre-pitch

Before pitching, search the forums and the [commonly-rejected proposals list](https://github.com/swiftlang/swift-evolution/blob/main/commonly_proposed.md) for prior discussion. If a related thread exists, link it in the pitch.

### 2. Pitch

Open an informal thread in **Evolution > Pitches**, tagged `networking`. Describe the problem and possible solutions; a formal proposal document is not required yet. Pitch threads are where the shape of a solution gets worked out, and often where the workgroup and community identify open questions worth resolving before a proposal is drafted.

For larger efforts, a pitch may lead to a **vision** or **roadmap** rather than jumping straight to a proposal.

### 3. Proposal document

Write the proposal using the [Swift proposal template](https://github.com/swiftlang/swift-evolution/blob/main/proposal-templates/0000-swift-template.md). Store it under `proposals/networking/` in the [swift-evolution repository](https://github.com/swiftlang/swift-evolution), using the prefix **`SN-`**.

The proposal header must include, in order:

- `Proposal` — formatted `[SN-NNNN](filename.md)`
- `Author(s)`
- `Review Manager(s)`
- `Status` (bolded)
- Optional but strongly encouraged: `Vision`, `Roadmap`, `Bug`, `Implementation`, `Previous Proposal`, `Previous Revision(s)`
- `Review` — space-separated parenthesized links to forum threads (pitch, review, acceptance, and so on), following the [standard label grammar](https://github.com/swiftlang/swift-evolution/blob/main/process.md).

Every NWG proposal should set `Vision:` to the networking vision (and `Roadmap:` when it derives from one) so the connection from vision to change is explicit.

### 4. Prototype implementation

**A working prototype implementation is required before a proposal enters review.** It does not need to be production-ready, but reviewers must be able to pull it down, build against it, and evaluate the proposed API in code. Link the prototype from the proposal's `Implementation:` field.

This mirrors the LSG's requirement and reflects that most NWG proposals touch API surface where hands-on evaluation catches problems a document alone cannot.

### 5. Submission

Open a **non-draft pull request** against `swiftlang/swift-evolution` adding the proposal document. Opening the PR is the signal that the proposal is ready for the workgroup to appoint a review manager and schedule review.

### 6. Open review

The review manager opens a review thread in **Evolution > Proposal Reviews**, tagged `networking`, using the standard [review announcement template](https://github.com/swiftlang/swift-evolution/blob/main/process.md#review-announcement-template): proposal link, review end date, "Trying it out" instructions for the prototype, and the "What goes into a review?" prompts.

- Review runs for at least **10 days** and covers at least two consecutive weekends.
- Feedback may be **public** in the review thread or **private** to the review manager.
- Reviews are **not votes**. Decisions are based on judgment about what is best for Swift and the networking ecosystem, not on tallies or intensity of preference.
- Substantial revisions during review may extend the review period, or the review manager may return the proposal for revision and re-open review later.

Reviewers are encouraged to include: their evaluation of the proposal, whether the problem warrants a change, how well the design fits the rest of Swift and the networking vision, comparisons to similar features in other libraries or languages, and concrete usage examples.

### 7. Decision

At the end of the review period the workgroup deliberates and the review manager posts the decision on the forums and updates the proposal's `Status`. Possible outcomes are the standard ones from the main process:

- **Accepted** or **Accepted with revisions**
- **Rejected**
- **Returned for revision**
- **Withdrawn**

For **Accepted with revisions**, the review manager records the required revisions in the decision post and the author updates the proposal accordingly before it moves to implementation.

### 8. Implementation

The change is implemented in the relevant repository (or repositories), and the proposal `Status` is eventually updated to **Implemented** once the change ships in a release (for example, "Implemented (`swift-http-types` 2.0.0)"). Where useful, implementations may ship as a preview package first.

## Alternate paths

The following are the alternate paths defined in the [main process](https://github.com/swiftlang/swift-evolution/blob/main/process.md), applied by the NWG:

- **Summary acceptance** — The workgroup may decide that certain design changes are sufficiently obvious to accept without a proposal document or open review (for example, filling in an overlooked method, forbidding an unsafe use, or gating a change behind an upcoming-feature flag to preserve source compatibility). The NWG errs on the side of running a normal review in close cases, and announces summary-accepted changes on the forums and in the affected package's release notes.
- **Summary rejection** — The workgroup may reject proposals without review when it believes there is no possibility of acceptance. Reasons are clearly communicated on the pitch thread. The NWG treats summary rejection as a last resort and uses it only when a full review would not add information.
- **Returned for revision** — Substantial changes made during review may result in the proposal being returned to the author. If the revised proposal is substantially different from what was reviewed, the workgroup may ask the author to re-pitch before opening a new review.

## Focus areas

Each Swift release has documented focus areas. The NWG maintains its own working priorities as part of the [Networking Vision](https://github.com/swiftlang/swift-evolution/blob/main/visions/networking.md) and its ongoing planning; off-focus proposals are not automatically excluded, but the workgroup may ask that they be deferred so effort concentrates on the current focus.

## Related

- [Swift Evolution Process](https://github.com/swiftlang/swift-evolution/blob/main/process.md) — the process this document extends.
- [Networking Vision](https://github.com/swiftlang/swift-evolution/blob/main/visions/networking.md)
- [Swift Networking Workgroup charter](https://www.swift.org/networking-workgroup/)
- [Networking forums category](https://forums.swift.org/c/development/networking/129)
- [Swift Code of Conduct](https://www.swift.org/code-of-conduct/)
