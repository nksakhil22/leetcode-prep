Approach: I use backtracking to build subsets step by step. I start with an empty subset and add it to the result first because every set has an empty subset. Then, from the current position, I try adding each remaining number into the current subset. After adding a number, I recursively continue building subsets using only the elements that come after it. Once that recursive path is done, I remove the last added number so I can try a different possibility. This choose, explore, and undo process helps generate all possible subsets without creating duplicates.

Solution:

class Solution {
public:
    vector<vector<int>> result;

    void backtrack(vector<int>& nums, int start, vector<int>& subset) {
        result.push_back(subset);

        for (int i = start; i < nums.size(); i++) {
            subset.push_back(nums[i]);

            backtrack(nums, i + 1, subset);

            subset.pop_back();
        }
    }

    vector<vector<int>> subsets(vector<int>& nums) {
        vector<int> subset;

        backtrack(nums, 0, subset);

        return result;
    }
};


### Complexity

Time Complexity: O(n × 2ⁿ)
There are 2ⁿ total subsets, and copying each subset into the result can take up to `O(n)` time.

Space Complexity: O(n × 2ⁿ)
The result stores all 2ⁿ subsets, and each subset can contain up to `n` elements, so the output space is O(n × 2ⁿ).
