# 最长上升子序列问题



## 最长连续递增子序列（递增子数组）的长度

[674. 最长连续递增序列 - 力扣（LeetCode）](https://leetcode.cn/problems/longest-continuous-increasing-subsequence/)

```c++
class Solution {
public:
    int findLengthOfLCIS(vector<int>& nums) {
        //dp[i]  以i结尾的最长连续递增子序列长度
        //dp[i+1]=dp[i]+1  if num[i+1]>nums[i]
        //       =  1    else
        int max_lenth=1;
        int n=nums.size();
        vector<int>dp(n,0);
        dp[0]=1;
        for(int i=1;i<n;i++){
            if(nums[i]>nums[i-1])dp[i]=dp[i-1]+1;
            else dp[i]=1;
            max_lenth=max(max_lenth,dp[i]);
        }
        return max_lenth;

    }
};
```



## 最长递增子序列的长度

[300. 最长递增子序列 - 力扣（LeetCode）](https://leetcode.cn/problems/longest-increasing-subsequence/)

```c++
class Solution {
public:
    int lengthOfLIS(vector<int>& nums) {

        //dp[i] 表示以i结尾的最长严格递增子序列  属性：长度
        //那么  dp[i]=  如果nums[i]>nums[i-1] dp[i-1]+1
        //              否则 nums[i]>nums[j] max{dp[j]+1} j<i-1

        //也就是说 nums[i]>nums[j] max{dp[j]+1} j<i

        int n=nums.size();
        vector<int>dp(n+1,0);
        int res=0;
        for(int i=1;i<=n;i++){
            for(int j=i-1;j>=0;j--){
                if(!j)
                    dp[i]=max(dp[i],1);
                else if(nums[i-1]>nums[j-1])
                    dp[i]=max(dp[i],dp[j]+1);
            }
            res=max(dp[i],res);
        }
        return res;
    }
};
```

