#### Container-With-Most-Water 盛更多水的容器

##### 题目描述
```
给你 n 个非负整数 a1，a2，...，an，每个数代表坐标中的一个点 (i, ai) 。在坐标内画 n 条垂直线，垂直线 i 的两个端点分别为 (i, ai) 和 (i, 0)。 
找出其中的两条线，使得它们与 x 轴共同构成的容器可以容纳最多的水。 

说明：你不能倾斜容器，且 n 的值至少为 2。 

```
![](../images/question_11.jpg) 
```
Input: height = [1,8,6,2,5,4,8,3,7]
Output: 49
Explanation: 图中垂直线代表输入数组 [1,8,6,2,5,4,8,3,7]。在此情况下，容器能够容纳水（表示为蓝色部分）的最大值为 49。
```
##### 思路
> 1. 暴力遍历  
用两层for循环遍历每一个柱子，找到两个柱子最小的那根柱子乘上其对应的索引的差(right - left)得到每一次的面积(area)，只要依次对比area得到最大的面积即可  
> 2. 左右指针  
左右指针分别位于容器壁两端通过移动左指针或者右指针更新area最大值，如果左指针对应的柱子比右指针对应的柱子小,则左指针向后移动一位且更新area，如果右指针所对应的柱子小于左指针所对应的柱子,那么右指针向后移动一位，并且更新area,直到左指针和右指针相等结束，返回已经记录的area的最大的那个值

##### 代码
###### 暴力
```Java
class Solution {
  public int maxArea(int[] arr) {
    int max = 0;
    for(int i = 0; i < arr.length - 1; i++) {
      for(int j = i + 1; j < arr.length; j++) {
        int area = (j - i) * Math.min(arr[i], arr[j]);
        max = Math.max(max, area);
      }
    }
    return max;
  }
}
//时间复杂度O(n²)
```
###### 左右指针
```Java
class Solution {
  public int maxArea(int[] arr) {
    int max = 0;
    for(int i = 0, j = arr.length - 1; i < j;) {
      int minHeight = arr[i] < arr[j] ? arr[i++] : arr[j--];
      int area = (j - i + 1) * minHeight;
      max = Math.max(max, area);
    }
    return max;
  }
}
//时间复杂度O(n)
//空间复杂度 O(1)O(1)，指针使用常数额外空间。
```
 
