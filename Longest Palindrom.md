# problem
给定一个字符串 s，找到 s 中最长的回文子串。你可以假设 s 的最大长度为 1000。

示例 1：

输入: "babad"
输出: "bab"
注意: "aba" 也是一个有效答案。
示例 2：

输入: "cbbd"
输出: "bb"
# solution
a.
```javascript
/**
 * @param {string} s
 * @return {string}
 */
var longestPalindrome = function (s) {
  if (!s.length) {
    return s
  }
  let n = s.length;
  //save palindrome
  let dp = new Array()
  let left = 0, right = 0
  for (let i = n - 2; i >= 0; i--) {
    dp[i] = new Array()
    dp[i][i] = true
    for (j = i + 1; j < n; j++) {
      dp[i][j] = s[i] === s[j] && (j - i < 3 || dp[i + 1][j - 1])
      if (dp[i][j] && right - left < j - i) {
        left = i;
        right = j;
      }
    }
  }
  return s.slice(left, right + 1)
};
b.
```
# complexity
time complexity: O(2n)

space complexity: O(min(m,,n)) 字符串大小:n, 字符集/字母:m。
