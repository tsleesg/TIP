# Why Put KIN in the TIP Pool, Explained

This document provides a simple overview of how chaining pools with "fixed" (ultra-narrow range) rate and low-fee, locked pools benefits holders of two arbitrary tokens:

::: mermaid
---
config:
  theme: neutral
---
flowchart LR
    ZPool["Z Token"] <--> |" Fixed Rate, Locked Pool "| XPool["X Token"]
:::

### Basic System Mechanisms
- Pools have ultra-narrow range (±0.001)
  - Function as fixed rate exchanges
- Negligible swap fees (0.01% recommended)
- Locked liquidity pools (funds can't be withdrawn by pool creator)
- Can be entirely one-sided initial deposits (asymmetric/single-token)

- Value propagation
  - Z price increases →
    Value flows Z→Y→X→...→N
  - N price increases →
    Value flows N→...→X→Y→Z

These properties can be curated by an oracle that transparently scores pools to increase investor confidence.

### Chained Value Flows

::: mermaid
---
config:
  theme: neutral
---
flowchart LR
    %% Define token and holder nodes
    H1[Holder 1] <--> Z((Token Z))
    Z <--> ZY[Fixed Fee<br>pool<br>±0.001 Range] <--> Y((Token Y))
    Y <--> YX[Fixed Fee<br>pool<br>±0.001 Range] <--> X((Token X))
    X <--> Dots((...))
    Dots <--> DN[Fixed Fee<br>pool<br>±0.001 Range] <--> N((Token N))
    N <--> H2[Holder 2<br>N Token Holder]
    
    %% Style nodes with Bokeh palette colors
    classDef tokenZ fill:#EC1557,stroke:#EC1557,color:white
    classDef tokenY fill:#F05223,stroke:#F05223,color:white
    classDef tokenX fill:#F6A91B,stroke:#F6A91B,color:white
    classDef tokenN fill:#892889,stroke:#A5CD39,color:white
    classDef poolZY fill:white,stroke:#EC1557,stroke-width:3px
    classDef poolYX fill:white,stroke:#F05223,stroke-width:3px
    classDef poolDN fill:white,stroke:#F6A91B,stroke-width:3px
    classDef holder1 fill:white,stroke:#000,stroke-width:3px
    classDef holder2 fill:white,stroke:#000,stroke-width:3px
    classDef dots fill:white,stroke:#20B254,stroke-width:2px
    
    %% Apply styles
    class Z tokenZ
    class Y tokenY
    class X tokenX
    class N tokenN
    class ZY poolZY
    class YX poolYX
    class DN poolDN
    class H1 holder1
    class H2 holder2
    class Dots dots
:::



### Benefits To Token Holders

| Benefit Type | Holder 1 (Z holder) | Holder 2 (N holder) |
|:------------|:-------------------|:-------------------|
| **Token Ownership** | Keeps Z tokens | Keeps N tokens |
| **Price Exposure** | Gets N price exposure | Gets Z price exposure |
| **Investment Underwriting** | Underwrites investment with Z | Underwrites investment with N |
| **Upside Potential** | Maintains upside potential of N | Maintains upside potential of Z |



## How This System Works

1. **Token Chain Structure**: Tokens Z, Y, X, through N are connected sequentially via concentrated liquidity pools.

2. **Fixed Rate pools**: Each pool has an extremely narrow price range (±0.001), effectively creating a fixed exchange rate between adjacent tokens.

3. **Value Propagation**: When any token in the chain increases in value, arbitrageurs move through the chain to capture the price difference, propagating the value increase to all connected tokens.

4. **No Position Liquidation**: Holders never need to sell their base token, allowing them to maintain their original investment while gaining exposure to other tokens in the chain.

5. **Mathematical Guarantees**: The narrow range pools with locked liquidity create price floors that mathematically guarantee value preservation while allowing price appreciation to flow through the system.

This arrangement allows Holder 1 (who owns token Z) to benefit from price increases in token N without ever having to sell their Z tokens. Similarly, Holder 2 (who owns token N) benefits from price increases in token Z while maintaining their N position. The system essentially creates a bidirectional value conduit where upside flows through the entire chain, benefiting all token holders.

## Asymmetric Liquidity Provision and Value Pools

::: mermaid
---
config:
  theme: neutral
---
flowchart TB
    subgraph "Liquidity Provider Scenario"
        direction LR
        LP["Token X Project<br>(Needs Liquidity)"] --> |"Creates"| Pool["Fixed Rate Pool<br>X-Y<br>(±0.001 Range)<br>Locked"]
        Pool --> |"Initially filled with"| TokenX["X Tokens Only<br>(Asymmetric)"]
        
        ExternalY["Y Token Holder"] --> |"Swaps Y for X"| Pool
        Pool --> |"Now contains"| TokenY["Y Tokens<br>(Replacing X)"]
        
        Market["External Markets"] --> |"Price changes"| Effects
        
        subgraph Effects ["Effect on Liquidity Pool"]
            direction TB
            Effect1["If Y price ↑:<br>Pool value ↑<br>X liquidity value ↑"]
            Effect2["If X price ↑:<br>X selling pressure<br>Pool absorbs some selling"]
        end
    end
:::



### Examples

1. **Asymmetric Pool Creation**: A token project (Token X) can create liquidity by offering a single-sided pool locked at a fixed rate against another token (Token Y).

2. **Locked Liquidity**: The initial liquidity provider (the X token project) locks X tokens in the pool. When Y holders swap to X, Y replaces X in the pool and remains locked.

3. **No Direct Market Price Benefit**: The entity providing the locked pool does not directly benefit from price changes in the external market. Their primary benefit is establishing liquidity for their token.

4. **Indirect Value Effects**:
   - If Y price appreciates: The total liquidity value for X will increase as the pool value increases
   - If X price appreciates: There may be selling pressure as holders take profits, which can be partially absorbed by the pool

5. **Secondary Effects**: The locked liquidity creates price stability and confidence in Token X, potentially attracting more holders and increasing overall market value.

## Incentives for Fixed-Rate, Locked Liquidity Pool Creation
Liquidity is a vital consideration for investors assessing new markets. To stay competitive and aligned with the Solana ecosystem, token providers establish locked liquidity pools as an industry standard. While the provision of liquidity is a fundamental driver, pool providers are motivated by a variety of additional incentives that enhance the appeal of creating these low-risk, fixed-rate pools. Below are some key motivations:

### Trading Fees
A primary and obvious incentive is the revenue generated from trading fees. Even with minimal fees (e.g., 0.01%), pools experiencing high trading volumes can accumulate substantial earnings over time, offering liquidity providers a consistent income stream. Pool creators can experiment with different fee levels depending on their objectives.

### Minimal Marketing Costs
These pools are inherently low-risk for token "buyers" due to their fixed-rate structure and locked liquidity, which ensures stability and predictability. This safety attracts participants organically, reducing the need for extensive marketing efforts. As a result, pools should fill quickly without significant promotional investment, saving projects both time and resources.

### Enhanced Token Visibility and Adoption
Creating a liquidity pool, particularly one linked to a chain of other tokens, boosts a token's exposure within the ecosystem. This increased visibility can drive broader adoption as the token becomes more accessible and interconnected with other projects, appealing to a wider audience of users and investors.

### Regulatory Compliance
In certain jurisdictions, maintaining locked liquidity may align with regulatory requirements or market operation standards. This compliance can reduce legal risks and enhance the project's credibility with regulators and institutional stakeholders.

### Also:
- Strategic Partnerships
- Market Making and Price Stability
- Community Engagement and Loyalty
- Innovation and Experimentation
- Risk Management
- Attracting Institutional Interest


These motivations highlight that creating locked liquidity pools is not just about meeting basic liquidity needs—it's a strategic decision with financial, operational, and community-oriented benefits. Together, these incentives enable projects to strengthen their ecosystem presence, optimise resource use, and appeal to diverse stakeholders, all while maintaining a competitive edge.



## Holder Impacts: Price Change Scenarios in Markets X, Y & Z


### Exit Options for Holders

::: mermaid
---
config:
  theme: neutral
---
flowchart TB
    subgraph "Holder 1 (Z Holder) Options"
        Z1((Z Tokens)) --> |"HOLD"| Option1["Maintain Z position"]
        Z1 --> |"EXIT via regular markets"| Option2["Sell Z in regular markets<br>without using pool system"]
        Z1 --> |"REBALANCE risk via pools"| Option3["Swap some Z→X→Y<br>to capture Y upside directly"]
        Option3 --> |"EXIT via Y market"| Option4["Sell Y in Y markets<br>reducing X market sell pressure"]
        Option3 --> |"SWAP back to Z"| Z1
    end
    
    classDef options fill:#f5f5f5,stroke:#333,stroke-width:1px
    classDef token fill:#d4f1f9,stroke:#29b6f6,stroke-width:2px,color:black
    
    class Option1,Option2,Option3,Option4,Option5,Option6 options
    class Z1,Y1 token
:::

Note the reduced sell pressure on the Z market under this system.




## De-Risking Z for Holders and Its Ecosystem
A primary benefit to holders using this system is better distribution of their portfolio which brings inherent de-risking benefits.


::: mermaid
---
config:
  theme: neutral
  flowchart:
    htmlLabels: true
---
flowchart LR
    subgraph RMM["Risk Mitigation"]
        direction TB
        Risk1["Initial Risk:<br>Holders exposed only to<br>their token Z's price movements"]
        Risk2["Holders gain access to other tokens via pools<br>at fixed rates"]
        Risk3["Result:<br>Shifted exposure, revert<br>at any time with minimal cost"]
        Risk1 --> Risk2 --> Risk3
    end
    
    SB["<div style='text-align:left'><b>System Benefits for Z</b><br>• Indirect exposure to other tokens' upside<br>through value propagation<br>• Reduced sell pressure on Z markets<br>due to alternative exit paths<br>• Enhanced price stability through<br>interconnected liquidity<br>• Ability to rebalance portfolio<br>without direct selling</div>"]
    
    ZB["<div style='text-align:left'><b>Z Holder Benefits</b><br>• Can maintain Z position<br>• Can acquire X at fixed rate if X is undervalued<br>• Can shift to X when Z is overvalued<br>• Maintains exit options through Z markets<br>• No exposure to X downside unless swapped</div>"]
    
    %% Connect System Benefits to the RMM subgraph
    RMM --> SB
    
    %% Connect Z Holder Benefits to Risk2 (second green box)
    Risk2 --> ZB
    
    %% Position the benefit boxes to the right of the Risk Mitigation box
    SB ~~~ Risk3
    ZB ~~~ SB
    
    classDef risk fill:none,stroke:#A5CD39,stroke-width:2px
    classDef benefit fill:none,stroke:#F6A91B,stroke-width:2px
    classDef subgraphStyle fill:none,stroke:#dedede,stroke-width:1px
    
    class Risk1,Risk2,Risk3 risk
    class SB,ZB benefit
    class RMM subgraphStyle
:::    




### Detailed Scenario when X Price Increases in its Market

::: mermaid
---
config:
  theme: neutral
---
sequenceDiagram
    participant XM as X Market
    participant XH as X Holder
    participant XY as X-Y Fixed pool<br>(±0.001 range)
    participant YZ as Y-Z Fixed pool<br>(±0.001 range)
    participant ZH as Z Holder
    
    Note over XH: Initial State:<br>Holds X tokens
    Note over ZH: Initial State:<br>Holds Z tokens
    
    XM->>XM: X price increases in<br>regular X market only
    Note right of XM: Markets are decoupled<br>Z price unchanged
    
    Note over XH: Options for X Holder:
    XH->>XH: 1. HOLD X:<br>Benefiting from<br>X appreciation
    XH->>XM: 2. SELL X:<br>Take profits at<br>appreciated price
    
    XH-->>XY: 3a. Swap X→Y through pool<br>(0.01% fee)
    Note right of XY: Getting more Y per X<br>than before X appreciated
    XY-->>YZ: 3b. Possibly swap Y→Z<br>(additional 0.01% fee)
    Note right of YZ: May get favorable rate<br>compared to direct X→Z market swap
    
    Note over ZH: Options for Z Holder:
    ZH->>ZH: 1. HOLD Z:<br>No direct benefit from<br>X appreciation
    
    ZH-->>YZ: 3a. Swap Z→Y through pool<br>(0.01% fee)
    YZ-->>XY: 3b. Swap Y→X through pool<br>(additional 0.01% fee)
    Note right of XY: Benefits from X appreciation<br>by acquiring X at fixed pool rate
    
    Note over XH,ZH: pool provides fixed-rate<br>exchange path unaffected by<br>external market movements
:::




### Detailed Scenario when Z Price Increases in its Market


::: mermaid
---
config:
  theme: neutral
---
sequenceDiagram
    participant XH as X Holder
    participant XY as X-Y Fixed pool<br>(±0.001 range)
    participant YZ as Y-Z Fixed pool<br>(±0.001 range)
    participant ZH as Z Holder
    participant ZM as Z Market
    
    Note over XH: Initial State:<br>Holds X tokens
    Note over ZH: Initial State:<br>Holds Z tokens
    
    ZM->>ZM: Z price increases in<br>regular Z market only
    Note right of ZM: Markets are decoupled<br>X price unchanged
    
    Note over ZH: Options for Z Holder:
    ZH->>ZH: 1. HOLD Z:<br>Benefiting from<br>Z appreciation
    ZH->>ZM: 2. SELL Z:<br>Take profits at<br>appreciated price
    
    ZH-->>YZ: 3a. Swap Z→Y through pool<br>(0.01% fee)
    Note right of YZ: Less optimal after Z appreciates<br>(getting less Y per Z)
    YZ-->>XY: 3b. Possibly swap Y→X<br>(additional 0.01% fee)
    Note right of XY: Only logical if seeking X exposure<br>or if pool rate better than markets
    
    Note over XH: Options for X Holder:
    XH->>XH: 1. HOLD X:<br>No direct benefit from<br>Z appreciation
    
    XH-->>XY: 3a. Swap X→Y through pool<br>(0.01% fee)
    XY-->>YZ: 3b. Swap Y→Z through pool<br>(additional 0.01% fee)
    Note right of YZ: Benefits from Z appreciation<br>by acquiring Z at fixed pool rate
    
    Note over XH,ZH: pool provides accessibility<br>to other tokens at fixed rates<br>regardless of market fluctuations
:::

#### System's Beneficial-Only Impact
Without this system, a price increase in X or Z would likely result in holders selling directly into the open market, potentially amplifying selling pressure and causing sharper price drops. The system’s buffering effect ensures that the selling pressure remains equal to or less than what would occur in a standard market setup, maintaining greater price stability.
