# FactCheck Studio

A live web app built on two GenLayer Intelligent Contracts deployed on StudioNet. Every record the app shows is read directly from the blockchain — a fact or verdict is only stored after independent GenLayer validators fetched the same web pages and reproduced the exact same result under the strict equivalence principle.

**Live app:** https://adryanryan03-create.github.io/factcheck-studio/

## The two contracts

### CrossCheck — two-source claim corroboration
`verify_claim(claim, url_a, url_b)` fetches both sources, judges whether each supports the claim, and stores the pair of judgements on-chain only on exact validator agreement. A claim is *corroborated* only when both independent sources support it.

- Contract: `0x37D56fBd44ef4965d6059d0039393fC3800d50AF`
- Explorer: https://explorer-studio.genlayer.com/address/0x37D56fBd44ef4965d6059d0039393fC3800d50AF
- Source: https://github.com/adryanryan03-create/crosscheck-genlayer

### FactAnchor — consensus-verified web fact snapshots
`anchor_fact(url, question)` extracts a short factual answer from a public page and anchors it on-chain only when validators reproduce the identical extraction. `check_claim(url, claim)` stores a consensus verdict on whether a page supports a specific claim.

- Contract: `0xa5b15C2F47770BD6F10f51BE0bBf945f8149D127`
- Explorer: https://explorer-studio.genlayer.com/address/0xa5b15C2F47770BD6F10f51BE0bBf945f8149D127
- Source: https://github.com/adryanryan03-create/factanchor-genlayer

## How the app works

`index.html` is a dependency-light static page. It uses the official `genlayer-js` client (loaded from a CDN) configured for StudioNet and calls the contracts' read methods (`get_verdict_count` / `get_verdict`, `get_fact_count` / `get_fact`, `get_check_count` / `get_check`) directly from the visitor's browser. There is no backend and no cached or simulated data.

Writes (anchoring a new fact or verifying a new claim) are done in GenLayer Studio with the deployed contracts; the app links there with step-by-step instructions.

## Why it matters

AI agents increasingly act on information pulled from the web, but a normal blockchain cannot check a web page, and a single LLM answer cannot be trusted. FactCheck Studio shows the GenLayer answer to that problem: subjective questions about real web content, settled by validator consensus and stored as citable, re-checkable on-chain records.
