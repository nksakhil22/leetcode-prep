### Approach

I use an iterative BFS-style approach to build valid parenthesis strings step by step. Instead of using recursion, I store each state in a queue. Each state keeps track of the current string, how many opening parentheses have been used, and how many closing parentheses have been used.

At each step, I take one state from the queue and try to add the next valid parenthesis. I can add '(' if I have not used all n opening parentheses yet. I can add ')' only if the number of closing parentheses used is less than the number of opening parentheses used. This keeps every generated string valid.

Once the current string length becomes 2 * n, it means a valid combination is complete, so I add it to the result. By continuing this process until the queue becomes empty, I generate all valid combinations without recursion.

---

### Solution


class Solution {
public:
    vector<string> generateParenthesis(int n) {

        vector<string> result;

        queue<pair<string, pair<int, int>>> q;

        q.push({"", {0, 0}});

        while (!q.empty()) {

            string current = q.front().first;
            int open = q.front().second.first;
            int close = q.front().second.second;

            q.pop();

            if (current.size() == 2 * n) {
                result.push_back(current);
                continue;
            }

            if (open < n) {
                q.push({current + "(", {open + 1, close}});
            }

            if (close < open) {
                q.push({current + ")", {open, close + 1}});
            }
        }

        return result;
    }
};


### Complexity

Time Complexity: O(4ⁿ)
The number of valid parenthesis combinations grows exponentially as `n` increases, and we generate each valid combination once.

Space Complexity: O(4ⁿ)
The queue can store many partial strings at the same time in the worst case.

