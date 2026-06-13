### Approach

Since we need to generate all valid combinations of parentheses, I use backtracking to build the string one character at a time.

At each step, I can add an opening parenthesis '(' as long as I have not used all n opening parentheses. I can add a closing parenthesis ')' only if the number of closing parentheses used so far is less than the number of opening parentheses. This ensures that the generated string always remains valid.

Once the length of the current string becomes 2 * n, it means I have used all parentheses and formed a valid combination, so I add it to the result. After exploring a path, I remove the last added parenthesis and try other possibilities. This choose, explore, and undo process helps generate all valid combinations without generating invalid ones.

---

### Solution


class Solution {
public:
    vector<string> result;

    void backtrack(string& current, int open, int close, int n) {

        if (current.size() == 2 * n) {
            result.push_back(current);
            return;
        }

        if (open < n) {
            current.push_back('(');

            backtrack(current, open + 1, close, n);

            current.pop_back();
        }

        if (close < open) {
            current.push_back(')');

            backtrack(current, open, close + 1, n);

            current.pop_back();
        }
    }

    vector<string> generateParenthesis(int n) {

        string current;

        backtrack(current, 0, 0, n);

        return result;
    }
};


### Complexity

Time Complexity: O(4ⁿ)
The number of valid parenthesis combinations grows exponentially as n increases, and we generate each valid combination exactly once.

Space Complexity: O(n)
The recursion stack and the current string can grow up to length 2 * n, so the auxiliary space used is proportional to n.

