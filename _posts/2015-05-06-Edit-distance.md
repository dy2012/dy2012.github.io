---
layout: post

title:  Edit Distance 

tags: [算法]

---
**Edit Distance：Given two words word1 and word2, find the minimum number of steps required to convert word1 to word2. (each operation is counted as 1 step.)**
**You have the following 3 operations permitted on a word:**

* **a) Insert a character**
* **b) Delete a character**
* **c) Replace a character**


&emsp;&emsp;Edit Distance 是leetcode上的一道动态规划方面的题。通过增加，减少或替换来使两个不同的字符串变得相同，计算其最少的操作次数。编程之美上有道相同的题，计算字符串的相似度，书中给了递归的解决方法，但是时间复杂度是O(N!)，通过书中的递归树可以看到，有子问题被重复计算了，需要将子问题计算后的解存储起来。算法分析在编程之美上都有，唯一需要做的就是设置一个数组记录。

设distance[row][col]
有三种情况:

* 1）将word1的前i-1个字符变成word2的前j-1个字符，再把word1的第i个字符修改为word2的第j个字符，即distance[i-1][j-1]＋１
* 2）将word1的前i个字符变成word2的前j-1个字符，再加上word2的第j个字符，即distance[i][j-1] + 1
* 3）删除word1的第i个字符，将word1的前i-1个字符变成word2的第j个字符，即dp[i-1][j] + 1

则distance[i][j]是三种情况的最小值。

    distance[i][j] = min(distance[i-1][j-1], min(distance[i][j-1],distance[i-1][j])) + 1

空间复杂度是O(M*N)，应该还可以减少，用一个vector，O（max(M,N))。
 

{% highlight c++ linenos %}
class Solution {
 public:
  int minDistance(string word1, string word2) {
    int m = word1.length();
    int n = word2.length();
    if(m == 0 || n == 0) {
      return m == 0 ? m : n;
    }

    vector<vector<int>> distance(m + 1, vector<int>(n + 1));
    distance[0][0] = 0;
    for(int i = 0; i <= m; ++i) {
      distance[i][0] = i;
    }

    for(int j = 0; j <= n; ++j) {
      distance[0][j] = j;
    }

    for(int i = 0; i <= m; ++i) {
      for(int j = 0; j <= n; ++j) {
        if(word1[i-1] == word2[j-1]) {
          distance[i][j] = distance[i-1][j-1];
        } else {
          distance[i][j] = min(distance[i-1][j-1],
                               min(distance[i-1][j],
                                   distance[i][j-1])) + 1;
        }
      }
    }
    return distance[m][n];
  }
};
{% endhighlight %}
