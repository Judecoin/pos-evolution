# Legacy PoS References

This page keeps older general Proof-of-Stake reference material for historical reference.

Some information on this page may not directly reflect the current Judecoin service node implementation or the latest Proof-of-Stake transition.

For current Judecoin service node operation, please refer to the main documents in this repository.

## Proof of Stake Overview

Many people wonder what Proof of Stake is, and how it works. On this page you will find older general Proof-of-Stake reference links and FAQ content. If anything is missing or unclear, please refer to the current Judecoin documentation or official community channels.

**General Proof-of-Stake references:**

* https://en.wikipedia.org/wiki/Proof-of-stake
* https://www.investopedia.com/terms/p/proof-stake-pos.asp
* http://cryptocurrencyfacts.com/proof-of-stake-pos/

**Technical references:**

* https://github.com/ethereum/wiki/wiki/Proof-of-Stake-FAQ
* https://en.bitcoin.it/wiki/Proof_of_Stake
* https://bitcoinmagazine.com/articles/what-proof-of-stake-is-and-why-it-matters-1377531463/

**Original whitepapers:**

* Peercoin PoS: https://peercoin.net/assets/paper/peercoin-paper.pdf
* Blackcoin PoS v2: http://blackcoin.co/blackcoin-pos-protocol-v2-whitepaper.pdf
* Blackcoin PoS v3: https://blackcoin.org/Blackcoin-POS-3.pdf
* Blackcoin PoS v3.1: https://blackcoin.org/blackcoin-pos-protocol-v3.1-whitepaper.pdf

## FAQ

### How can I participate in PoS?

You leave your wallet open, connected to the Internet. The amount of coins you have determines how often you will receive a reward. Additionally, if you have encrypted your wallet, you need to "unlock" it in order to be able to stake. There is usually an indicator in your wallet that will say "Staking".

### Is there a minimum amount of coins necessary to stake?

No. It will just take much longer until you get a reward, if you only have a few coins.

### Does my PC have to be online 24/7?

No. But you might not get the full reward if you are offline a lot, depending on the implementation. PoS 1 and 2 have mechanisms to ensure that you will always receive the full reward according to your balance, while with PoS 3, your total reward will depend on the amount of time you have been online. For more details, see the [Calculations section](#calculations) below.

### Does my wallet have to be encrypted?

No. If your wallet is not encrypted, there is no need to unlock it.

### Why does the "expected time to reward" not decrease?

Because it is just an estimation of the _average_ time you need to wait. It depends on the network weight and your local weight. If some of your coins become immature or when the network weight changes, then this number will change accordingly. If nothing changes, then this number will stay the same, since it is the _expected_ time you need to wait, on average.

### Why is my local weight less than the number of coins I have?

See above.

### Why is my stake "conflicted" or "not accepted"?

You created (minted/forged) a block, and should get the reward, but some other block was added to the blockchain some seconds earlier than yours. That means your block is not included in the current blockchain. This is completely normal, the next time you may be some seconds earlier than someone else.

## Calculations

The idea of PoS is that you will generate blocks according to your fair share in the network. For example, if you own 1% of the coins in the network, you will generate every 100th block. Unfortunately the "local weight" and the "network weight" are not completely accurate numbers, as coins that just generated a block are disqualified for a certain time and do not contribute to the weight until the stake is mature. We will still use these two numbers for a rough estimation. Also, because new coins you earned will add to your local weight after they have become mature, the reward curve is exponential. But using a linear estimation here is usually good enough to get an idea.

### Time between rewards

As I said, you will generate blocks according to your fair share in the network. This is true for PoS 2 and PoS 3. So you can calculate the average time between your rewards using this formula:

* `Waiting time = Network weight / Local weight * Block time`

where `Network weight` is the total balance of _all_ participants in the network, including ourselves. In PoS 1, your local weight will increase over time, so even very small balances will get a reward from time to time. This comes with various security problems, which is why PoS 2 was invented.

### Number of rewards per time

Based on the above formula, you can calculate the number of rewards per time unit by dividing your desired time span through your expected waiting time:

* `Rewards per Time = Time / Waiting time`

For example with `Time = one Year` you will get the number of rewards per year.

### Total reward per time

With PoS 1 and 2, the reward size will be adjusted based on the last time you staked using those coins, in such a way that it totals out to a fixed percentage per year:

* `PoS 1/2 Reward = Time / one Year * Balance * Percentage`

So for `Time = one Year` that is simply `Balance * Percentage`.

With PoS 3, the reward size is calculated as a fixed percentage of the total coin supply:

* `PoS 3 Reward Size = Coin supply * Percentage / Blocks per Year`

where `Blocks per Year = one Year / Block time`. When we know the reward size, calculating the total reward is simple:

* `PoS 3 Reward = Rewards per Time * Reward size`

### Putting it together

If we assume for PoS 3 that _everybody_ is staking, so that `Network weight = Coin supply`, we can simplify the equations as follows:

```text
PoS 3 Reward = Rewards per Time * Reward size
= Rewards per Time * (Coin supply * Percentage / Blocks per Year)
= (Time / Waiting time) * (Coin supply * Percentage / Blocks per Year)
= (Time / (Network weight / Local weight * Block time))
    * (Coin supply * Percentage / Blocks per Year)
= Time / Block time * Local weight * Percentage / Blocks per Year
