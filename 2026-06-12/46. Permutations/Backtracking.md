### Approach

Since we need to generate all possible arrangements of the given numbers, I use backtracking to build each permutation one element at a time. At every step, I try choosing a number that has not already been used in the current permutation.

I keep track of the numbers that are already included using a used array. If a number has already been used, I skip it. Otherwise, I add it to the current permutation, mark it as used, and recursively continue building the permutation.

Once the size of the current permutation becomes equal to the size of the input array, it means I have formed a complete permutation, so I add it to the result. After exploring that path, I remove the last added number and mark it as unused so that it can be used in other permutations. This choose, explore, and undo process helps generate all possible permutations.

---

### Solution


class Solution {
public:
    vector<vector<int>> result;

    void backtrack(vector<int>& nums,
                   vector<int>& permutation,
                   vector<bool>& used) {

        if (permutation.size() == nums.size()) {
            result.push_back(permutation);
            return;
        }

        for (int i = 0; i < nums.size(); i++) {

            if (used[i]) {
                continue;
            }

            permutation.push_back(nums[i]);
            used[i] = true;

            backtrack(nums, permutation, used);

            permutation.pop_back();
            used[i] = false;
        }
    }

    vector<vector<int>> permute(vector<int>& nums) {

        vector<int> permutation;
        vector<bool> used(nums.size(), false);

        backtrack(nums, permutation, used);

        return result;
    }
};


### Complexity

Time Complexity: O(n × n!)
There are n! possible permutations, and copying each complete permutation into the result takes O(n) time.

Space Complexity: O(n)
The recursion stack, current permutation, and used array can each grow up to size n. The output space is not included in the auxiliary space calculation.

