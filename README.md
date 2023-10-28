Many people wonder what Proof of Stake is, and how it works. In this document you will find a few overview links, and a FAQ further down. If there is anything missing or still unclear, feel free to ask me about it!

**Overview:** 

* https://en.wikipedia.org/wiki/Proof-of-stake
* https://www.investopedia.com/terms/p/proof-stake-pos.asp
* http://cryptocurrencyfacts.com/proof-of-stake-pos/

**More technical (not for newbies):**

* https://github.com/ethereum/wiki/wiki/Proof-of-Stake-FAQ
* https://en.bitcoin.it/wiki/Proof_of_Stake
* https://bitcoinmagazine.com/articles/what-proof-of-stake-is-and-why-it-matters-1377531463/
* http://earlz.net/view/2017/07/27/1904/the-missing-explanation-of-proof-of-stake-version


**Original whitepapers:**

* Peercoin PoS: https://peercoin.net/assets/paper/peercoin-paper.pdf
* Blackcoin PoS v2: http://blackcoin.co/blackcoin-pos-protocol-v2-whitepaper.pdf
* Blackcoin PoS v3: https://bravenewcoin.com/assets/Whitepapers/Blackcoin-POS-3.pdf


# FAQ

### How can I participate in PoS?

You leave your wallet open, connected to the Internet. The amount of coins you have determines how often you will receive a reward. Additionally, if you have encrypted your wallet, you need to "unlock" it in order to be able to stake. There is usually an indicator in your wallet that will say "Staking".

### Is there a minimum amount of coins necessary to stake?

No. It will just take much longer until you get a reward, if you only have a few coins.

### Does my PC have to be online 24/7?

No. But you might not get the full reward if you are offline a lot, depending on the implementation. POS 1 and 2 have mechanisms to ensure that you will always receive the full reward according to your balance, while with POS 3, your total reward will depend on the amount of time you have been online. Fore more details, see the [Calculations section](#calculations) below.

### Does my wallet have to be encrypted?

No. If your wallet is not encrypted, there is no need to unlock it.

### Why does the "expected time to reward" not decrease?

Because it is just an estimation of the _average_ time you need to wait. It depends on the network weight and your local weight. If some of your coins become immature or when the network weight changes, then this number will change accordingly. If nothing changes, then this number will stay the same, since it is the _expected_ time you need to wait, on average.

### What does "immature" / "not mature" mean?

When some of your coins have staked or just arrived at your wallet, they are "disqualified" for a certain time. This is necessary for technical reasons. We call these coins "immature". After a certain time (that depends on your coin), they will become mature. Only coins that are mature can participate in staking, and are added to your local weight.

### Why is my local weight less than the number of coins I have?

See above.

### Why is my stake "conflicted" or "not accepted"?

You created (minted/forged) a block, and should get the reward, but some other block was added to the blockchain some seconds earlier than yours. That means your block is not included in the current blockchain. This is completely normal, the next time you may be some seconds earlier than someone else.

# Calculations

The idea of POS is that you will generate blocks according to your fair share in the network. For example, if you own 1% of the coins in the network, you will generate every 100th block. Unfortunately the "local weight" and the "network weight" are not completely accurate numbers, as coins that just generated a block are disqualified for a certain time and do not contribute to the weight until the stake is mature. We will still use these two numbers for a rough estimation. Also, because new coins you earned will add to your local weight after they have become mature, the reward curve is exponential. But using a linear estimation here is usually good enough to get an idea.

### Time between rewards

As I said, you will generate blocks according to your fair share in the network. This is true for POS 2 and POS 3. So you can calculate the average time between your rewards using this formula:

* `Waiting time = Network weight / Local weight * Block time`

where `Network weight` is the total balance of _all_ participants in the network, including ourselves. In POS 1, your local weight will increase over time, so even very small balances will get a reward from time to time. This comes with various security problems, which is why POS 2 was invented.

### Number of rewards per time

Based on the above formula, you can calculate the number of rewards per time unit by dividing your desired time span through your expected waiting time:

* `Rewards per Time = Time / Waiting time`

For example with `Time = one Year` you will get the number of rewards per year.

### Total reward per time

With POS 1 and 2, the reward size will be adjusted based on the last time you staked using those coins, in such a way that it totals out to a fixed percentage per year:

* `POS 1/2 Reward = Time / one Year * Balance * Percentage`

So for `Time = one Year` that is simply `Balance * Percentage`.

With POS 3, the reward size is calculated as a fixed percentage of the total coin supply:

* `POS 3 Reward Size = Coin supply * Percentage / Blocks per Year`

where `Blocks per Year = one Year / Block time`. When we know the reward size, calculating the total reward is simple:

* `POS 3 Reward = Rewards per Time * Reward size`

### Putting it together

If we assume for POS 3 that _everybody_ is staking, so that `Network weight = Coin supply`, we can simplify the equations as follows:

```
POS 3 Reward = Rewards per Time * Reward size
= Rewards per Time * (Coin supply * Percentage / Blocks per Year)
= (Time / Waiting time) * (Coin supply * Percentage / Blocks per Year)
= (Time / (Network weight / Local weight * Block time))
    * (Coin supply * Percentage / Blocks per Year)
= Time / Block time * Local weight * Percentage / Blocks per Year
```

With `Local weight = Balance`, `Time = one Year` and `Blocks per Year = one Year / Block time` we get a total reward of `Balance * Percentage` per year, which is the same as for POS 2!

If we re-insert this lower bound of the total reward into the original equation, we get:

```
POS 3 Reward = Rewards per year * Reward size = Balance * Percentage

=> Rewards per year = Balance * Percentage / Reward size
```

and with `Rewards per year = (365 days / Waiting time)`

```
(365 days / Waiting time) = Balance * Percentage / Reward size

=> Waiting time (days) = 365 * Reward size / (Balance * Percentage)
```

Realistically not everybody is staking, so the numbers will be better by a factor of `Coin supply / Network weight`. In particular, the total reward with POS 3 will be higher than with POS 2 if you stake 24/7.

## Example calculations

If we assume that everybody on the network is staking, the following equations hold for all classical POS implementations:

* You will get `Balance * Percentage` coins per year, on average
* You will get `Balance * Percentage / 365` coins per day, on average

If your coin uses POS 3, we can additionally make the following calculations:

* You will get a reward `Balance * Percentage / Reward size` times per year, on average.
* You will get a reward `Balance * Percentage / Reward size / 365` times per day, on average.
* The average waiting time is `365 * Reward size / (Balance * Percentage)` days (the inverse of the above).
* The minimum balance you need to stake at least 365 times per year (once a day on average) is `365 * Reward size / Percentage` (setting the above to 1).

As a rule of thumb we can assume that 50% will be staking, so for POS 3 the numbers will be better (higher or lower) by a factor of 2 if you stake 24/7, and will be about accurate if you stake 12 hours a day.

# Optimization

tbd.