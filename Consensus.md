  Start with the current Solana architecture which has all validators voting on all blocks and that consensus requires 66% of the stake before a block is committed to the chain.  Reducing the number of consensus participants has been part of the plan for Safecoin from the beginning.  By reducing the number of participants you reduce the amount of voting which in general makes the validators and the overall cluster run more efficiently.  As long as you don’t reduce the consensus stake too much (and keep the voters random) it is still extremely hard for a group of validators to consistently apply a high stake amount in order to attack the chain. 

The first stab at the reducing the number of vote participants was to only allow a 10% sample of the validators to vote on each block.  This required three changes; the first change, obviously, in the TVU code where vote transactions are created, then a corresponding change is added into the TPU because votes are themselves transactions so you need to verify that only the same 10% sample of validator’s transactions *actually* vote.  (Because you can imagine a attack where validators send extra vote transactions *outside* the sample). The third change was to reduce the vote stake threshold for consensus down from 66% to 4% because if you reduce the voters by 90% you need to correspondingly reduce the minimum voted stake by 90%.

But wait, you might notice that reducing by 90% would make the stake requirement 6.6% not 4%!!!  What gives?  What gives is statistics. The problem with this attempt was that the 10% check resulted in the “bell curve”. On average with 60 validators, then (two-thirds of the time) six validators vote but on the tails of the curve more than six and fewer than six would vote.  And even, very rarely, ZERO validators would vote.  Add in the fact that stake is very unevenly distributed amongst the validators (whales and minnows) … any way, the result was that you would have too many blocks where you never got enough stake to reach commitment. This resulted in skips for validators and retries for applications running transactions.  So after (I think/assume) trying 6.6% of stake for consensus they dropped the consensus requirement to 4% which reduced the number of skips to a tolerable amount (while still requiring a big enough consensus stake to make attacks nigh impossible)

So nobody was satisfied with the first stab at reducing the consensus requirements and a “second stab” was desired.  My improvement is to make the reduced consensus “smoother”, more consistent. So instead of selecting validators by rolling a 10-sided die each time, the new implementation is to put all the (staked) validators in a bag and randomly pull out six (or whatever number) of them every time you need to decide who votes on a given block.  You are still up against the whales vs minnows stake distribution problem but at least you don’t have to worry about the bell curve choosing zero validators.  