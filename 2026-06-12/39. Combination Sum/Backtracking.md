### Approach

Since we need to find all combinations whose sum equals the target, I use backtracking to explore every possible combination. At each step, I try adding one of the candidate numbers to the current combination and reduce the remaining target accordingly.

If the remaining target becomes 0, it means I have found a valid combination, so I add it to the result. If the remaining target becomes negative, I stop exploring that path because it can no longer produce a valid answer.

Since a candidate can be used multiple times, when I choose a number, I continue the recursive call from the same index instead of moving to the next one. This allows the same number to be picked again. After exploring a path, I remove the last added number and try the next candidate. This choose, explore, and undo process helps generate all valid combinations without missing any possibilities.

---

### Solution

class Solution {
public:
    vector<vector<int>> result;

    void backtrack(vector<int>& candidates, int target,
                   int start, vector<int>& combination) {

        if (target == 0) {
            result.push_back(combination);
            return;
        }

        if (target < 0) {
            return;
        }

        for (int i = start; i < candidates.size(); i++) {

            combination.push_back(candidates[i]);

            backtrack(candidates,
                      target - candidates[i],
                      i,
                      combination);

            combination.pop_back();
        }
    }

    vector<vector<int>> combinationSum(vector<int>& candidates, int target) {

        vector<int> combination;

        backtrack(candidates, target, 0, combination);

        return result;
    }
};


### Complexity

Time Complexity: O(N^(T/M))

Where:

N = number of candidates
T = target value
M = smallest candidate value

In the worst case, the recursion tree can have a branching factor of N, and the maximum depth can be approximately T/M.

Space Complexity: O(T/M)

The recursion depth can go up to T/M when repeatedly choosing the smallest candidate. The output space is not included in the auxiliary space calculation.
