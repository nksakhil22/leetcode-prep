Approach: I start with the empty subset because every set always has an empty subset. Then, for each number in the input array, I iterate through all the subsets that have already been generated. For every existing subset, I create a new copy, add the current number to it, and store it back in the result. This way, each number gets a chance to be included in every previously formed subset. As I process more elements, the number of subsets keeps doubling, and by the end, I have generated all possible subsets of the given array.


Solution:
class Solution {
public:
    vector<vector<int>> subsets(vector<int>& nums) {

        vector<vector<int>> result;

        result.push_back({});

        for (int num : nums) {

            int size = result.size();

            for (int i = 0; i < size; i++) {

                vector<int> subset = result[i];

                subset.push_back(num);

                result.push_back(subset);
            }
        }

        return result;
    }
};

### Complexity
Time Complexity: O(n × 2ⁿ)
  There are a total of 2ⁿ subsets, and for each element, we iterate through all previously generated subsets and create copies of them. Since copying a subset can take up to `O(n)` time in the worst case, the overall time complexity becomes `O(n × 2ⁿ)`.

Space Complexity: O(n × 2ⁿ)
  The result stores all 2ⁿ subsets, and each subset can contain up to `n` elements, so the total space required to store the output is O(n × 2ⁿ).

:
