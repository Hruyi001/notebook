
### 318.最大单词长度乘积[****](https://leetcode.cn/problems/maximum-product-of-word-lengths/description/)
```c++
class Solution {
public:
    int maxProduct(vector<string>& words) {
        int n = words.size();
        vector<int> state(n, 0);
        int k = 0;
        // 存储所有单词的26个字母是否出现的二进制
        for(auto word : words) {
            for(auto c : word) {
                state[k] |= 1 << (c - 'a');
            }
            k++;
        }
        int res = 0;
        for(int i = 0; i < n; i++)
        for(int j = i + 1; j < n; j++)
        // 26个字母不匹配
            if((state[i] & state[j]) == 0) {
                res = max(res, (int)(words[i].size() * words[j].size()));
            }
        return res;
    }
};
```

### 319.灯泡开关[**](https://leetcode.cn/problems/bulb-switcher/)
```c++
class Solution {
public:
// 最后亮着的灯是奇数个约数
// 平方数等于奇数个约数
// 平方数的个数是sqrt(n)
    int bulbSwitch(int n) {
      
        return sqrt(n);
    }
};
```
