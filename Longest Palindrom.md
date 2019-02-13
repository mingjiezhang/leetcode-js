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
## a.动态规划
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
```
### b.中心扩展法
```javascript
/**
 * @param {string} s
 * @return {string}
 */
var longestPalindrome = function(s) {
  if (s.length < 2) {
    return s;
  }
  let start = 0,
    end = 0;
  for (let i = 0; i < s.length; i++) {
    let len1 = singlePalindrome(s, i, i);
    let len2 = singlePalindrome(s, i, i + 1);
    let maxLen = Math.max(len1, len2);
    if (maxLen > end - start) {
      //偶数:(max-2)/2,奇数:(max-1)/2
      start = i - (maxLen % 2 === 0 ? (maxLen - 2) / 2 : (maxLen - 1) / 2);
      end = start + maxLen - 1;
    }
  }
  return s.slice(start, end + 1);
};

function singlePalindrome(s, start, end) {
  let L = start,
    R = end;
  while (L >= 0 && R < s.length && s[L] == s[R]) {
    L--;
    R++;
  }
  //2两种情况，a.为i,i多加的一次，b.为i,i+1初次出错也为2，后续多加一次也为2
  //R-L+1-2
  return R - L - 1;
}
```
# complexity
time complexity: O(n^2)

space complexity: a: O(n^2); b: O(n^2)
