# problem
给定一个字符串，请你找出其中不含有重复字符的 最长子串 的长度。

示例 1:

输入: "abcabcbb"
输出: 3 
解释: 因为无重复字符的最长子串是 "abc"，所以其长度为 3。
示例 2:

输入: "bbbbb"
输出: 1
解释: 因为无重复字符的最长子串是 "b"，所以其长度为 1。
示例 3:

输入: "pwwkew"
输出: 3
解释: 因为无重复字符的最长子串是 "wke"，所以其长度为 3。
     请注意，你的答案必须是 子串 的长度，"pwke" 是一个子序列，不是子串。
# solution
```javascript

/**
 * @param {string} s
 * @return {number}
 */
// 暴力解法超时
// var lengthOfLongestSubstring = function(s) {
//     let length=s.length;
//     let ans=0;
//     for(let i = 0;i<length;i++){
//         for(let j = i+1;j<length+1;j++){
//             let str = s.slice(i,j)
//             let set = new Set()
//             for(let k=0;k<str.length;k++){
//                 if(set.has(str[k])){
//                     break;
//                 }else{
//                     set.add(str[k])
//                     if(k == str.length-1){
//                         ans = Math.max(ans,str.length)
//                     }
//                 }
//             }
//         }
//     }
//     return ans
// };
/**
 * @param {string} s
 * @return {number}
 */
var lengthOfLongestSubstring = function(s) {
  let n = s.length;
  let i = 0,
    j = 0,
    ans = 0;
  let strSet = new Set();
  while (i < n && j < n) {
    if (!strSet.has(s[j])) {
      strSet.add(s[j++]);
      ans = Math.max(ans, j - i);
    } else {
      strSet.delete(s[i++]);
    }
  }
  return ans;
};
```
# complexity
time complexity: O(max(m,n))

space complexity: O(max(m,n))
