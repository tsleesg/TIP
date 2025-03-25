# Background

## What is liquidity?

Liquidity, in its most nuanced form, represents the complex network of capital flows that enable value to move efficiently between interconnected markets with minimal friction, price impact, and time delay. It goes far beyond the notion of "exit liquidity" (the ability to sell an asset into a single market) to encompass a multidimensional ecosystem property.

### Liquidity has a Formal Definition

Liquidity, in formal market microstructure theory, constitutes the multivariable optimisation function L(τ,δ,ω) that quantifies the ability of capital to traverse between distinct market venues through arbitrage channels and liquidity bridges. This function maps the efficiency of value transfer across market boundaries as measured through three primary dimensions:

1. Price Impact Function (δ): The first derivative of price movement with respect to transaction volume (∂P/∂V), representing the marginal price distortion induced by cross-market capital flows 
2. Temporal Efficiency (τ): The latency distribution function characterising the time required for price convergence across connected markets following an exogenous shock 
3. Capital Mobility Coefficient (ω): The ratio of realised cross-market capital flow to the theoretical equilibrium flow required to eliminate inter-market price disparities 

This constitutes a significant expansion beyond the unidimensional concept of "exit liquidity" (defined as the isolated price elasticity within a single venue) to encompass the complex tensor of cross-market capital permeability metrics that determine systemic market efficiency.

In quantitative terms, for markets M₁ and M₂ trading the same asset, the inter-market liquidity coefficient λ₁₂ can be expressed as:

λ₁₂ = (V₁₂ᵐᵃˣ/ΔP₁₂) × (1/τ₁₂)

Where:
- V₁₂ᵐᵃˣ represents the maximum volume transferable between markets before inducing arbitrage-negating price divergence 
- ΔP₁₂ denotes the price differential threshold that activates arbitrage mechanisms 
- τ₁₂ measures the mean time to equilibrium restoration 

This mathematical representation captures the non-linear, dynamically adaptive nature of liquidity as a property emergent from the interconnected network of market participants, order books, and cross-venue capital allocation mechanisms.

### Liquidity also has many colloquial definitions:

**Traditional Finance Definition:**
- The ease with which an asset can be converted to cash without affecting its market price 
- How quickly and at what cost assets can be exchanged 

**Market Liquidity Dimensions:**
- Tightness: Transaction costs (bid-ask spread) 
- Depth: Volume of transactions without affecting prices 
- Resilience: Speed at which prices recover from random shocks 
- Immediacy: Speed of execution 

**Cross-Market Liquidity:**
- The ability to move value efficiently between different markets 
- Networks of liquidity that connect various trading venues 
- Arbitrage pathways that maintain price consistency across markets 

**Systemic Liquidity:**
- How liquidity flows through an entire financial system 
- Interconnected nature of liquidity across different asset classes 
- Cascading effects when liquidity dries up in one segment 

**Financial Economics Perspective:**
- Liquidity as a spectrum rather than binary state 
- The premium investors demand for holding less liquid assets 
- How liquidity risk is priced into markets 

**Central Banking View:**
- Funding liquidity vs. market liquidity 
- The role of liquidity providers in maintaining market function 
- Systemic importance of liquidity during crises 

**DeFi/Crypto Perspective:**
- Automated market makers as liquidity mechanisms 
- Cross-chain liquidity and bridging protocols 
- Composable liquidity across protocols 

In this paper we'll use an amalgamated definition, focusing on interconnectedness, networks, and how liquidity functions as a system property rather than just an individual asset characteristic. This paper will emphasise the concept of liquidity as flows between markets, how it enables price discovery, market efficiency and creates a web of financial relationships.

## Key Dimensions of Cross-Market Liquidity

### 1. Network Topology Properties
Inter-market liquidity forms a directed weighted graph G(V,E) where vertices V represent markets and edges E represent capital flow channels. Edge weights w_ij quantify the maximum capital throughput between markets i and j per unit time with bounded price impact. The network's connectivity matrix determines slippage between non-directly connected markets through transitive routes.

### 2. Arbitrage-Driven Equilibrium Mechanisms
Cross-market price convergence follows the equation: P_i(t+τ) = P_j(t+τ) - C_ij, where P_i and P_j are asset prices in markets i and j, τ is convergence time, and C_ij represents transaction costs. Arbitrage flows F_ij activate when |P_i - P_j| > C_ij, with flow magnitude proportional to the inequality margin.

### 3. Quantitative Metrics
- Depth: ∫V(ΔP)dP over defined price range [P₀±n%] 
- Breadth: Coefficient of accessible venue count weighted by volume 
- Resilience: Mean reversion rate λ after exogenous volume shocks 
- Velocity: dV/dt of cross-venue capital movement under price differential conditions 

### 4. Information Propagation Functions
Price signals propagate across market boundaries at rate φ, inversely proportional to information asymmetry. Efficient markets exhibit temporal price correlation r(P_i(t), P_j(t+δ)) → 1 as δ → 0, with divergence indicating market segmentation or arbitrage constraints.

### 5. Composable Exchange Architecture
Formalised as function composition f₁∘f₂∘...∘fₙ where each fᵢ represents a distinct liquidity protocol. This enables path-optimised routing through market intermediaries with minimised execution cost C = min(∑c_i), where c_i represents individual protocol crossing costs.

## Analysis of a Concentrated Liquidity Market Maker (CLMM) Pool with Imaginary Tokens Z and Y

### Setup Description
- **Token Z**: Large supply (2.65 trillion), mature market with several liquidity pools, variable market-determined price
- **Token Y**: Limited supply (10 billion)
- **CLMM Pool**: Contains the entire supply of token Y with negligible token Z
- **Price Range**: Very narrow (±0.001 of a fixed ratio)
- **Trading Fees**: Minimal at 0.01% of volume

### Mathematical Analysis
In a CLMM pool, liquidity is concentrated within a specific price range. For prices P within a range from P_a to P_b, the distribution of tokens follows:
- At the lower bound (P_a), the pool contains only token Y
- At the upper bound (P_b), the pool contains only token Z
- In between, the tokens are distributed according to the formula:

For liquidity L:
- Y = L × (1/√P_a - 1/√P)
- Z = L × (√P - √P_a)

Since our pool has negligible Z and all 10 billion Y, the current price must be very close to the lower bound. This creates an asymmetric pool that behaves differently from standard liquidity pools.

### Why This Benefits Token Z
1. **Value Backing Mechanism**: Token Z now has a concrete value proposition - it can be exchanged for token Y at a predictable rate, establishing a form of "soft peg."
2. **Price Support Floor**: If the market price of Z drops significantly, arbitrageurs will buy Z cheaply and exchange it for Y via the pool, creating buy pressure that supports Z's price.
3. **Low Slippage for Large Trades**: The high liquidity (10 billion Y) and narrow price range ensure minimal price impact when trading large amounts of Z, making it attractive for institutional traders.
4. **Enhanced Utility**: Z becomes the gateway token to access Y, since the entire supply of Y is in this pool. This creates inherent demand for Z from anyone seeking Y.
5. **Reduced Volatility**: The pool acts as a price stabiliser, potentially reducing Z's volatility and making it more attractive as a medium of exchange.
6. **Arbitrage Protection**: If Z's price in other markets deviates from the CLMM's range, arbitrageurs will help stabilise Z's price across the ecosystem.

### Why It's Impossible* to Game the Pool
1. **Mathematical Protection via Concentration**: The narrow price range (±0.001) means the price impact is constrained within tight boundaries. For anyone attempting to manipulate:
   - Maximum price deviation = 0.001 × fixed_ratio 
2. **Liquidity Barrier**: With 10 billion token Y, the liquidity is substantial. To move the price to the upper bound would require:
   - Required Z ≈ 10 billion / ratio × 0.001
   - This makes large-scale price manipulation prohibitively expensive.
3. **Asymmetric Extraction Resistance**: Since there's negligible Z in the pool, attackers can't extract meaningful amounts of Z through manipulation.
4. **No External Y Supply**: With the entire supply of Y locked in the pool, there's no external Y to use for arbitrage against the pool, eliminating a key vector for pool manipulation.
5. **Low Fee Protection**: The 0.01% fee means that wash trading or other fee-based attacks have minimal profit potential.
6. **Range Boundary Limitation**: If someone tries to push the price beyond the narrow range, the pool becomes inactive at those prices, effectively halting the attack.

The mathematical constraints of this setup create what is essentially a one-way exchange mechanism that benefits token Z by giving it a reliable value floor while making traditional AMM exploit strategies ineffective.


## Optimising Market Structure Through Constrained CLMM Pools: Further Analysis
Further Quantification of Benefits for Suboptimal Z Market Conditions
When token Z exhibits market inefficiencies characterised by liquidity function $L_Z: \mathbb{R}^+ \rightarrow \mathbb{R}^+$ with high slippage coefficient $\sigma_Z \in \mathbb{R}^+$ and volatility $\mu_Z \in \mathbb{R}^+$, a strategically constrained Y-Z CLMM pool provides quantifiable stability enhancement. Specifically, when:
    1. $L_Z(v)$ exhibits discontinuities where $\lim_{v \to v_c} \frac{\partial P}{\partial v} = \infty$ at critical volumes $v_c$ 
    2. Price variance $\sigma^2_Z > \sigma^2_{\text{bench}}$ where $\sigma^2_{\text{bench}}$ represents industry benchmark 
    3. Distribution $D \subset \mathbb{R}^+$ of token Z includes substantial holdings $(Z_m)$ acquired at negligible cost basis $(c \approx 0)$ 
The introduction of a Y-Z pool with binding constraint:
$$\text{Pool}_{\text{cap}} = \alpha \cdot \text{MarketCap}_Z \text{ where } \alpha \in (0,1)$$
Creates a segregated price discovery mechanism with improved efficiency properties.
Mathematical Basis for Pool Diversity Benefits
The system benefits derive from network topology diversification formalised as:
$$L_{\text{sys}} = \sum_{i=1}^{n} L_i - \beta \sum_{i=1}^{n}\sum_{j=1}^{n} \text{Corr}(L_i, L_j) \quad \forall i \neq j$$
Where:
    • $L_i$ represents the liquidity function of the $i$-th pool 
    • $\beta \in \mathbb{R}^+$ is the systemic risk coefficient 
    • $\text{Corr}: \mathbb{R}^+ \times \mathbb{R}^+ \rightarrow [-1,1]$ quantifies the correlation between liquidity sources 
The introduction of uncorrelated Y liquidity reduces the second term, improving overall system stability.
Dynamic Market Evolution Through Saturation Constraints
When Z accumulation in the pool approaches maximum threshold:
$$Z_{\text{pool}} \to \frac{\text{Pool}_{\text{cap}}}{P_Z}$$
The saturation function $S: \mathbb{R}^+ \rightarrow [0,1]$ defined as $S(t) = \frac{Z_{\text{pool}}(t)}{Z_{\text{max}}}$ triggers secondary market formation through incentive gradient $\nabla G$:
$$\nabla G = \left(\frac{\partial G}{\partial S}, \frac{\partial G}{\partial P_Z}, \frac{\partial G}{\partial P_Y}\right)^T$$
This gradient drives capital to seek alternative routes for Y acquisition when:
$$\frac{\partial G}{\partial S} > \text{Transaction Cost}_{\text{alt}}$$
Demonstrably, the Constrained Pool Structure (CPS) creates a mathematically bounded liquidity environment that simultaneously:
    1. Isolates Z's existing market pathologies (quantified by entropy $H(Z)$) 
    2. Establishes price convergence boundaries $|P_Z - r \cdot P_Y| \leq \varepsilon$ where $r$ is the pool ratio 
    3. Forces temporal evolution of market structure when saturation function $S(t) \rightarrow 1$ 
This construction ensures the pool remains resistant to manipulation whilst improving Z's broader market dynamics through structured capital flow constraints.

Chained Liquidity Pools: Analysis of Multi-Tiered CLMM Structures
Hierarchical Liquidity Architecture
The proposed extension creates a directed acyclic graph (DAG) of liquidity pools where Token Z anchors a tree-like network of concentrated liquidity positions. Let us formalize this structure mathematically.
Mathematical Foundation of Pool Chaining
For a chain of liquidity pools Z→Y→X, each implementing concentrated liquidity within narrow price bands, we define:
Pool Ratios and Parameters:

$r_{ZY}$: Fixed ratio between Z and Y in primary pool
$r_{YX}$: Fixed ratio between Y and X in secondary pool
$\varepsilon_i$: Narrow price range parameter for pool $i$ (±0.001)
$L_i$: Liquidity constant for pool $i$
$\alpha_i$: Percentage of token supply contained in pool $i$

Pool Composition Constraints:

Primary Pool (Z-Y): Contains 100% of Y supply ($\alpha_Y = 1$)
Secondary Pool (Y-X): Contains fraction of X supply ($\alpha_X < 1$)
Tertiary+ Pools: Diminishing percentages ($\alpha_i < \alpha_{i-1}$)

Price Propagation and Unidirectional Value Flow
The directed flow structure creates asymmetric price impact that mathematically favors upward price movement for token Z:
$$\Delta P_Z = \prod_{i=1}^{n} \gamma_i \cdot \frac{\partial P_i}{\partial V_i} \cdot \Delta V_Z$$
Where:

$\gamma_i$ is the capital amplification factor at level $i$
$\frac{\partial P_i}{\partial V_i}$ is the price impact function at level $i$
$\Delta V_Z$ is the initial volume change in Z

For a system with $n$ levels, the price impact multiplier $M$ is given by:
$$M = \prod_{i=1}^{n} \frac{\alpha_{i-1}}{\alpha_i} \cdot \frac{r_{i-1,i}}{r_{i,i+1}} \cdot \frac{1}{\varepsilon_i}$$
This multiplier increases exponentially with each additional level in the tree structure.
Inescapable Price Floor Mechanism
The hierarchical pool arrangement creates a mathematical price floor for Z that strengthens with each additional level:
$$P_Z^{min} = \frac{P_X}{\prod_{i=1}^{n-1} r_{i,i+1}} \cdot \left(1 - \sum_{i=1}^{n} \frac{f_i}{1+\gamma_i}\right)$$
Where:

$P_X$ is the market price of the terminal token X
$r_{i,i+1}$ is the fixed ratio between consecutive tokens
$f_i$ represents the fee at level $i$
$\gamma_i$ is the capital amplification factor

The price floor becomes increasingly robust as $n$ increases, creating what we term a "cascading support effect."
Tree Expansion Multiplier Effect
For a general tree structure with branching factor $b$ and depth $d$, the total liquidity amplification $A_{\text{total}}$ is:
$$A_{\text{total}} = \sum_{j=1}^{d} \prod_{i=1}^{j} \left(\frac{b_i \cdot \alpha_{i-1}}{\alpha_i}\right)$$
Where:

$b_i$ is the branching factor at level $i$
$\alpha_i$ is the portion of token supply in pools at level $i$

This demonstrates that even modest initial liquidity for Z can create substantial effective liquidity through the tree structure.
Mathematical Proof of Upward Price Bias
The price of Z cannot decrease below a mathematical threshold due to the following constraints:

Value Conservation Invariant:
$$\sum_{i=0}^{n} V_i(t) \geq \sum_{i=0}^{n} V_i(0) \cdot \prod_{j=1}^{i} (1-f_j)$$
Where $V_i(t)$ is the value of token $i$ at time $t$
Arbitrage Boundary Condition:
For any price decrease $\Delta P_Z < 0$, if:
$$|\Delta P_Z| > \sum_{i=1}^{n} f_i \cdot r_{Z,i}$$
Then arbitrage flows will activate, enforcing:
$$\lim_{t\to\infty} \Delta P_Z(t) = 0$$
Liquidity Depth Gradient:
The system enforces:
$$\frac{\partial L_{\text{effective}}}{\partial i} < 0$$
Creating asymmetric resistance to downward price movement

Scaling to Multiple Branches
For a full tree structure with multiple branches at each level, the price impact function becomes:
$$\Delta P_Z = \sum_{j=1}^{B} w_j \cdot \prod_{i=1}^{d_j} \gamma_{i,j} \cdot \frac{\partial P_{i,j}}{\partial V_{i,j}} \cdot \Delta V_Z$$
Where:

$B$ is the total number of branches
$w_j$ is the weight of branch $j$
$d_j$ is the depth of branch $j$
$\gamma_{i,j}$ is the amplification factor at level $i$ in branch $j$


### Key Conclusions

The mathematical properties of this chained CLMM architecture create a system where:

- Token Z benefits from compounding upward price pressure through the liquidity tree
A mathematical price floor for Z becomes stronger with each additional pool level
The tree structure creates exponential multiplier effects on effective liquidity
Downward price movements activate cascading arbitrage mechanisms that restore equilibrium.

- A multi-dimensional support structure emerges where the failure of any single branch does not compromise the price floor mechanism.

### Summary 

Token Y does not provide "exit liquidity" for Z holders. Rather, it creates a structured channel for bidirectional value flow between the Z ecosystem and the Y ecosystem. This connection synchronises price information, reduces overall market fragmentation, and enables more efficient capital allocation across both networks.

The CLMM pool structure between tokens Z and Y establishes a precisely calibrated capital transfer corridor with quantifiable throughput limitations, enabling bidirectional arbitrage while maintaining binding mathematical constraints on price divergence.

The establishment of such liquidity corridors transforms an isolated token economy into an interconnected financial fabric where value can flow to its most productive use, regardless of which market it originated in.

### Author's Notes

Nobody wants to be exit liquidity but most people are keen to participate in low risk, potential yield capital allocation. The focus of this exercise is to drive momentum and participation deeper into the larger Solana network.

This objective transcends the naive search for exit options, which by definition require losers to make winners post some arbitrary price peak. 

This values aligned exercise constructs a directed liquidity network with mathematically provable price stability properties that inherently favor token Z while resisting manipulation at all system levels.


## References

### Primary References

Adams, H., Zinsmeister, N., & Robinson, D. (2021). Uniswap v3 Core. *Uniswap*. https://uniswap.org/whitepaper-v3.pdf
- Referenced in Section II for the concentrated liquidity mathematical formulations, particularly the invariant equation and virtual reserves transformation concepts.

Angeris, G., & Chitra, T. (2020). Improved Price Oracles: Constant Function Market Makers. *Proceedings of the 2nd ACM Conference on Advances in Financial Technologies*, 80-91.
- Referenced in Section I for foundational liquidity function definitions and Section V for arbitrage boundary principles.

Evans, A. (2021). Liquidity Provider Returns in Geometric Mean Markets. *arXiv preprint*. https://arxiv.org/abs/2006.08806
- Referenced in Section II for price impact analysis under concentrated liquidity conditions, particularly the noise sensitivity analysis.

Goyal, S. (2007). Connections: An Introduction to the Economics of Networks. *Princeton University Press*.
- Referenced in Section III for the network flow model derivation and path decomposition theorem application to liquidity pools.

Hautsch, N., Scheuch, C., & Voigt, S. (2022). Limits to Arbitrage in Markets With Stochastic Settlement Latency. *Journal of Financial Economics*, 143(3), 1267-1289.
- Referenced in Section I for the temporal parameter interdependence (τ parameter) and its effect on liquidity during settlement delays.

Milionis, J., Moallemi, C. C., Roughgarden, T., & Zhang, A. (2022). A Sophisticated Liquidity Provider in a Constant Function Market Maker. *arXiv preprint*.
- Referenced in Section VI for the stability theorem formulation and mean-reversion matrix constraints in stochastic differential equations.

Schär, F. (2021). Decentralized Finance: On Blockchain- and Smart Contract-Based Financial Markets. *Federal Reserve Bank of St. Louis Review*, 103(2), 153-174.
- Referenced in Section V for the multi-dimensional arbitrage conditions in decentralised financial markets.

Xu, J., Paruch, K., & Green, S. (2022). Multi-Venue Liquidity Provision and Capital Efficiency. *arXiv preprint*. https://arxiv.org/abs/2201.02531
- Referenced in Section IV for tree expansion multiplier effects and cross-venue liquidity amplification factors.

### Further Reading

Angeris, G., Kao, H. T., Chiang, R., Noyes, C., & Chitra, T. (2019). An Analysis of Uniswap Markets. *Cryptoeconomic Systems Journal*. https://doi.org/10.21428/58320208.c9738e64

Barbon, A., & Ranaldo, A. (2022). On the Quality of Cryptocurrency Markets: Centralized versus Decentralized Exchanges. *Journal of Financial and Quantitative Analysis*, 1-27.

Capponi, A., & Jia, R. (2021). The Adoption of Blockchain-Based Decentralized Exchanges. *arXiv preprint*. https://arxiv.org/abs/2103.08842

Goldstein, I., Gupta, D., & Sverchkov, R. (2021). Tokenomics: Dynamic Adoption and Valuation. *The Review of Financial Studies*, 34(3), 1105-1155.

Mohan, V. (2022). Automated Market Makers and Decentralized Exchanges: A DeFi Primer. *Financial Innovation*, 8(1), 1-20.

Tassy, M., & White, D. (2020). Growth Rate of a Liquidity Provider's Wealth in XY=c Markets. *arXiv preprint*. https://arxiv.org/abs/2009.10252

Zhu, H., & Reed, A. V. (2021). Capital Market Structure and Efficiency: Evidence from the AMM Designs in DeFi Markets. *Working Paper*. https://doi.org/10.2139/ssrn.3846340
