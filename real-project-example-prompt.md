# ================================================================
# AQUifier RESOURCE — REQUIREMENT GATHERING + ARCHITECTURE R&D
# ================================================================

# STOP — REQUIREMENT GATHERING + R&D ONLY

DO NOT IMPLEMENT CODE.

DO NOT MODIFY PRODUCTION SOURCE CODE.

DO NOT CHANGE EXISTING FEATURES.

DO NOT CREATE PRs.

DO NOT CREATE COMMITS.

DO NOT FIX CURRENT BUGS.

DO NOT CHANGE DATABASE SCHEMAS.

DO NOT CHANGE API IMPLEMENTATIONS.

DO NOT CHANGE EXISTING .agents SOURCE-OF-TRUTH DOCUMENTS.

DO NOT INSTALL DEPENDENCIES.

DO NOT REFACTOR CODE.

This task is ONLY:

    DISCOVERY
    CURRENT-STATE ANALYSIS
    REQUIREMENT GATHERING
    ARCHITECTURE R&D
    CROSS-REPOSITORY ANALYSIS
    API CONTRACT ANALYSIS
    DATA-FLOW ANALYSIS
    RISK ANALYSIS
    TEST STRATEGY
    IMPLEMENTATION PLANNING

The final result must be a requirement/architecture specification
that another implementation agent can use later.

--------------------------------------------------
# ROLE
--------------------------------------------------

You are acting as a:

    Principal Software Architect
    Cross-Repository Research Coordinator
    Multi-Agent R&D Lead

You must analyze the CURRENT implementation of the Autographa
system across FOUR repositories and produce a verified architecture
and requirement specification for a new feature:

    Aquifier Resource inside BT Resource

Do not assume the architecture.

Verify it against:

    1. actual current source code
    2. current repository state
    3. existing .agents documentation
    4. Graphify output
    5. previous source-of-truth/current-system documents

Clearly distinguish:

    VERIFIED CURRENT CODE
    VERIFIED DOCUMENTATION
    INFERENCE
    PROPOSED DESIGN
    UNKNOWN
    CONFLICTING INFORMATION

--------------------------------------------------
# FEATURE BEING INVESTIGATED
--------------------------------------------------

The desired future feature is:

    Aquifier Resource

inside the existing:

    BT Resource

The Aquifier Resource is an independent resource/object.

It must NOT depend on Bible verse mapping.

The intended high-level flow is:

    Aquifier Resource
          ↓
    Resource/Object content
          ↓
    Extract relevant words/content
          ↓
    Build translation JSON
          ↓
    Translation Engine
          ↓
    Receive translated JSON
          ↓
    Identify corresponding Aquifier item
          ↓
    Update ONLY its translation card
          ↓
    Display translation in BT Resource translation panel

Example:

LEFT SIDE

    Aquifier Resource

    ┌─────────────────────────────┐
    │ Object / Resource           │
    │                             │
    │ twelve tribes of Israel     │
    │ twelve tribes               │
    │ ...                         │
    └─────────────────────────────┘

              ↓

           JSON

              ↓

      Translation Engine

              ↓

      translated JSON

              ↓

RIGHT SIDE

    Translation Card

    ┌─────────────────────────────┐
    │ Aquifier item 1              │
    │                             │
    │ translated result            │
    └─────────────────────────────┘

--------------------------------------------------
# CRITICAL REQUIREMENT — NO VERSE MAPPING
--------------------------------------------------

The Aquifier Resource must NOT require:

    Aquifier item → Bible verse

    Aquifier item → GEN 2:1

    Aquifier item → verse ID

    Aquifier item → Scripture reference

The Aquifier Resource is an independent resource/object.

Do NOT assume Bible verse mapping is necessary.

Do NOT reuse Bible verse identity as the primary identity for an
Aquifier item unless the existing implementation proves that this
is required by some unrelated infrastructure.

The translation card should correspond to the Aquifier resource
object/item itself.

IMPORTANT:

    "NO VERSE MAPPING"
    does NOT mean
    "NO IDENTITY".

The system still requires deterministic identity so that a returned
translation can be applied to the correct Aquifier translation card.

Therefore investigate:

    AquifierItemId
        ↓
    TranslationRequest
        ↓
    TranslationResponse
        ↓
    AquifierItemId
        ↓
    TranslationCard

The exact identity mechanism must be discovered from the current
architecture before proposing a new one.

--------------------------------------------------
# CURRENT SYSTEM CONTEXT
--------------------------------------------------

The system consists of:

    1. autographa-app
    2. autographa-dashboard
    3. IndicTrans2
    4. autographa-desktop

Known high-level architecture:

    User
       ↓
    autographa-desktop
       ↓
    autographa-app
       ↓
    Dashboard HTTP APIs
       ↓
    Dashboard / PostgreSQL

IndicTrans2 exists as the translation worker.

The App contains MT UI/client/orchestration.

Dashboard contains API/auth/database infrastructure.

IndicTrans2 contains a translation worker endpoint.

IMPORTANT:

Do NOT treat the above as verified architecture.

Verify every relevant part against the current checkout.

--------------------------------------------------
# PRIOR MT ISSUE — MUST BE RECONCILED, NOT ASSUMED
--------------------------------------------------

There has previously been an MT issue reported as:

    POST /api/v2/mt/translate
    → 403 Forbidden

However, prior current-system research may have found that the
route does not exist on a particular checkout and may therefore
produce a missing-route/404 result instead.

This means:

    403
    vs
    404 / missing route
    vs
    another behavior

MUST be treated as an unresolved historical/current-state discrepancy.

DO NOT assume that 403 is the current behavior.

DO NOT assume that the route is missing either.

Agent 13 MUST determine the actual current state from the current
checkout and reconcile it against prior research.

The report MUST identify:

    exact repository
    branch
    commit
    route path
    route registration
    middleware
    authorization
    controller/service
    actual discovered behavior
    source of the historical 403 claim
    source of any missing-route claim

If two findings came from different branches/commits, explicitly
record that fact.

Do not "fix" the issue.

--------------------------------------------------
# PREVIOUSLY IDENTIFIED ORCHESTRATION / EDITOR RISKS
--------------------------------------------------

Also investigate whether the following previously identified issues
could affect Aquifier:

    httpBusy
    vs
    tryBeginInFlight()

and:

    TipTap / contentEpoch remount behavior

These are investigation targets only.

Do NOT fix them.

Determine whether Aquifier:

    reuses them safely
    triggers them
    worsens them
    requires a separate mechanism

--------------------------------------------------
# REPOSITORIES TO ANALYZE
--------------------------------------------------

You MUST analyze all four repositories:

    1. autographa-app
    2. autographa-dashboard
    3. IndicTrans2
    4. autographa-desktop

Do not analyze only the repository where the UI is expected to
change.

Trace the complete cross-repository flow.

--------------------------------------------------
# EXISTING DOCUMENTATION — MUST BE DISCOVERED FIRST
--------------------------------------------------

Before detailed analysis, inspect:

    .agents/

inside EVERY repository.

Do not assume the exact filenames.

Search the repositories and relevant project/workspace roots for
existing documentation.

Especially look for documents similar to:

    .agents/graphify-bootstrap.md
    .agents/shared-context-current-system.md
    .agents/system-repository-inventory.md
    .agents/app-analysis.md
    .agents/dashboard-analysis.md
    .agents/indictrans2-analysis.md
    .agents/desktop-analysis.md
    .agents/cross-repository-flow.md
    .agents/current-implementation.md
    .agents/api-flow.md
    .agents/data-flow.md
    .agents/current-testing.md
    .agents/adversarial-system-review.md

ALSO explicitly search for:

    AUTOGRAPHA_CURRENT_SYSTEM_ARCHITECTURE.md

IMPORTANT:

AUTOGRAPHA_CURRENT_SYSTEM_ARCHITECTURE.md may be:

    inside .agents/
    at a repository root
    at a cross-repository/project root
    elsewhere in the current workspace

Therefore Agent 1 MUST search the relevant repository roots AND
the common parent/project workspace before concluding that the
document does not exist.

This document is prior current-state research.

If found, read it and use it as evidence.

In particular, investigate its findings concerning:

    MT route existence
    /api/v2/mt/translate
    403 vs missing route
    IndicTrans2 integration
    current architecture

Do not blindly trust it.

Verify its claims against current source code.

--------------------------------------------------
# DOCUMENT EVIDENCE RULE
--------------------------------------------------

For every important architectural finding, identify its evidence.

Use:

    VERIFIED CURRENT CODE
    VERIFIED EXISTING DOCUMENTATION
    GRAPHIFY EVIDENCE
    INFERENCE
    PROPOSED
    UNKNOWN
    CONFLICT

If documentation and source code disagree:

    source code wins

provided the source code is confirmed to be from the current
checkout/branch/commit being analyzed.

Always record the branch/commit when it matters.

--------------------------------------------------
# GRAPHIFY REQUIREMENT
--------------------------------------------------

Before the main R&D:

Search every relevant repository for existing Graphify output.

Search for:

    graphify
    graphify.json
    graphify output
    dependency graph
    architecture graph
    generated repository graph
    graph visualization

If valid Graphify output already exists:

    READ IT
    USE IT
    CROSS-CHECK IT

If valid Graphify output does NOT exist:

    DO NOT SKIP GRAPHIFY.

Use the project's existing Graphify workflow/configuration if
available.

Generate/create the required Graphify analysis/output in an isolated
research/generated location.

Do NOT modify production source code.

Do NOT overwrite existing Graphify output.

The Graphify output becomes an input to R&D.

Required analysis chain:

    Graphify
       ↓
    Existing .agents research
       ↓
    Prior current-system/source-of-truth documents
       ↓
    Actual source-code verification
       ↓
    Cross-repository analysis

--------------------------------------------------
# MULTI-AGENT / SUB-AGENT STRATEGY
--------------------------------------------------

Use multiple specialized sub-agents.

Do NOT make one agent independently rediscover the entire system.

Use the following execution model.

--------------------------------------------------
# SHARED CONTEXT FILE — CREATE BEFORE DETAILED AGENTS
--------------------------------------------------

The coordination layer must create:

    .agents/aquifier-shared-context.md

BEFORE Agents 2–15 begin detailed analysis.

This file is a NEW R&D artifact.

It may be created and updated during this task.

It must NOT overwrite any existing .agents source-of-truth file.

The initial shared-context file MUST contain:

    1. Aquifier feature requirement
    2. No-verse-mapping requirement
    3. No-verse-mapping ≠ no-identity rule
    4. Four repositories being analyzed
    5. Existing documentation discovered so far
    6. Graphify status
    7. Current unresolved MT-route discrepancy
    8. Known analysis constraints
    9. Execution-wave rules
    10. Evidence/confidence rules

IMPORTANT:

The "no verse mapping ≠ no identity" rule is NOT attributed to
Agent 7.

It is already a direct requirement in this task's framing.

Agent 7 later CONFIRMS or REFINES this rule using repository
evidence.

Agent 7 must update the shared-context file if its investigation
changes or strengthens the architectural conclusion.

Later agents MUST re-read the latest shared-context file before
starting their work.

--------------------------------------------------
# EXECUTION WAVES
--------------------------------------------------

WAVE 0 — COORDINATION / BOOTSTRAP

Perform:

    repository discovery bootstrap
    Graphify discovery/generation
    existing .agents discovery
    prior-document discovery
    creation of aquifier-shared-context.md

No detailed per-repository architecture analysis yet.

--------------------------------------------------
WAVE 1 — PARALLEL
--------------------------------------------------

Run:

    Agent 2 — autographa-app
    Agent 3 — autographa-dashboard
    Agent 4 — IndicTrans2
    Agent 5 — autographa-desktop

These agents may run in parallel because their primary repository
analysis is independent.

Each agent MUST:

    read aquifier-shared-context.md
    read relevant existing documentation
    inspect actual current source
    produce a complete artifact
    identify evidence
    identify unknowns
    identify proposed conclusions separately

--------------------------------------------------
WAVE 2 — CROSS-REPOSITORY ANALYSIS
--------------------------------------------------

Run:

    Agent 6 — Current Resource Architecture
    Agent 7 — No-Mapping Architecture Review
    Agent 8 — Translation Flow Analysis
    Agent 10 — State Management Analysis
    Agent 11 — API Contract Analysis
    Agent 12 — Data/Persistence Analysis
    Agent 13 — Security/Authorization Analysis

These agents depend on the completed Wave 1 repository findings.

Each must consume the relevant Wave 1 artifacts.

Do NOT allow them to rely on memory of another agent's work.

--------------------------------------------------
WAVE 3 — DEPENDENT ANALYSIS
--------------------------------------------------

Run:

    Agent 9 — Translate All Analysis

Agent 9 depends on:

    Agent 8
    Agent 10

--------------------------------------------------
WAVE 4 — FINAL DOMAIN ANALYSIS
--------------------------------------------------

Run:

    Agent 14 — Testing Strategy
    Agent 15 — Risk Analysis

They must consume ALL relevant previous findings.

--------------------------------------------------
WAVE 5 — FINAL CROSS-REPOSITORY ARCHITECT
--------------------------------------------------

Run the final synthesis agent only after all required prior artifacts
exist and have been validated.

The final architect must:

    reconcile findings
    resolve conflicts
    distinguish current vs proposed architecture
    create the final requirement document
    determine V1 minimum scope
    determine whether implementation can safely begin

--------------------------------------------------
# WAVE GATE / ARTIFACT VALIDATION
--------------------------------------------------

A wave may NOT be considered complete merely because an agent says
it is complete.

### REQUIRED ARTIFACTS BY WAVE

For mechanical wave validation, the required artifacts are:

WAVE 0:
    .agents/aquifier-shared-context.md

WAVE 1:
    Agent 2 → app-analysis artifact
    Agent 3 → dashboard-analysis artifact
    Agent 4 → indictrans2-analysis artifact
    Agent 5 → desktop-analysis artifact

WAVE 2:
    Agent 6  → resource-architecture artifact
    Agent 7  → no-mapping-review artifact
    Agent 8  → translation-flow artifact
    Agent 10 → state-management artifact
    Agent 11 → api-contract artifact
    Agent 12 → data-persistence artifact
    Agent 13 → security artifact

WAVE 3:
    Agent 9 → translate-all-analysis artifact

WAVE 4:
    Agent 14 → testing-strategy artifact
    Agent 15 → risk-analysis artifact

WAVE 5:
    Final Cross-Repository Architect →
    .agents/aquifier-resource-requirements-rnd.md

A downstream wave MUST NOT begin until every required artifact
for its prerequisite wave exists, is non-empty, and passes the
artifact validation rules below.


For every agent, require a research artifact containing:

    Agent
    Repository/scope
    Branch
    Commit
    Files inspected
    Existing documents consulted
    Findings
    Evidence
    Unknowns
    Risks
    Recommendations
    Confidence

Before the next wave starts:

    verify each required artifact exists
    verify it is non-empty
    verify it contains the required sections
    verify it does not contain obvious truncation
    verify it identifies its repository/commit where relevant

If an artifact is missing or incomplete:

    DO NOT silently continue.

Mark the dependency as:

    BLOCKED

and either repair the research artifact or document the limitation.

--------------------------------------------------
# SAFE READ-ONLY INVESTIGATION BOUNDARY
--------------------------------------------------

This is an R&D task.

All repository investigation must be read-only.

Allowed:

    source inspection
    configuration inspection
    route discovery
    schema inspection
    test inspection
    static dependency analysis
    Graphify generation
    existing log inspection
    local read-only analysis

Do NOT:

    mutate production data
    modify production databases
    send real translation requests
    expose credentials
    expose JWTs
    expose bearer tokens
    expose API keys
    expose environment secrets
    make destructive API calls
    modify running services

For the MT route investigation:

    POST /api/v2/mt/translate

prefer static inspection of:

    route registration
    middleware
    controllers
    services
    API clients
    tests
    configuration
    logs

If live reproduction is genuinely necessary:

    document the required reproduction steps

but do NOT execute them if they could touch production data,
real credentials, or an uncertain environment.

Never print secrets discovered during investigation.

--------------------------------------------------
# AGENT FAILURE RULE
--------------------------------------------------

If any sub-agent cannot complete its assigned analysis:

    DO NOT fabricate findings.

Record:

    agent
    failed scope
    reason
    missing evidence
    affected downstream decisions

Downstream agents must treat missing findings as:

    UNKNOWN

not as proof that the feature is unsupported.

--------------------------------------------------
# CONFLICT RESOLUTION
--------------------------------------------------

When findings disagree, use this hierarchy:

    1. Actual current source code
    2. Current branch/commit evidence
    3. Verified existing .agents documentation
    4. Verified prior Source-of-Truth/current-system documents
    5. Graphify evidence
    6. Agent inference

Do NOT average conflicting findings.

Do NOT silently choose one.

Document:

    conflicting claim
    source A
    source B
    branch/commit
    evidence
    resolution
    confidence

If the conflict cannot be resolved:

    mark it UNKNOWN

and identify the human decision required before implementation.

--------------------------------------------------
# REASONING / EVIDENCE FORMAT
--------------------------------------------------

Do not expose private chain-of-thought.

For each important conclusion provide:

    Finding:
    Evidence:
    Reasoning Summary:
    Decision:
    Confidence:
    Unknowns:

Confidence:

    HIGH
    MEDIUM
    LOW

Never turn an inference into a verified fact.

--------------------------------------------------
# AGENT 1 / BOOTSTRAP — REPOSITORY DISCOVERY
--------------------------------------------------

The bootstrap/discovery phase MUST determine:

    exact repository paths
    current branch
    current commit
    working-tree status
    relevant .agents documents
    Graphify status
    prior architecture documents
    AUTOGRAPHA_CURRENT_SYSTEM_ARCHITECTURE.md location
    relevant MT/resource code
    relevant tests

Search:

    repository roots
    .agents/
    common project/workspace root

Do NOT modify dirty work.

Record repository dirt.

Never overwrite user changes.

--------------------------------------------------
# AGENT 2 — AUTOGRAPHA-APP ANALYSIS
--------------------------------------------------

Analyze autographa-app deeply.

Find:

    BT Resource architecture
    Resource panel
    current resource types
    resource loading
    object/resource data structures
    card creation
    card identity
    translation-card identity
    translation-store
    Zustand/state management
    SQLite persistence
    MT session store
    MT orchestrator
    single translation
    Translate All
    MT API client
    response parsing
    apply logic
    content synchronization
    TipTap/editor lifecycle
    contentEpoch
    content-list
    active-content-editor
    existing verse assumptions
    existing mapping assumptions

Determine:

    Can Aquifier use the existing translation-card infrastructure?

If YES:

    explain exactly how.

If NO:

    identify the exact architectural limitation.

Identify the minimum change surface.

Do not implement.

--------------------------------------------------
# AGENT 3 — AUTOGRAPHA-DASHBOARD ANALYSIS
--------------------------------------------------

Analyze autographa-dashboard deeply.

Find:

    current API architecture
    auth middleware
    JWT validation
    roles
    permissions
    MT routes
    route registration
    translation schemas
    request DTOs
    response DTOs
    service layer
    database layer
    PostgreSQL models
    text translation APIs
    BT resource APIs
    project APIs
    MTT permissions
    /api/v2/mt/translate
    middleware chain
    controller/service path
    IndicTrans2 integration

Determine:

    What Dashboard changes would be required for Aquifier?

Also determine whether:

    existing endpoint can be reused
    endpoint can be generalized
    new endpoint is required

Do not implement.

--------------------------------------------------
# AGENT 4 — INDICTRANS2 ANALYSIS
--------------------------------------------------

Analyze IndicTrans2.

Find:

    worker_server.py
    POST /translate
    request JSON schema
    response JSON schema
    authentication
    bearer key
    language validation
    batching
    text limits
    error handling
    GPU/device handling
    model loading
    concurrency
    timeout expectations
    tests

Critical question:

Can IndicTrans2 accept Aquifier resource content using the existing
translation contract?

If yes:

    explain exactly how.

If no:

    identify the required transformation.

Investigate possible structures such as:

    {
        "id": "...",
        "text": "..."
    }

or:

    {
        "items": [...]
    }

or another existing/proposed structure.

Do NOT choose a schema merely because it looks convenient.

Base the recommendation on the actual worker implementation.

--------------------------------------------------
# AGENT 5 — AUTOGRAPHA-DESKTOP ANALYSIS
--------------------------------------------------

Analyze autographa-desktop.

Determine:

    how it hosts the App
    renderer architecture
    IPC
    SQLite
    filesystem/resource access
    resource flow
    MT flow
    desktop-to-app communication
    whether Aquifier requires Desktop changes

Do not assume Desktop needs modification.

Prove whether it does.

If no change is required:

    explicitly state why.

--------------------------------------------------
# AGENT 6 — CURRENT RESOURCE ARCHITECTURE
--------------------------------------------------

Analyze the current BT Resource.

Trace:

    Resource
       ↓
    Resource content
       ↓
    Resource object/item
       ↓
    Left-side display
       ↓
    User selection
       ↓
    Translation action
       ↓
    Translation card
       ↓
    Translation state
       ↓
    Persistence

Identify the actual identity mechanism.

Investigate:

    verseId
    contentId
    resourceId
    objectId
    itemId
    UUID
    composite keys
    other identity mechanisms

Determine:

    Can Aquifier use its own identity?

Expected conceptual architecture:

    Aquifier Resource
          ↓
    Aquifier Item ID
          ↓
    Translation Request
          ↓
    Translation Result
          ↓
    SAME Aquifier Item ID
          ↓
    Corresponding Translation Card

There must be no unnecessary Bible verse mapping.

--------------------------------------------------
# AGENT 7 — "NO MAPPING" ARCHITECTURE REVIEW
--------------------------------------------------

This agent CONFIRMS/REFINES the requirement.

Do NOT attribute the requirement to Agent 7's original framing.

The requirement already exists in the task:

    NO VERSE MAPPING
    ≠
    NO IDENTITY

Explicitly separate:

    1. Bible verse mapping
    2. Translation-card identity
    3. Resource-item identity
    4. Database identity
    5. UI selection identity
    6. API request correlation

The requirement is:

    NO Bible/verse mapping.

But the system still needs deterministic identity to know:

    "This translation result belongs to THIS Aquifier card."

Determine the cleanest identity mechanism supported by the actual
architecture.

Do not accidentally interpret "no mapping" as:

    "no IDs."

After analysis:

    update aquifier-shared-context.md

with the verified/refined identity conclusion.

IMPORTANT WAVE-ORDER RULE:

Agent 7 runs in the same wave as Agents 6, 8, 10, 11, 12, and 13.

Agents in this wave MUST treat the initial
aquifier-shared-context.md as authoritative for the baseline
requirement:

    NO VERSE MAPPING ≠ NO IDENTITY

Agent 7's refinement is an additional evidence-based confirmation,
not a prerequisite for the other Wave 2 agents.

Agent 7 MUST NOT silently change an existing requirement in a way
that contradicts the shared context during the active wave.

If Agent 7 discovers evidence that materially contradicts the
baseline architecture:

    STOP
    record the conflict
    identify the conflicting evidence
    mark the affected conclusion UNKNOWN/CONFLICT
    escalate it to the Final Cross-Repository Architect

Do not silently rewrite the shared context and allow other
same-wave agents to consume a changed requirement inconsistently.


--------------------------------------------------
# AGENT 8 — TRANSLATION FLOW ANALYSIS
--------------------------------------------------

Trace the current single-item translation flow.

Document the actual flow:

    User clicks Translate
          ↓
    selected resource/item
          ↓
    text extraction
          ↓
    API client
          ↓
    Dashboard
          ↓
    IndicTrans2
          ↓
    response
          ↓
    App
          ↓
    translation card
          ↓
    persistence

Then design the proposed Aquifier equivalent:

    Aquifier Item
          ↓
    JSON payload
          ↓
    MT endpoint
          ↓
    translation engine
          ↓
    translated JSON
          ↓
    correlation by Aquifier Item ID
          ↓
    corresponding translation card only

Clearly identify:

    REUSED
    NEW
    CHANGED
    NOT NEEDED

Do not implement.

--------------------------------------------------
# AGENT 9 — TRANSLATE ALL ANALYSIS
--------------------------------------------------

Analyze existing Translate All.

Determine whether Aquifier V1 requires:

    Translate single item
    Translate All
    Retry
    Cancel
    Progress
    Failure state
    Partial completion
    Sequential requests
    Batching

Do not assume the existing verse-based Translate All can be reused.

Determine the minimum architecture required.

Classify each capability:

    REQUIRED
    OPTIONAL
    FUTURE
    UNKNOWN

--------------------------------------------------
# AGENT 10 — STATE MANAGEMENT ANALYSIS
--------------------------------------------------

Investigate whether current stores assume:

    verse IDs
    chapter IDs
    Bible resource IDs
    contentEpoch
    contentItem IDs
    translation block IDs

Determine exactly what state changes are needed to support:

    Aquifier Resource
    Aquifier Item
    Translation Card

Also identify:

    render loops
    remount loops
    stale-state issues
    duplicate requests
    race conditions
    stale translation application

Especially inspect:

    httpBusy
    tryBeginInFlight()
    TipTap
    contentEpoch

Do not fix them.

Determine whether Aquifier will:

    reuse
    trigger
    worsen
    bypass

those issues.

--------------------------------------------------
# AGENT 11 — API CONTRACT ANALYSIS
--------------------------------------------------

Produce the CURRENT API contract.

Document:

    App → Dashboard request
    Dashboard → IndicTrans2 request
    IndicTrans2 response
    App apply format

Then propose:

    Aquifier request contract
    Aquifier response contract

Clearly label every new proposal:

    PROPOSED

Never claim a proposed contract is already implemented.

Determine whether:

    /v2/mt/translate

can safely support Aquifier.

Investigate:

    Can it accept arbitrary resource items?
    Does it require projectId?
    Does it require Bible verse context?
    Does Dashboard authorization assume MTT project ownership?
    Does IndicTrans2 care about resource type?
    Can the endpoint be generalized?
    Is a new endpoint required?

Recommend the minimum safe option.

--------------------------------------------------
# AGENT 12 — DATA / PERSISTENCE ANALYSIS
--------------------------------------------------

Determine where Aquifier translations should live.

Analyze:

    App SQLite
    Zustand
    Dashboard PostgreSQL
    Sync APIs
    Resource storage
    Translation storage

Answer:

    Should Aquifier translations be persisted locally?
    Should they sync to Dashboard?
    Does Dashboard already contain a compatible entity?
    Is a new DB table required?
    Is persistence required for V1?
    Can V1 be local-only?

Do not invent requirements.

Classify:

    REQUIRED
    OPTIONAL
    FUTURE
    UNKNOWN

--------------------------------------------------
# AGENT 13 — SECURITY / AUTHORIZATION
--------------------------------------------------

Analyze:

    App JWT
    Dashboard JWT verification
    roles
    MTT role
    projectId
    worker bearer key
    Dashboard → IndicTrans2 authentication
    route middleware
    authorization middleware

Investigate the historical/current MT issue:

    POST /api/v2/mt/translate

Possible states include:

    403 Forbidden
    404 / route missing
    another HTTP result
    route exists but is inaccessible
    route exists under a different path
    route exists only on another branch/commit
    another architectural discrepancy

IMPORTANT:

Do NOT assume 403 is confirmed.

Do NOT assume the route is missing.

Determine the actual current behavior from the current checkout.

Reconcile against:

    AUTOGRAPHA_CURRENT_SYSTEM_ARCHITECTURE.md

and any other prior documentation.

The report MUST identify:

    branch
    commit
    route registration
    middleware
    authorization
    controller/service
    historical finding
    current finding
    explanation for discrepancy

Do NOT fix the problem.

Only report:

    where
    why
    affected role
    affected route
    affected architecture
    whether Aquifier would hit the same issue

--------------------------------------------------
# AGENT 14 — TESTING STRATEGY
--------------------------------------------------

Analyze existing tests across all four repositories.

Determine:

    unit test framework
    integration tests
    API tests
    worker tests
    UI tests
    mocks
    fixtures
    test utilities
    commands
    coverage
    CI execution

Define the FULL Aquifier test strategy.

UNIT TESTS:

    resource parsing
    JSON serialization
    JSON deserialization
    item identity
    translation payload creation
    response correlation
    card update
    no verse mapping
    error handling
    empty resource
    malformed resource
    duplicate IDs
    long content
    multiple items

INTEGRATION TESTS:

    App → Dashboard
    Dashboard → IndicTrans2
    authentication
    authorization
    response propagation

UI/E2E TESTS:

    Aquifier appears
    select item
    Translate
    translation appears in correct card
    another card remains unchanged
    no verse mapping
    Translate All if supported
    resource switching
    resource modification during translation
    retry
    failure state

REGRESSION:

    existing BT
    existing TT
    Manual
    AI
    Translate All
    Resource
    Sync
    Desktop

Do not implement tests.

--------------------------------------------------
# AGENT 15 — ADVERSARIAL RISK ANALYSIS
--------------------------------------------------

Perform an adversarial architecture review.

Find risks involving:

    identity collisions
    verse coupling
    incorrect card updates
    stale state
    race conditions
    duplicate requests
    auth failures
    API contract mismatch
    worker failures
    long text
    unsupported language
    persistence
    synchronization
    TipTap remounting
    SQLite
    Dashboard schema
    Desktop
    backwards compatibility
    existing BT Resource behavior

Rank:

    CRITICAL
    HIGH
    MEDIUM
    LOW

For each risk provide:

    Risk
    Cause
    Affected repository
    Detection
    Mitigation
    V1 blocker: YES/NO
    Confidence

--------------------------------------------------
# FINAL CROSS-REPOSITORY ARCHITECT
--------------------------------------------------

After all agents complete, synthesize one verified cross-repository
architecture.

It MUST answer:

    Where does Aquifier originate?
    Where is it stored?
    How is it represented?
    How is an item identified?
    How does translation start?
    What JSON is sent?
    Which endpoint receives it?
    Which service calls IndicTrans2?
    What does IndicTrans2 return?
    How is the result correlated?
    How is the right-side card updated?
    Where is the result persisted?
    Does Dashboard store it?
    Does Desktop participate?
    What happens on failure?
    What happens on retry?
    What happens on Translate All?
    What happens if the user switches resources?
    What happens if the resource changes during translation?

For every answer identify:

    current
    proposed
    unknown

--------------------------------------------------
# REQUIRED DIAGRAMS
--------------------------------------------------

Generate Mermaid diagrams.

### Diagram 1 — CURRENT ARCHITECTURE

Show:

    App
    Dashboard
    IndicTrans2
    Desktop
    SQLite
    PostgreSQL
    Current MT path
    Current MT gap/discrepancy

Do not falsely show an endpoint as existing if it is not verified.

### Diagram 2 — CURRENT BT RESOURCE FLOW

Show:

    Resource
       ↓
    Item
       ↓
    Selection
       ↓
    Translation
       ↓
    Card
       ↓
    Persistence

### Diagram 3 — PROPOSED AQUIFIER FLOW

Show:

    Aquifier Resource
          ↓
    Aquifier Item
          ↓
    JSON
          ↓
    Dashboard MT
          ↓
    IndicTrans2
          ↓
    Translated JSON
          ↓
    Aquifier Item ID
          ↓
    Corresponding Translation Card

Explicitly show:

    NO VERSE MAPPING

### Diagram 4 — IDENTITY / CORRELATION

Show:

    AquifierItemId
          ↓
    TranslationRequest
          ↓
    TranslationResponse
          ↓
    AquifierItemId
          ↓
    TranslationCard

### Diagram 5 — PERSISTENCE

Show:

    UI
    Zustand
    SQLite
    Sync
    Dashboard
    PostgreSQL

Only include verified paths.

Mark proposed paths explicitly as:

    PROPOSED

--------------------------------------------------
# REQUIREMENT CLASSIFICATION
--------------------------------------------------

Every requirement must be classified:

    REQUIRED
    OPTIONAL
    FUTURE
    UNKNOWN

Every implementation area must be classified:

    EXISTING
    REUSE
    CHANGE
    NEW
    REMOVE
    NOT REQUIRED

Use:

| Requirement | Classification | Status | Repository |
|-------------|----------------|--------|------------|

Example:

| Aquifier resource UI | REQUIRED | NEW | App |
| Verse mapping | NOT REQUIRED | NOT REQUIRED | App |
| Translation-card identity | REQUIRED | REUSE/CHANGE | App |
| MT endpoint | REQUIRED | REUSE/CHANGE/NEW | Dashboard |
| Worker JSON contract | REQUIRED | VERIFY/CHANGE | IndicTrans2 |
| Desktop IPC | UNKNOWN | VERIFY | Desktop |

--------------------------------------------------
# CHANGE-SURFACE MATRIX
--------------------------------------------------

Create:

| Repository | Exact File/Area | Current Responsibility | Required Change | Risk | Priority |
|------------|-----------------|------------------------|-----------------|------|----------|

DO NOT INVENT FILE NAMES.

Only include exact files discovered during analysis.

--------------------------------------------------
# FILE-LEVEL R&D
--------------------------------------------------

For every proposed change identify:

    repository
    exact file
    exact symbol/component/function where available
    current behavior
    evidence
    why it matters
    proposed responsibility
    dependencies
    risk
    test requirement
    confidence

Do not edit the file.

--------------------------------------------------
# API CONTRACT TABLE
--------------------------------------------------

Produce a table:

| Layer | Current Contract | Aquifier Requirement | Change |
|------|------------------|----------------------|--------|

Include:

    App → Dashboard
    Dashboard → IndicTrans2
    IndicTrans2 → Dashboard
    Dashboard → App

Clearly distinguish:

    CURRENT
    PROPOSED

--------------------------------------------------
# DATA MODEL TABLE
--------------------------------------------------

Produce:

| Entity | Current Representation | Aquifier Requirement | Reuse/New/Change |
|--------|------------------------|----------------------|------------------|

Include:

    Resource
    Aquifier Resource
    Aquifier Item
    Translation Request
    Translation Response
    Translation Card
    Persistence
    Sync

--------------------------------------------------
# MINIMUM ARCHITECTURE
--------------------------------------------------

Determine the MINIMUM implementation architecture.

Do NOT over-engineer.

Answer:

    What is the smallest safe set of changes required to support
    Aquifier Resource translation?

Separate:

    V1 REQUIRED
    V1 OPTIONAL
    FUTURE

Do not include improvements merely because they are technically
interesting.

--------------------------------------------------
# V1 SCOPE
--------------------------------------------------

Define the smallest V1 that satisfies:

    Aquifier Resource exists
    Aquifier content can be selected
    relevant content can be sent to translation engine
    translation is represented as JSON where required
    translation returns successfully
    result is correlated to the correct Aquifier item
    only the correct translation card is updated
    no Bible verse mapping is required
    existing BT behavior is not broken

Everything else must be justified before inclusion.

--------------------------------------------------
# NON-REQUIREMENTS
--------------------------------------------------

Explicitly identify features that are NOT required for V1.

At minimum investigate:

    Bible verse mapping
    Scripture reference mapping
    forced verse IDs
    unnecessary project coupling
    unnecessary Desktop changes
    unnecessary Dashboard DB changes
    unnecessary batching
    unnecessary Translate All support

Do not mark something "not required" unless the analysis supports it.

--------------------------------------------------
# KNOWN BUGS / EXISTING ISSUES
--------------------------------------------------

Create a separate table:

| Issue | Current Evidence | Aquifier Impact | V1 Blocker | Fix Now? |
|------|------------------|-----------------|------------|----------|

For this R&D task:

    Fix Now? = NO

unless the issue is merely documented and not modified.

Include:

    MT route discrepancy
    httpBusy / tryBeginInFlight()
    TipTap/contentEpoch
    other verified relevant issues

--------------------------------------------------
# SECURITY
--------------------------------------------------

Do not expose:

    JWTs
    bearer tokens
    API keys
    environment secrets
    passwords

If credentials are discovered:

    identify their existence
    redact them
    never copy their value into reports

--------------------------------------------------
# DO NOT IMPLEMENT
--------------------------------------------------

This task MUST NOT:

    edit source code
    modify production files
    change API implementation
    modify API routes
    modify schemas
    modify database
    modify worker
    modify App
    modify Dashboard
    modify Desktop
    install packages
    refactor
    fix bugs
    create commits
    create PRs
    overwrite existing .agents documents

Allowed NEW research artifacts:

    .agents/aquifier-shared-context.md
    .agents/aquifier-resource-requirements-rnd.md

and isolated temporary research artifacts required by the analysis.

Existing source-of-truth documents are READ-ONLY.

--------------------------------------------------
# OUTPUT ARTIFACTS
--------------------------------------------------

The research process must produce:

    .agents/aquifier-shared-context.md

and finally:

    .agents/aquifier-resource-requirements-rnd.md

Do not overwrite either if it already exists.

If either exists:

    create a new uniquely named research artifact
    OR
    explicitly determine whether it is safe to update

Never destroy existing research.

--------------------------------------------------
# FINAL R&D DOCUMENT
--------------------------------------------------

Create:

    .agents/aquifier-resource-requirements-rnd.md

It MUST contain:

# 1. Executive Summary

# 2. Repositories Analyzed

# 3. Repository Branches and Commits

# 4. Graphify Findings

# 5. Existing .agents Findings

# 6. AUTOGRAPHA_CURRENT_SYSTEM_ARCHITECTURE.md Findings

# 7. Current System Architecture

# 8. Current BT Resource Architecture

# 9. Current Translation Flow

# 10. Current API Flow

# 11. Current Authentication Flow

# 12. Current Persistence Flow

# 13. Current MT Route Status

Explicitly reconcile:

    403
    404/missing route
    other behavior

# 14. Current Known Problems / Risks

# 15. Aquifier Functional Requirements

# 16. Aquifier Non-Requirements

# 17. Aquifier Data Model

# 18. Aquifier Identity Model

# 19. No-Verse-Mapping Architecture

# 20. Aquifier Translation JSON Contract

# 21. Aquifier End-to-End Flow

# 22. Required Repository Changes

# 23. File-Level Change Surface

# 24. API Changes

# 25. Database/Persistence Changes

# 26. Desktop Impact

# 27. Security/Auth Impact

# 28. State Management Impact

# 29. Translate All Strategy

# 30. Unit Test Strategy

# 31. Integration Test Strategy

# 32. UI/E2E Test Strategy

# 33. Regression Test Strategy

# 34. Risk Analysis

# 35. Open Questions

# 36. Decisions Required Before Implementation

# 37. V1 Minimum Scope

# 38. Explicitly Out of Scope

# 39. Mermaid Architecture Diagrams

# 40. Implementation Readiness Assessment

--------------------------------------------------
# FINAL DECISION TABLE
--------------------------------------------------

End the document with:

| Decision | Recommendation | Evidence | Confidence |
|----------|----------------|----------|------------|

The table MUST include:

    Aquifier identity
    verse mapping
    translation endpoint
    JSON request
    JSON response
    Dashboard responsibility
    IndicTrans2 responsibility
    App responsibility
    Desktop responsibility
    persistence
    Translate All
    error handling
    authentication
    testing
    V1 scope

--------------------------------------------------
# IMPLEMENTATION READINESS GATE
--------------------------------------------------

Before declaring the architecture ready, verify:

[ ] All four repositories analyzed

[ ] Current branches/commits recorded

[ ] Graphify checked/generated

[ ] Existing .agents documentation reviewed

[ ] AUTOGRAPHA_CURRENT_SYSTEM_ARCHITECTURE.md searched for and
    reviewed if present

[ ] Current code verified against prior documentation

[ ] Current MT route status determined

[ ] Historical 403 vs missing-route discrepancy reconciled

[ ] Aquifier identity mechanism determined

[ ] No Bible verse mapping required

[ ] Translation request contract determined/proposed

[ ] Translation response contract determined/proposed

[ ] Correct-card correlation mechanism determined

[ ] Dashboard impact determined

[ ] IndicTrans2 impact determined

[ ] App impact determined

[ ] Desktop impact determined

[ ] Persistence impact determined

[ ] Security/auth impact determined

[ ] Translate All scope determined

[ ] Unit test strategy defined

[ ] Integration test strategy defined

[ ] UI/E2E test strategy defined

[ ] Regression strategy defined

[ ] Risks identified and ranked

[ ] V1 scope defined

[ ] Open questions documented

[ ] Conflicts resolved or explicitly marked UNKNOWN

[ ] Exact file-level change surface documented

[ ] No invented filenames

[ ] No production source modified

[ ] No existing source-of-truth document overwritten

If any REQUIRED item is missing:

    ARCHITECTURE STATUS = BLOCKED

If all required evidence exists:

    ARCHITECTURE STATUS = READY FOR IMPLEMENTATION

--------------------------------------------------
# FINAL CHAT RESPONSE
--------------------------------------------------

After creating the R&D document:

DO NOT IMPLEMENT ANYTHING.

Return a concise summary containing:

1. Repositories analyzed
2. Branches/commits analyzed
3. Graphify status
4. Existing .agents documents used
5. AUTOGRAPHA_CURRENT_SYSTEM_ARCHITECTURE.md status
6. Current architecture summary
7. Current MT route status
8. 403 vs missing-route reconciliation
9. Current BT Resource flow
10. Proposed Aquifier architecture
11. NO VERSE MAPPING conclusion
12. Aquifier identity mechanism
13. Exact repositories requiring changes
14. Exact major files requiring changes
15. API changes
16. Data/persistence changes
17. Desktop impact
18. Security impact
19. Test strategy
20. Top risks
21. Open questions
22. V1 minimum scope
23. Implementation readiness

The response MUST clearly separate:

    VERIFIED
    PROPOSED
    UNKNOWN

The final line MUST be exactly:

    IMPLEMENTATION STATUS: NOT IMPLEMENTED
