# Raydium Concentrated Liquidity Pools Guide: Creating Fixed-Rate Token Exchanges

This guide explains how to create specialised Raydium concentrated liquidity pools that implement the "TIP Pool" concept described in the paper. The focus is on creating ultra-narrow range, low-fee pools that function as fixed-rate exchanges between tokens.

## Core Strategy Overview

The paper describes a system of chained, ultra-narrow range liquidity pools that:
- Function as fixed-rate exchanges between token pairs
- Allow value to propagate between different tokens
- Enable holders to maintain their original tokens while gaining price exposure to others
- Use minimal trading fees (0.01% recommended)

## Step-by-Step Implementation Guide

### Prerequisites
- Solana wallet with SOL for gas
- The two tokens you want to connect (e.g., Token A and Token B)
- Understanding of Raydium's concentrated liquidity interface (https://docs.raydium.io/raydium/pool-creation/creating-a-clmm-pool-and-farm)
- Understanding of the costs involved (https://docs.raydium.io/raydium/pool-creation/pool-creation-fees)

### Creating the Initial Nominal Pool

1. **Navigate to Raydium Concentrated Liquidity**
- Connect your wallet
- Select "Liquidity" → "Concentrated"
   
2. **Create New Pool**
- Select your token pair
- Choose the lowest fee tier (0.01% recommended)

   
3. **Set Ultra-Narrow Price Range**
   ```
   Important: This is your "positioning" pool that establishes the initial price relationship
   ```
- On the next screen do NOT use the "Full Range" option. Toggle to the "Custom" option.
    - Select the narrowest range the program will accept, filling the lower bound and uppoer bound tightly around the target price(±0.001 from target price)
- Add minimal amounts of both tokens as you will not need this pool later, the funds can be withdrawn but leave the pool open
- Note the exact price and range you've set
   
4. **Confirm and Create Pool**
   - Review all parameters
   - Approve the transaction
   
5. **Optional: Withdraw Liquidity**
   ```
   Important: DO NOT close the pool - just withdraw your tokens
   ```
   - Find your position in "Your Liquidity"
   - Select "Remove Liquidity"
   - Remove all or most liquidity
   - The pool remains open but now has minimal liquidity

### Creating the Main Asymmetric Pool

1. **Create a Second Pool for the Same Token Pair**
   - Select the same tokens as the first pool
   - Use the same low fee tier (0.01%)
   
2. **Position Adjacent to First Pool**
   ```
   Critical: This is where the strategy is implemented
   ```
   - For a single-sided deposit of Token A:
     * Set a very narrow range (as narrow as Raydium allows)
     * Position this range just to the LEFT of your first pool's range
   - For a single-sided deposit of Token B:
     * Set a very narrow range (as narrow as Raydium allows)
     * Position this range just to the RIGHT of your first pool's range
   
3. **Make Your Asymmetric Deposit**
   - Input the amount of just ONE token (the token you want to provide)
   - The interface will automatically disable deposits for the other token
   - Review the expected position details
   
4. **Confirm and Create**
   - Approve the transaction
   - Wait for confirmation

## Strategic Considerations

### Price Range Positioning

```
For buying pressure: position second pool BELOW first pool
For selling pressure: position second pool ABOVE first pool
```

The position of your second pool relative to the first determines:

| Position | Effect | Use Case |
|----------|--------|----------|
| Below first pool | Creates buying pressure | When you expect/want token price to rise |
| Above first pool | Creates selling pressure | When you want to distribute tokens |

### Impact of Pool Parameters

| Parameter | Recommendation | Impact |
|-----------|---------------|--------|
| **Price Range Width** | Ultra-narrow (±0.001) | Maximises capital efficiency, functions as fixed exchange rate |
| **Fee Tier** | Lowest (0.01%) | Minimises friction, encourages arbitrage flow |
| **Deposit Size** | Based on desired liquidity | Larger deposits allow for larger swaps without price impact |
| **Token Selection** | Strategic pairs | Connect tokens that benefit from shared value movements |

## Advanced Implementation: Chaining Multiple Pools

To implement the full value propagation system described in the paper:

1. **Create multiple connected pool pairs**
   ```
   Token Z ⟷ Token Y ⟷ Token X ⟷ ... ⟷ Token N
   ```

2. **Ensure consistent parameters**
   - All pools should use the same low fee tier
   - All pools should use ultra-narrow ranges
   - Position all pools to facilitate value flow in both directions

3. **Consider creating parallel paths**
   - Multiple paths between the same tokens create redundancy
   - Different fee tiers or ranges can serve different use cases

## Example Scenarios

### Coming soon.

## Monitoring and Maintenance
The setup is largely set and forget but it is always recommended to conduct:
1. **Regular Monitoring**
   - Check if market price has moved outside your ranges
   - Monitor available liquidity in your pools

2. **Rebalancing**
   - If price moves significantly, create new pools at updated price levels
   - Consider closing and recreating pools if they've been fully depleted

3. **Performance Assessment**
   - Track swap volumes through your pools
   - Calculate ROI from fees versus capital commitment

## Tips

1. **Test with small amounts first**
   - Verify that your pools are correctly positioned
   - Confirm that asymmetric deposits work as expected

2. **Consider market liquidity**
   - Ensure base pools exist for your tokens in normal markets
   - Larger pools require deeper external markets to function properly

3. **Fee optimisation**
   - Lower fees encourage arbitrage and value propagation
   - Higher fees generate more revenue from volume
   - The paper recommends 0.01% for optimal performance

4. **Range width tradeoffs**
   - Narrower ranges amplify capital efficiency but become inactive more easily
   - Ultra-narrow ranges (±0.001) function as fixed-rate exchanges
   - Slightly wider ranges stay active longer but dilute efficiency

## Final Thoughts

The technique described in this guide creates the foundation for implementing the value propagation system described in the paper. By carefully positioning ultra-narrow range pools and using strategic asymmetric deposits, you can create a network of fixed-rate exchanges that allow value to flow between different tokens while token holders maintain their original investments.

The key innovation is using the initial nominal pool to establish a position, then creating adjacent asymmetric pools that allow single-token deposits. This works within Raydium's concentrated liquidity framework while achieving the paper's goals of creating fixed-rate token exchanges.