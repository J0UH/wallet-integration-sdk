[← All systems](https://github.com/J0UH) · [Open finance and payments](https://github.com/J0UH/open-finance-payments)

<p align="center">
  <img src="assets/hero.webp" alt="One shared connector branches into four differently keyed mechanical adapter ports" width="100%" />
</p>

# Wallet and integration SDK

Wallet integrations sit at an awkward boundary. Product teams want one clean interface, but the underlying providers, networks, permissions, sessions, and error modes refuse to behave uniformly. This work turned that variation into a smaller contract that applications could rely on.

## The engineering problem

An SDK has to hide accidental complexity without hiding the states developers must handle. Compatibility, clear errors, predictable lifecycle events, and safe defaults matter more than a clever abstraction.


## Foundation and adaptation

Part of this work adapts [Reown AppKit](https://github.com/reown-com/appkit), retained under its Apache-2.0 licence. The adapter work covers the smaller SDK contract, provider integration, product lifecycle, and operating behaviour built around that foundation.

## What the system covers

- Provider and connector abstraction
- Session and network lifecycle handling
- Typed integration surfaces
- Error normalisation and recovery
- Application examples and developer guidance

## System shape

```mermaid
flowchart TD
accTitle: Wallet and integration SDK
accDescr: The application depends on one SDK contract. Supported providers pass through adapters into an observable session, while unsupported or revoked states return explicitly to the application.
    app["Application"] --> sdk["SDK contract"]
    sdk --> support{"Provider supported?"}
    support -->|Yes| adapter["Provider adapter"]
    support -->|No| reject["Explicit unsupported state"]
    adapter --> session["Wallet session"]
    session --> product["Observable product state"]
    session -->|Disconnect or revoke| app
```

## Build notes

- Keep provider-specific behaviour at the edge.
- Make lifecycle changes observable instead of surprising the application.
- Prefer a small stable contract over a wrapper for every upstream option.

<sub>Public overview only. Source code, customer data, credentials, and private operating details are not included.</sub>

## Talk through a similar problem

Working on something similar? [Tell me about it](mailto:ju@jomena.group?subject=Wallet%20and%20integration%20SDK).
