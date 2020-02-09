# 467-环绕字符串中唯一的子字符串

```c++
把字符串 s 看作是“abcdefghijklmnopqrstuvwxyz”的无限环绕字符串，所以 s 看起来是这样的："...zabcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyzabcd....". 

现在我们有了另一个字符串 p 。你需要的是找出 s 中有多少个唯一的 p 的非空子串，尤其是当你的输入是字符串 p ，你需要输出字符串 s 中 p 的不同的非空子串的数目。 

注意: p 仅由小写的英文字母组成，p 的大小可能超过 10000。

 

示例 1:

输入: "a"
输出: 1
解释: 字符串 S 中只有一个"a"子字符。
 

示例 2:

输入: "cac"
输出: 2
解释: 字符串 S 中的字符串“cac”只有两个子串“a”、“c”。.
 

示例 3:

输入: "zab"
输出: 6
解释: 在字符串 S 中有六个子串“z”、“a”、“b”、“za”、“ab”、“zab”。.

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/unique-substrings-in-wraparound-string
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

---

为了去掉重复的短序列的情况，我们以一个序列最后一个出现的字符为准，统计以每个字符作为结尾的最长连续序列长度。

最后将长度累加（26个不同的长度）就是答案

例如:abcd, 对于以d结尾的最长的序列是abcd,长度为4，代表了（abcd,bcd,cd，d 四个）同理以c结尾的最长为abc，长度为3

总结果就是4+3+2+1 = 10

```c++
class Solution {
public:
    int findSubstringInWraproundString(string p) {
        int len = p.size();
        if(len == 0)
            return 0;
        int ans =0;
        int dp[26] = {0};
        int count = 0;
        for(int i=0;i<len;i++){
            if( i >0 && (p[i-1] + 1 == p[i] || p[i-1] -p[i] == 25) )
                count++;
            else
                count =1;
            dp[p[i] -'a'] = max(dp[p[i] -'a'] ,count);
        }
        
        for(int t :dp){
            ans+=t;
        }
        return ans;
    }
};
```

---



