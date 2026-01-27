---
name: research-extensive
description: Conducts comprehensive, multi-source research using web search and document scraping with built-in verification via secondary subagents. Use when researching complex topics, validating claims, gathering evidence, or needing high-confidence findings. Enforces minimum 10+ sources with automated challenge phase.
---

# Extensive Research Skill

Performs thorough, evidence-based research with extensive reasoning, minimum 10+ source requirement, and secondary subagent verification. Optimized for deep understanding, cross-validation, and comprehensive analysis with built-in adversarial testing.

## Core Principles

1. **Minimum 10+ Sources**: Every research task must utilize at least 10 distinct authoritative sources
2. **Extensive Reasoning**: Show all reasoning steps, trade-offs, contradictions, and confidence levels (token cost irrelevant)
3. **Secondary Verification**: Use subagents to challenge and verify original findings with fresh or updated sources
4. **Multi-Layer Validation**: Cross-check facts across multiple sources, then challenge conclusions independently
5. **Source Diversity**: Include academic papers, official documentation, industry reports, expert analysis, and case studies

## Research Workflow

### Phase 1: Initial Research (Primary Subagent)

**Reconnaissance (Source Gathering)**
- Conduct web searches with 3-5 distinct search queries from different angles
- Identify 15+ promising sources for initial assessment
- Categorize by authority level, recency, potential bias, and complementarity

**Deep Collection (Content Extraction)**
- Read and extract content from 10-12 selected web sources with specific objectives
- Extract key data points, quotes, statistics, arguments
- Document source metadata (author, date, domain, authority level)

**Comprehensive Analysis**
- Synthesize findings across all sources
- Map consensus areas and contradictions
- Assess confidence levels (high/medium/low) for each claim
- Note coverage gaps that might indicate bias

### Phase 2: Challenge & Verification (Secondary Subagent)

**Critical Review of Original Findings**
The secondary subagent receives the original research output and must:
- Question the methodology: Were search terms comprehensive enough? Did they bias results?
- Test completeness: Are there opposing viewpoints not adequately explored?
- Verify recency: Are there newer sources that contradict or clarify original findings?
- Search independently with different queries targeting:
   - Opposing viewpoints and alternative perspectives
   - Recently published contradictory evidence
   - Domain-specific expert sources missed in round 1
   - Case studies that validate or refute claims
 - Minimum 8-10 new sources (different from Phase 1)
 - Document which original claims held up under scrutiny
 - Identify weaknesses, overconfidences, or gaps

**Challenge Workflow**
1. Secondary subagent receives: original research, identified claims, confidence levels, source list
2. Explicitly task: "Challenge these findings. Find sources that disagree, contradict, or refine these conclusions."
3. Execute 3-4 targeted web searches with adversarial intent
4. Read and extract content from 8-10 new sources
5. Create "Challenge Report":
   - Findings that held up (with supporting evidence)
   - Findings that weakened (with refuting evidence)
   - New information that changes conclusions
   - Remaining uncertainties
   - Confidence adjustments for original claims

### Phase 3: Synthesis & Final Conclusions (Collaboration)

- Integrate challenge findings into original analysis
- Adjust confidence levels based on verification results
- Create final report with:
  - All 18-22+ source citations across both phases
  - Explicit "Verified," "Refined," and "Questionable" claim categorization
  - Updated reasoning reflecting adversarial testing
  - Remaining gaps and uncertainty areas

## Research Task Template

1. **Define scope**: What is being researched? What specific questions need answers?
2. **Primary research** (Phase 1): Execute 3-5 search queries, read 10-12 sources
3. **Secondary challenge** (Phase 2): Create challenge subagent, execute 3-4 adversarial searches, read 8-10 new sources
4. **Synthesize**: Integrate findings, adjust confidence, document verification results
5. **Document**: Cite all 18-22+ sources, state confidence with justification, highlight remaining uncertainty

## Source Quality Framework

**Priority Tiers**
1. Primary sources (original research, official data, firsthand accounts)
2. Peer-reviewed academic research and established institutions
3. Expert analysis from recognized authorities
4. Recent investigations and analyses
5. Secondary sources and aggregators

**Document for Each Source**
- Author/publisher and their authority/bias
- Publication date and recency
- Relationship to other sources (confirming, contradicting, complementary)
- Specific evidence contribution

## Analysis Requirements

For every major claim:
1. State the claim clearly
2. List supporting sources (with links) from Phase 1
3. Note Challenge Phase verification status
4. Provide confidence assessment pre- and post-verification
5. Document reasoning connecting evidence to conclusion
6. Flag if adversarial sources contradict or refine the claim

## Minimum Requirements Checklist

**Phase 1 (Initial Research)**
- [ ] Conducted web searches with 3-5 distinct queries from different angles
- [ ] Identified and screened 15+ potential sources
- [ ] Extracted detailed content from 10+ sources
- [ ] Documented source metadata (author, date, authority, bias)
- [ ] Identified contradictions and consensus areas
- [ ] Created confidence assessments for all major claims
- [ ] Showed comprehensive reasoning for conclusions

**Phase 2 (Challenge Verification)**
- [ ] Secondary subagent explicitly tasked to challenge findings
- [ ] Conducted 3-4 adversarial web searches targeting opposing views
- [ ] Read and extracted content from 8-10 new sources (distinct from Phase 1)
- [ ] Documented which claims held up under scrutiny
- [ ] Identified weaknesses, overconfidences, or new evidence
- [ ] Created explicit Challenge Report with verification status
- [ ] Adjusted confidence levels based on verification results

**Phase 3 (Synthesis)**
- [ ] Integrated challenge findings into original analysis
- [ ] Categorized claims as: Verified, Refined, Questionable
- [ ] Cited all 18-22+ sources from both phases
- [ ] Provided confidence levels pre- and post-verification
- [ ] Highlighted remaining gaps and uncertainties
- [ ] Explained why sources disagreed where applicable

## Anti-Patterns to Avoid

- Single research pass without verification
- Ignoring contradictory findings or challenging evidence
- Failing to cite sources or verify via second pass
- Assuming currency without checking recent sources
- Treating all sources as equally authoritative
- Skipping cross-validation of key claims
- Allowing confirmation bias in source selection
- Not documenting what changed during verification phase

## Extended Analysis with Verification

### Verification-Driven Reasoning Pattern
1. **Initial Thesis**: State core thesis and supporting evidence (Phase 1)
2. **Evidence Mapping**: Show how sources support thesis
3. **Challenge Phase**: Independent subagent identifies contradictions, gaps, alternatives
4. **Refined Thesis**: Update thesis based on verification results
5. **Contradiction Resolution**: Explain why sources differ; which held up
6. **Confidence Evolution**: Show how confidence changed post-verification
7. **Limitation Statement**: Document what remains uncertain despite two phases

## Capabilities Required

- **Web Search**: Multiple queries with different intent (initial + adversarial)
- **Web Content Extraction**: Deep content extraction from URLs with specific objectives
- **Optional**: Shell commands for specialized content retrieval (curl/wget)
- **Optional**: Code/documentation search for technical topics

## Subagent Communication Pattern

**Primary Subagent Output to Secondary:**
```
# Research Findings: [Topic]

## Initial Findings (Phase 1)
[Claims with sources, confidence, reasoning]

## Sources Used (Phase 1)
1-10+: [URLs, titles, authority levels]

## Your Task (Secondary Subagent)
Challenge these findings:
- Search for opposing viewpoints
- Look for recent contradictory evidence
- Find domain expert sources we may have missed
- Identify methodological gaps in our search
- Provide minimum 8-10 new sources

Generate a Challenge Report addressing each finding.
```

**Secondary Subagent Deliverable:**
```
# Challenge Report: [Topic]

## Verification Status by Claim
- Claim 1: VERIFIED (supporting evidence)
- Claim 2: REFINED (new evidence changes scope)
- Claim 3: WEAKENED (contradictory sources found)

## New Sources (Phase 2): [8-10 URLs]

## Confidence Adjustments
- Original confidence: X → Updated: Y (reason)

## Remaining Gaps
[What two phases together could not resolve]
```

## Expected Final Output Format

```
# Research: [Topic]

## Summary
[1-2 sentence overview of verified findings]

## Verified Findings (from both phases)

### Finding 1: [Claim]
**Phase 1 Sources**: [Source A], [Source B]
**Phase 2 Verification**: VERIFIED / REFINED / WEAKENED
**Challenge Sources**: [Source C], [Source D]
**Confidence**: High (90%+) [with justification]
**Reasoning**: [explanation showing verification]

### Finding 2: [Claim]
**Phase 1 Sources**: [...]
**Phase 2 Status**: REFINED - Evidence from [Source] shows [new insight]
**Confidence**: Medium (70%) [with justification]

## Source Inventory
| # | URL | Title | Authority | Phase | Status |
|---|-----|-------|-----------|-------|--------|
| 1 | [...] | [...] | High | Phase 1 | Verified |
| 2 | [...] | [...] | High | Phase 2 | Challenge |

## Verification Summary
- Total Sources: 18+ (Phase 1: 10+, Phase 2: 8+)
- Claims Verified: X
- Claims Refined: Y
- Claims Weakened: Z

## Remaining Gaps & Limitations
[What could not be conclusively determined]

## Confidence Assessment
[Overall confidence level with pre/post-verification comparison]
```

---

**Critical**: This skill requires two distinct research passes (primary and secondary subagent). Do not shortcut to one pass. The verification phase catches overconfidence, discovers opposing evidence, and ensures robust findings. Show your work through both phases, and document how verification changed your conclusions.
