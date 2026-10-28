# Funding

Perpetual futures have no expiry. On the order book (V2), a periodic **funding payment** between longs and shorts keeps the perp price close to the spot price. On pool-based execution (V1 and Degen mode), holding costs, if any, are set by the pool engine and shown in the order panel before opening.

```mermaid
flowchart LR
    subgraph Positive["Perp above spot · rate > 0"]
        L1[Longs] -- pay --> S1[Shorts]
    end
    subgraph Negative["Perp below spot · rate < 0"]
        S2[Shorts] -- pay --> L2[Longs]
    end
```

```
funding payment = notional × funding rate
```

**Example.** A $10,000 ETH long with a +0.01% rate pays $1 at the funding time. A $10,000 short receives $1.

- Funding is exchanged between traders. DYXY receives no part of it.
- Only positions open at the funding time pay or receive.
- The current rate, the interval and a countdown to the next payment are shown in the market bar. Past payments appear in funding history.

| Situation | Effect |
| --- | --- |
| Long while funding is strongly positive | Pays at every interval |
| Short while funding is strongly positive | Collects on top of any price gain |
| Holding for weeks | Funding can exceed trading fees |
| In and out within an hour | Usually negligible |
