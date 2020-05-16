# Leetcode


## 2020/5/16 第一天开始

167. Twosum
大家看起来都不用迭代器进行解答，有点晚了，下次再看别人怎么解决的
```c++
class Solution {
public:
    vector<int> twoSum(vector<int>& numbers, int target) {
        
        auto end = numbers.end()-1; //尾迭代器指向最后一个元素的下一个元素（0）
        for(auto beg = numbers.begin();beg!=end;)
        {
            auto b = numbers.begin();
            if(*beg+*end<target)
                beg++;
            else if(*beg+*end>target)
                end--;
            else
                return vector<int> {(int)(beg-b+1),(int)(end-b+1)}; //迭代器的差返回的是difference_type
        }
        return {-1,-1};
    }
};
```
