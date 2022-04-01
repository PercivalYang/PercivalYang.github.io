## 概念

- ***O(1)***：该算法步数恒定，不随数组变化而变化；
- ***O(N)***：该算法步数与数组元素个数成正比；
- ***O(log N)***：典型例子：二分查找；
- ***O($N^2$)***：典型例子：循环嵌套；

## 实例

1. 解决嵌套循环的***$O(N^2)$***时间复杂度的问题——**线性解决**

```java
function hasDuplicateValue(array) { 
 var existingNumbers = []; 
 for(var i = 0; i < array.length; i++) { 
 	if(existingNumbers[array[i]] == undefined) { 
 		existingNumbers[array[i]] = 1; 
	 } else { 
 		return true; 
 	} 
 } 
 return false; 
}
```

- 上述方法存在**空间**上的缺点(新建了一个`existingNumbers`数组)，待改进。