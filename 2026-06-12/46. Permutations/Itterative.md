### Approach

I start with a single empty permutation. Then, for each number in the input array, I take all the permutations generated so far and insert the current number into every possible position within each permutation.

For every existing permutation, inserting the current number at all valid positions creates a new set of permutations. These newly generated permutations are collected and used as the input for the next iteration.

As I process more numbers, the number of permutations keeps growing until every number has been placed in every possible position. By the end, I have generated all possible permutations of the given array without using recursion or backtracking.

---

### Solution

class Solution {
public:
    vector<vector<int>> permute(vector<int>& nums) {

        vector<vector<int>> result = {{}};

        for (int num : nums) {

            vector<vector<int>> newResult;

            for (auto permutation : result) {

                for (int pos = 0; pos <= permutation.size(); pos++) {

                    vector<int> newPermutation = permutation;

                    newPermutation.insert(
                        newPermutation.begin() + pos,
                        num
                    );

                    newResult.push_back(newPermutation);
                }
            }

            result = newResult;
        }

        return result;
    }
};


### Complexity

Time Complexity: O(n × n!)
There are n! possible permutations, and creating each permutation requires copying up to n elements.

Space Complexity: O(n × n!)
The result stores all n! permutations, and each permutation can contain up to n elements.
