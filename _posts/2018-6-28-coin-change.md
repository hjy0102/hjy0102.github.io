---
layout: post
title: Coin Change
category: HackerRank
---


```cpp
/**
You are given coins of different denominations and a total amount of money amount. Write a function to 
compute the fewest number of coins that you need to make up that amount. If that amount of money cannot 
be made up by any combination of the coins, return -1.

Example 1:
coins = [1, 2, 5], amount = 11
return 3 (11 = 5 + 5 + 1)
*/

class Solution {
public:
	int coinChange(vector<int>& coins, int amount) {
		const int INF = 0x7fffffff;
		vector<int> dp(amount + 1, INF);
		dp[0] = 0;
		for (int i = 0; i <= amount; i++) {
			for (int j = 0; j<coins.size(); j++) {
				if (coins[j] != INF && i + coins[j] <= amount && dp[i] != INF && dp[i + coins[j]] > dp[i] + 1)
					dp[i + coins[j]] = dp[i] + 1;
			}
		}
		return dp[amount] == INF ? -1 : dp[amount];
	}
};
```
