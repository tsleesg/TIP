# Key Visualisations
## Liquidity Function Flow Diagram
::: mermaid
---
config:
  theme: neutral
---
flowchart TD
    A["Liquidity Function L(τ, δ, ω)"] --> B["Price Impact Function δ"]
    A --> C["Temporal Efficiency τ"]
    A --> D["Capital Mobility Coefficient ω"]
    B --> E["∂P/∂V: Price change per volume unit"]
    C --> F["Time for price convergence across markets"]
    D --> G["Ratio of realised to theoretical equilibrium flow"]
    E --> H["Inter-market Liquidity Coefficient λ₁₂"]
    F --> H
    G --> H
    H --> I["λ₁₂ = (V₁₂ᵐᵃˣ/ΔP₁₂) × (1/τ₁₂)"]
    
    classDef root fill:#f5f5f5,stroke:#EC1557,stroke-width:2px
    classDef level1 fill:#f5f5f5,stroke:#F05223,stroke-width:2px
    classDef level2 fill:#f5f5f5,stroke:#F6A91B,stroke-width:2px
    classDef level3 fill:#f5f5f5,stroke:#A5CD39,stroke-width:2px
    classDef level4 fill:#f5f5f5,stroke:#20B254,stroke-width:2px
    
    class A root
    class B,C,D level1
    class E,F,G level2
    class H level3
    class I level4
:::

## Arbitrage Mechanism Sequence Diagram
::: mermaid
---
config:
  theme: neutral
---
sequenceDiagram
    participant Market_i
    participant Arbitrageur
    participant Market_j
    
    Note over Market_i,Market_j: Initial state: |P_i - P_j| > C_ij
    Market_i->>Arbitrageur: Price P_i at time t
    Market_j->>Arbitrageur: Price P_j at time t
    
    Arbitrageur->>Arbitrageur: Calculate price differential
    Arbitrageur->>Arbitrageur: Activate flow F_ij when |P_i - P_j| > C_ij
    
    alt P_i < P_j - C_ij
        Arbitrageur->>Market_i: Buy asset
        Arbitrageur->>Market_j: Sell asset
    else P_i > P_j + C_ij
        Arbitrageur->>Market_j: Buy asset
        Arbitrageur->>Market_i: Sell asset
    end
    
    Note over Market_i,Market_j: Final state: P_i(t+τ) = P_j(t+τ) - C_ij
:::

## CLMM Pool Distribution Flow Diagram
::: mermaid
---
config:
theme: neutral
---

flowchart LR

A[CLMM Pool with Tokens Z and Y] --> B[Lower Bound P_a]
A --> C[Current Price P]
A --> D[Upper Bound P_b]
B --> E["Pool contains only token Y"]
D --> F["Pool contains only token Z"]
C --> G["Token Distribution at Price P"]
G --> H["Y = L × (1/√P_a - 1/√P)"]
G --> I["Z = L × (√P - √P_a)"]
J["Narrow Price Range (±0.001)"] --> A

classDef pool stroke:#EC1557,stroke-width:2px
classDef bounds stroke:#F05223,stroke-width:2px
classDef price stroke:#F6A91B,stroke-width:2px
classDef tokenY stroke:#A5CD39,stroke-width:2px
classDef tokenZ stroke:#20B254,stroke-width:2px
classDef distribution stroke:#00AAAE,stroke-width:2px
classDef formula stroke:#4998D3,stroke-width:2px
classDef range stroke:#892889,stroke-width:2px

class A pool
class B,D bounds
class C price
class E tokenY
class F tokenZ
class G distribution
class H,I formula
class J range

:::

## Hierarchical Liquidity Architecture Flow
::: mermaid
---
config:
  theme: neutral
---
flowchart TD
    A[Token Z] --> |r_ZY| B[Token Y]
    B --> |r_YX| C[Token X]
    B --> |r_YW| D[Token W]
    C --> |r_XV| E[Token V]
    
    A --> F["Primary Pool: 100% of Y supply (α_Y = 1)"]
    B --> G["Secondary Pools: Fraction of supply (α_X < 1, α_W < 1)"]
    C --> H["Tertiary Pools: Diminishing percentages (α_V < α_X)"]
    
    I["Price Floor for Z: P_Z^min = P_X / ∏r_i,i+1 × (1-∑f_i/(1+γ_i))"] --> A
    
    J["Price Impact Multiplier: M = ∏(α_i-1/α_i) × (r_i-1,i/r_i,i+1) × (1/ε_i)"] --> A
:::

## Liquidity Network Topology Diagram
::: mermaid
---
config:
  theme: neutral
---
graph TD
    A[Market 1] -- "w_12: Capital flow channel" --> B[Market 2]
    A -- "w_13: Capital flow channel" --> C[Market 3]
    B -- "w_23: Capital flow channel" --> C
    C -- "w_34: Capital flow channel" --> D[Market 4]
    B -- "w_24: Capital flow channel" --> D
    subgraph "Network Topology G(V,E)"
        A
        B
        C
        D
    end
    E[Arbitrage Flow F_ij activates when difference in prices exceeds C_ij] --> A
    E --> B
    F["Edge weights w_ij quantify maximum capital throughput"] --> A
    F --> B

:::

## System Liquidity Calculation Flow
::: mermaid
---
config:
theme: neutral
---
flowchart TD
A["System Liquidity L_sys"] --> B["Sum of Individual Pool Liquidity: ∑L_i"]
A --> C["Correlation Penalty: β∑∑Corr(L_i,L_j)"]
B --> D["L_sys = ∑L_i - β∑∑Corr(L_i,L_j)"]
C --> D
E["Pool Diversity Benefits"] --> F["Uncorrelated Liquidity Sources"]
F --> G["Reduced Systemic Risk"]
G --> A
H["Saturation Function S(t) = Z_pool(t)/Z_max"] --> I["Triggers Secondary Market Formation"]
I --> J["When ∂G/∂S > Transaction Cost_alt"]

classDef formula stroke:#EC1557,stroke-width:2px
classDef concept stroke:#F6A91B,stroke-width:2px
classDef effect stroke:#20B254,stroke-width:2px
classDef trigger stroke:#4998D3,stroke-width:2px

class A,D formula
class B,C,E,F concept
class G effect
class H,I,J trigger
:::
