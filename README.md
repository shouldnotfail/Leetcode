# Leetcode


## 2020/5/16 第一天开始

167. Twosum
大家看起来都不用迭代器进行解答,使用int类型变量作为容器的指针
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

663. judgeSquareSum

leetcode会验证程序是否溢出，所以需要注意合理的表达算式
```c++
class Solution {
public:
    bool judgeSquareSum(int c) {
        int low = 0,high = sqrt(c);
        while (low<=high){
            if(low*low==c-high*high)   //溢出可能
                return true;
            else if  (low*low<c-high*high)  //溢出可能
                low++;
            else
                high--;

        }
        return false;
    }
};
```


680.validPalindrome

只做一次修改，但是必须遍历整个字符串才能验证是否正确，在字符串中的“=”一定要思考实际意义，另外注意配合continue,break实现逻辑。

```c++
class Solution {
public:

    bool validPalindrome(string s) {
        string::size_type i=0, j = s.size()-1;
        bool l = false;
        bool r = false;
        while(i<=j)
        {
            if(s[i]==s[j]){i++;j--;}

            else
            {
                int i_ = i, j_ = j;
                if(s[i_]!=s[j_-1] && s[i+1]!=s[j])
                    return false;
                if(s[i+1]==s[j]){
                    l=true;
                    i=i+2;
                    j--;
                    while(i<=j)
                    {
                        if(s[i]==s[j]){i++;j--;}
                        else {l=false;
                        break;}
                    }
                }
                if(s[i_]==s[j_-1]){
                    r=true;
                    i_++;
                    j_=j_-2;
                    while(i_<=j_){
                        if(s[i_]==s[j_]){i_++;j_--;}
                        else {r=false;
                        break;}
                    }
                }
                return max(l,r);
            }

        }
        return true;}


};
```


86.merge

最本能的想法是从头排序，为了方式数据丢失重新创建了一个数组
如果从后面开始好像不用创建数组

```c++
class Solution {
public:
    void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) {
        int i = 0, j = 0;
        vector<int> ans;
        if( nums1.size()<nums2.size()) 
        {
            swap(n,m);
            swap(nums1,nums2);
        }
        if (m*n==0)
        {   
            if (m>n);

            else
                nums1=nums2;

        }
        else {
        while(j+i<nums1.size())
        {
            if(nums1[i]>=nums2[j])
            {
                ans.emplace_back(nums2[j]);
                j++;
                if(j>=n)
                {
                    for(i;i<m;i++)
                    ans.emplace_back(nums1[i]);
                }
            }
            else{
                ans.emplace_back(nums1[i]);
                i++;
                if(i>=m)
                {
                    for(j;j<n;j++)
                    ans.emplace_back(nums2[j]);
                }
                }
        }
        nums1=ans;
        }
    }
};


524. findlongestword

这题看了答案写，想用双指针，或许这里不是单纯的双指针了，是两个双指针，导致情况复杂了一点，需要考虑。不过逻辑就是要么查询单词先查询完毕，要么，被查询单词先查询完毕，特殊情况就是指针相等时候，需要继续查询该指针，因为不能确定是否查询完毕，如果是之前的双指针，因为不会涉及重复？无此情况

另外注意逻辑的实现，先实现什么，先break什么，这里先查询字典是否查询完毕，在后来的逻辑中会用到，所以要清楚顺序。
```
```c++
class Solution {
public:
    string findLongestWord(string s, vector<string>& d) {
        int i,j;
        string The_Whole=s;
        string zichuan;
        string better,best="";

        for(i=0;i<d.size();i++){   
            zichuan=d[i];
            int m=0;
            int m_ = zichuan.size()-1;
            int j_ = The_Whole.size()-1;

            for(j=0;j<s.size();){//遍历给定字符串
                if(The_Whole[j]==zichuan[m])
                    m++;
                if(The_Whole[j_]==zichuan[m_])
                    m_--;j++;j_--;
                if(m>=m_){
                if(m==m_){
                    while(j<=j_)
                    {
                        if(The_Whole[j++]==zichuan[m]){
                        better=zichuan;
                        if(better.size()>best.size()||(better.size()==best.size()&&better.compare(best)<0))
                        {best=better;break;}
                    }}}
                else if(m>m_){
                    better=zichuan;
                    if(better.size()>best.size()||(better.size()==best.size()&&better.compare(best)<0))
                        {best=better;break;}
                }break;}
                else if(j>=j_){
                if(j==j_&&m==m_&&The_Whole[j]==zichuan[m])                {
                    better=zichuan;
                    if(better.size()>best.size()||(better.size()==best.size()&&better.compare(best)<0))
                        best=better;
                }else if(j>j_)
                    break;}
            }

        }
        return best;
    }

};
```
