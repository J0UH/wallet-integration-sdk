[← All work](https://github.com/J0UH) · [Open finance and payments](https://github.com/J0UH/open-finance-payments)

# Wallet and integration SDK

A smaller application interface around providers and networks that behave differently underneath.

<img src="assets/hero-v2.webp" alt="Wallet and integration SDK illustrated as a crafted architectural model, with exposed sketch and structural framing" width="100%" />

Product teams want a wallet connection that fits their application. The providers bring different sessions, network lifecycles, permissions, and error states.

This work turns that variation into a more manageable integration contract. Part of it adapts Reown AppKit, with the local work in provider integration, lifecycle handling, and the behaviour exposed to products.

## Hiding the right amount

An application still needs to know when its session changes, when a network is unsuitable, or when an operation needs recovery. Those states cannot disappear just because the wrapper is convenient.

I keep provider-specific behaviour at the edge and make lifecycle changes observable. Typed interfaces and normalised errors help the consuming product handle the states that matter.

The aim is a small, stable contract rather than a wrapper for every upstream option. Application examples and developer guidance complete that work by showing how the integration behaves outside the ideal path.

## Built on

Part of this work adapts [Reown AppKit](https://github.com/reown-com/appkit), retained under its Apache-2.0 licence. The adapter work covers the smaller SDK contract, provider integration, product lifecycle, and operating behaviour built around that foundation.

## What the work covers

- Provider and connector abstraction
- Session and network lifecycle handling
- Typed integration surfaces
- Error normalisation and recovery
- Application examples and developer guidance

<details>
<summary>A closer look at the technical flow</summary>

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

</details>

## Related work

- [Open finance and payments](https://github.com/J0UH/open-finance-payments)
- [Decentralised exchange platform](https://github.com/J0UH/dex-platform)
- [Multi-asset money platform](https://github.com/J0UH/multi-asset-money-platform)

Working on a similar problem? [Tell me what you are building](mailto:ju@jomena.group?subject=Wallet%20and%20integration%20SDK).

*This is a public account of the work. Source code and private operating details are not included in this repository.*
