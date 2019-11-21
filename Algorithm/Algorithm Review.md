---
title: Leetcode Summary
date: 2019-07-26T16:48:12.773Z
tags: ['Algorithm']
categories: ['CS']
---

# Algorithm Review

## Greedy
|Name|difficulty|Solution|Link|
|:--:|:--:|:--:|:--:|
|316. Remove Duplicate Letters|Hard|Find the current smallest achievable letter and continue searching the rest|https://leetcode.com/problems/remove-duplicate-letters/description/|
|968. Binary Tree Cameras|Hard|Start from leaves, the parent of leaf always take less cameras to cover than the leaf itself carries a camera. Thus we derive from bottom to top and get the result.|https://leetcode.com/problems/binary-tree-cameras/description/|



## Monotonic Stack
|Name|difficulty|Solution|Link|
|:--:|:--:|:--:|:--:|
|316. Remove Duplicate Letters|Hard|Use a increasing stack to keep the str in order and use visited to keep the uniqueness of the letters|https://leetcode.com/problems/remove-duplicate-letters/description/|
|402. Remove K Digits| Medium| Keep the chars in increasing order and count the poped element. If we didn't delete enough element we delete from the end| https://leetcode.com/problems/remove-k-digits/description/|
|739. Daily Temperatures|Medium|classic Monostack Practice|https://leetcode.com/problems/daily-temperatures/description/|
|901. Online Stock Span|Medium|Keep a decreasing stack, and keep track the price and its appearace. If we find something to insert, just update it with the previous appearance.|https://leetcode.com/problems/online-stock-span/description/|
|962. Maximum Width Ramp|Medium|Maintain a decreasing stack of the array(the first one). Then search from the tail and try to enlarge the interval.|https://leetcode.com/problems/maximum-width-ramp/description/|
|907. Sum of Subarray Minimums|Medium|Maintain nextMin[] and prevMin[], then we scan from left to right, update res by A[i] * (i-prevMin[i])*(nextMin[i] - i). Note that the default of next should len(A), the other is -1|https://leetcode.com/problems/sum-of-subarray-minimums/description/|
|1124. Longest Well-Performing Interval|Medium| Same as maximum width ramp. Transform into subarray sum > k problem.|https://leetcode.com/problems/longest-well-performing-interval/description/|
|84. Largest Rectangle in Histogram|Hard|Use single monotonic stack, or 2 mono stack expanding each item.|https://leetcode.com/problems/largest-rectangle-in-histogram/description/|


## Binary Search
|Name|difficulty|Solution|Link|
|:--:|:--:|:--:|:--:|
|658. Find K Closest Elements|Medium|Use binary search to find a size k interval. Compare the distance from left bound to the x and right bound to x|https://leetcode.com/problems/find-k-closest-elements/description/|
|392. Is Subsequence|Easy|Practice bin search.|https://leetcode.com/problems/is-subsequence/description/|

## Prefix Sum
|Name|difficulty|Solution|Link|
|:--:|:--:|:--:|:--:|
| 548. Split Array with Equal Sum|Mediumn|find all possible positions of j, and find all possiblt positions of i and k. Use the prefixSum to check if we have seen the same interval sum.|https://leetcode.com/problems/split-array-with-equal-sum/description/|
|1171. Remove Zero Sum Consecutive Nodes from Linked List|Medium|Basic prefix sum practice. Use hashmap to record previous presum, when meet the same value, delete the part in between. Remember to delete previous presum after interval removal.|https://leetcode.com/contest/weekly-contest-151/problems/remove-zero-sum-consecutive-nodes-from-linked-list/|

## Divide & Conquer
|Name|difficulty|Solution|Link|
|:--:|:--:|:--:|:--:|
|312. Burst Balloons| Hard| dp(left, right) = nums[left] * nums[mid] * nums[right] + dp(left, mid) + dp(mid, right), left < mid < right | https://leetcode.com/problems/burst-balloons/description/  |
|53. Maximum Subarray| Easy | find the mid pos, solve its left and right subproblem, get the current result from mid to both ends, then merge the result.|https://leetcode.com/problems/maximum-subarray/description/|

## DP
|Name|difficulty|Solution|Link|
|:--:|:--:|:--:|:--:|
|312. Burst Balloons| Hard| dp(left, right) = nums[left] * nums[mid] * nums[right] + dp(left, mid) + dp(mid, right), left < mid < right. Find all possible length first, then search from left to right, from short to long of all subarrays(Bottom up)| https://leetcode.com/problems/burst-balloons/description/  |
|53. Maximum Subarray| Easy | dp[i] = dp[i-1] > 0?:dp[i-1] + nums[i]: nums[i]|https://leetcode.com/problems/maximum-subarray/description/|
|801. Minimum Swaps To Make Sequences Increasing|Medium|if is already valid, swap[i] = swap[i-1] + 1, keep[i] = keep[i-1. It we can swap, keep[i] = min(keep[i], swap[i-1]), swap[i] = min(swap[i], keep[i-1] + 1| https://leetcode.com/problems/minimum-swaps-to-make-sequences-increasing/description/|
|750. Number Of Corner Rectangles| Medium | dp[i][j] means the number of matches between colomn i and j. Loop all items and scan the right of it, update res = dp[i][k]++, when grid[i][j] == 1 and grid[i][k] == 1. | https://leetcode.com/problems/number-of-corner-rectangles/description/|
|1140. Stone Game II|Medium|dp(ind, m) = max points of cur player given ind and m. We search next player's possible points and pick the smallest. then return all points- opponent's points. can use a postsum array to optimize|https://leetcode.com/problems/stone-game-ii/description/|
|221. Maximal Square|Medium|dp[i][j] means the length of the square whose bottom-right corner is current pos. dp[i][j] = min(dp[i,j-1], dp[i-1, j], dp[i-1, j-1])+1 if grid[i][j] != 0, else 0. Can further optimize the space to On|https://leetcode.com/problems/maximal-square/description/|
|688. Knight Probability in Chessboard|Medium|dp[k][i][j] = sum(dp[k-1][i-dx][j-dy]) where dx dy in 8 directions|https://leetcode.com/problems/knight-probability-in-chessboard/description/|
|879. Profitable Schemes|Hard|dp[i, j] = given profit i and j people, the total number of profitable schemes.dp[i+p, j+g] += dp[i][j], the target we want is dp[P, _] and dp[P++, _]. Thus we combine all the answers to dp[P, _].|https://leetcode.com/problems/profitable-schemes/description/|
|1155. Number of Dice Rolls With Target Sum|Medium|Similar to Coin Change. dp[i][j] += dp[i-1][j-k] for k in [1...f]. Note that dp[0][0] should be 1.|https://leetcode.com/problems/number-of-dice-rolls-with-target-sum/description/|
|265. Paint House II|Hard|Simple DP. We can optimize it to Onk and O1 space by finding the minimum 2 items of each level while traversing.|https://leetcode.com/problems/paint-house-ii/description/|

## Design Datastructre
|Name|difficulty|Solution|Link|
|:--:|:--:|:--:|:--:|
|641. Design Circular Deque| Medium | Use a doubly linkedlist| https://leetcode.com/problems/design-circular-deque/description/ |
|146. LRU Cache|Medium|HashMap + Double Linkedlist|https://leetcode.com/problems/lru-cache/description/|
|460. LFU Cache|Hard|HashMap + LinkedHashSet. Use a map to store key to val, a map to store key to freq, a map to store freq to list of keys. Linked hash set can keep the keys in order and have a O1 insert and delete|https://leetcode.com/problems/lfu-cache/description/|
|381. Insert Delete GetRandom O(1) - Duplicates allowed|Hard|TODO: implement it with LinkedHashSet. Use HashMap + array. Hashmap stores the value and its index in the array. Array stores the value and its relative index in the hashmap|https://leetcode.com/problems/insert-delete-getrandom-o1-duplicates-allowed/description/|

## Sliding Window
|Name|difficulty|Solution|Link|
|:--:|:--:|:--:|:--:|
|713. Subarray Product Less Than K| Medium|Use a sliding window which product is less than k, and add the size of window to res|https://leetcode.com/problems/subarray-product-less-than-k/description/|
|1151. Minimum Swaps to Group All 1's Together|Medium|maintain a window which size is the same as total number of 1s in the array, in which have as many 1s as possible|https://leetcode.com/contest/biweekly-contest-6/problems/minimum-swaps-to-group-all-1s-together/|
|683. K Empty Slots|Hard|First record which bulb is turned on on each day, then try to find an subarray such that we have k+2 items in the subarray, and the items on both ends should be smaller than that in the middle. Then we try to find this window from left to right.|https://leetcode.com/problems/k-empty-slots/description/|

## Tree
|Name|difficulty|Solution|Link|
|:--:|:--:|:--:|:--:|
|663. Equal Tree Partition| Medium |Store the sum of every subtree and check if totalSum/2 in these subtrees| https://leetcode.com/problems/equal-tree-partition/description/|
|662. Maximum Width of Binary Tree| Medium | Change the val of the nodes to the corresponding index in a full binary tree, then do a level order traversal, track the largest distance| https://leetcode.com/problems/maximum-width-of-binary-tree/description/|
|652. Find Duplicate Subtrees| Medium|Encode the tree and track the appearance of all encoded strings|https://leetcode.com/problems/find-duplicate-subtrees/description/|
|549. Binary Tree Longest Consecutive Sequence II|Medium|helper gets a node and return the longest inc num and decnum. For each node, compare to its left and right, find current lonest inc num and dec num, then update the res with curInc + curDec - 1|https://leetcode.com/problems/binary-tree-longest-consecutive-sequence-ii/description/|
|515. Find Largest Value in Each Tree Row|Medium|Recursion: check the depth and the size of the res to see if we find the first node in the level. Non-recursion: simple level order traversal|https://leetcode.com/problems/find-largest-value-in-each-tree-row/description/|
|968. Binary Tree Cameras|Hard|0 for camera, 1 for need to be covered, 2 for doesn't need to be covered, do a DFS on the root. Finally check if the root itself needs to be covered by a virtual parent.|https://leetcode.com/problems/binary-tree-cameras/description/|
|545. Boundary of Binary Tree|Medium|First add the root -> add the left bound -> add the leaves of left subtree -> add the leaves of right subtree -> add the right bound reversely(postorder)|https://leetcode.com/problems/boundary-of-binary-tree/description/|
|222. Count Complete Tree Nodes|Medium|A regular tree question. Use the full binary tree characteristic. Check the right and left height and one of them must be a full binary tree, and use the formula will do.|https://leetcode.com/problems/count-complete-tree-nodes/description/|
|1161. Maximum Level Sum of a Binary Tree|Medium|level order/DFS level sum|https://leetcode.com/contest/weekly-contest-150/problems/maximum-level-sum-of-a-binary-tree/|
|428. Serialize and Deserialize N-ary Tree|Hard|Record the size of the subtree and Preorder traversal. |https://leetcode.com/problems/serialize-and-deserialize-n-ary-tree/description/|


## Graph
|Name|difficulty|Solution|Link|
|:--:|:--:|:--:|:--:|
|1135. Connecting Cities With Minimum Cost|Medium|TODO|https://leetcode.com/contest/biweekly-contest-5/problems/connecting-cities-with-minimum-cost/|
|417. Pacific Atlantic Water Flow|Medium|BFS/DFS from pacific and atlantic backwards. Search those points can reach both pacific and atlantic.|https://leetcode.com/problems/pacific-atlantic-water-flow/description/|
|505. The Maze II|Hard|BFS and record the min distance to each reachable point, return the distance to targete point|https://leetcode.com/problems/the-maze-ii/description/|
|834. Sum of Distances in Tree|Hard|First use a dfs(preorder) to build the count[] counting the number of nodes of each subtree. Then we use another dfs(postorder) to build the dist[]. dist[child] = dist[parent] - count[child] + N - count[child]. This means, from parent to child, we have counts[child] of nodes get 1 distance nearer, and N - counts[child] of nodes get 1 distance further.|https://leetcode.com/contest/weekly-contest-84/problems/sum-of-distances-in-tree/|
|1168. Optimize Water Distribution in a Village|Hard|The key is to build a MST among all pipes and a dummy node that connects all other nodes with cost of building wells. Practice for Kruskal and Prim|https://leetcode.com/contest/biweekly-contest-7/problems/optimize-water-distribution-in-a-village/|

## UnionFind
|Name|difficulty|Solution|Link|
|:--:|:--:|:--:|:--:|
|1135. Connecting Cities With Minimum Cost|Medium|TODO|https://leetcode.com/contest/biweekly-contest-5/problems/connecting-cities-with-minimum-cost/|

## SubMatrix
> For this type of question, always try to reduce the time complexity to n^3. Try to fix an edge/point and search other points.

|Name|difficulty|Solution|Link|
|:--:|:--:|:--:|:--:|
|1139. Largest 1-Bordered Square| Medium|Search all possible r for the square(big->small) and all possible root point, check if all 4 edges are 1s. Optimize it with helper matrix that tells how many consecutive 1s to the left/top of the current pos.|https://leetcode.com/problems/largest-1-bordered-square/description/|
|764. Largest Plus Sign|Medium|track the minimum distance that a pos can strech. then return the max pos.|https://leetcode.com/problems/largest-plus-sign/description/|

## String Parsing
|Name|difficulty|Solution|Link|
|:--:|:--:|:--:|:--:|
|640. Solve the Equation|Medium|Split the string with left and right. and then count the res of ax+b = cx+d. regex "(?=[+-])" means we want to match + or -a, but not including the sign into the split.|https://leetcode.com/problems/solve-the-equation/description/|
|385. Mini Parser|Medium|Use stack to record each level of [], always operate on the latest level. Note that we need a basic level(stack = [NestedInteger()]) for return value here.|https://leetcode.com/problems/mini-parser/description/|
|224. Basic Calculator|Hard|Store the result by level. Here we also need to store the sign of each level by pushing num first then sign. So when we push, we get the sign first, apply on the cur level, and add to previous level.|https://leetcode.com/problems/basic-calculator/description/|
|726. Number of Atoms|Hard|Same as calculator. Store each level in the stack and merge the result to last level when we have ')'.|https://leetcode.com/problems/number-of-atoms/description/|
|68. Text Justification|Hard|Similar to round robin, Calculate the num of space first, then use modular to pad space to each word one by one until finish.|https://leetcode.com/problems/text-justification/description/|
|1106. Parsing A Boolean Expression|Hard|Use 2 stacks to store operands and operators|https://leetcode.com/problems/parsing-a-boolean-expression/description/|
|150. Evaluate Reverse Polish Notation|Medium|Need to pay attention on the floor division problem and take care of the sign.|https://leetcode.com/problems/evaluate-reverse-polish-notation/description/|
|394. Decode String|Medium|String parsing practice.|https://leetcode.com/problems/decode-string/description/|

## HashMap
|Name|difficulty|Solution|Link|
|:--:|:--:|:--:|:--:|
|525. Contiguous Array|Medium|replace the 0 to -1, then we do the same thing as max subarray with sum k(k=0). We store the sum with the index, and if curSum already in the map, it means current interval is 0-1 balanced, we update the res. Otherwise, we update the map.|https://leetcode.com/problems/contiguous-array/description/|
|554. Brick Wall|Medium|count the pos of all brick edges in map, and return the num of walls - edge with most appearance|https://leetcode.com/problems/brick-wall/description/|

## Substring/Subsequence/SubArray
|Name|difficulty|Solution|Link|
|:--:|:--:|:--:|:--:|
|395. Longest Substring with At Least K Repeating Characters|Medium|Searching from substring containing only 1 unique letter to 26 of them. Maintain a window using 2 pointers with certain unique letters, and check if this window is a valid window. The reason why window works here is we are dealing with substring, which is continuous.|https://leetcode.com/problems/longest-substring-with-at-least-k-repeating-characters/description/|
|862. Shortest Subarray with Sum at Least K|Hard|Same idea. Use deque as a sliding window and keep the sum >= k. Use a prefix array and increasing monotonic stack to help control the sum calculation and size control.|https://leetcode.com/problems/shortest-subarray-with-sum-at-least-k/|

## Trie
|Name|difficulty|Solution|Link|
|:--:|:--:|:--:|:--:|
|212. Word Search II|Hard|Classic Trie problem. Build Trie with all words and search each grid using backtrack.|https://leetcode.com/problems/word-search-ii/description/|
|1166. Design File System|Medium|Practice for Trie Tree|https://leetcode.com/contest/biweekly-contest-7/problems/design-file-system/|

## Math
|Name|difficulty|Solution|Link|
|:--:|:--:|:--:|:--:|
|204. Count Primes|Easy|Use Sieve of Eratosthenes, loop all n and try to get rid of all composites of every prime|https://leetcode.com/problems/count-primes/description/|
|296. Best Meeting Point|Hard|Find the median of all houses.`Proof: totalX = |x1 - m| + |x2-m| + ... + |xn-m|. `Derivative of totalX = -1 + 1 + -1 + ... Since we want the derivative to be 0, thus, the number of -1 and 1 should equal. Thus we should have half of the xn smaller than m and half bigger, which is median. Same idea with the totalY.|https://leetcode.com/problems/best-meeting-point/description/|
|264. Ugly Number II|Medium|Generate `1*2, 1*3, 1*5...` by multiplying 2, 3, 5 to current minimum ugly number. We set up 3 pointers that can generate next `*2, *3, *5`ugly number, and keep track of them until we generate n number.|https://leetcode.com/problems/ugly-number-ii/description/d|

## Stack
|Name|difficulty|Solution|Link|
|:--:|:--:|:--:|:--:|
|946. Validate Stack Sequences|Medium|simulate the process of stack operation. First push, then check if we shoud pop anything at this moment. Then check the final result|https://leetcode.com/problems/validate-stack-sequences/description/|
|1003. Check If Word Is Valid After Substitutions|Medium|Reconstruct this string. the first c we met has to be the last abc we insert, thus previous 2 chars have to be a and b. Check this continously until the stack is empty|https://leetcode.com/problems/check-if-word-is-valid-after-substitutions/description/|

## Segmant Tree
|Name|difficulty|Solution|Link|
|:--:|:--:|:--:|:--:|
|1157. Online Majority Element In Subarray|Hard|TODO|https://leetcode.com/problems/online-majority-element-in-subarray/discuss/356227/C++-Codes-of-different-approaches-(Random-Pick-Trade-off-Segment-Tree-Bucket)|

## Random
|Name|difficulty|Solution|Link|
|:--:|:--:|:--:|:--:|
|1157. Online Majority Element In Subarray|Hard|Every time i pick a random element between bounds, And check to see if it's a majority item by binary search its left and right pos. right_pos - left_pos is the number of this element, and we check it with threshold. |https://leetcode.com/problems/online-majority-element-in-subarray/discuss/356227/C++-Codes-of-different-approaches-(Random-Pick-Trade-off-Segment-Tree-Bucket)|

## Backtrack
|Name|difficulty|Solution|Link|
|:--:|:--:|:--:|:--:|
|291. Word Pattern II|Hard|For each pattern char, search the following source to find a match, search deeper and backtrack.|https://leetcode.com/problems/word-pattern-ii/description/|

## Bucket Sort
|Name|difficulty|Solution|Link|
|:--:|:--:|:--:|:--:|
|274. H-Index|Medium|Use a bucket to store the number of citations of each paper. If exceeds, merge the result to nth paper. Then check backwards, try to find a point where the total count > ith paper. That point is that at this point, we have this amount of citations (total count), that have at least this many citations(ith paper)|https://leetcode.com/problems/h-index/description/|