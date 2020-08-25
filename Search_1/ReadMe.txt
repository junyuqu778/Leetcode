考虑的基本数据结构
第一类： 查找有无--set
元素'a'是否存在，通常用set：集合
set只存储键，而不需要对应其相应的值。
set中的键不允许重复
第二类： 查找对应关系(键值对应)--dict
元素'a'出现了几次：dict-->字典
dict中的键不允许重复
第三类： 改变映射关系--map
通过将原有序列的关系映射统一表示为其他



二分查找又称折半查找，对排好序的数组，每次取这个数和数组中间的数进行比较，复杂度是O(logn)如:设数组为a[n],查找的数x,

如果x==a[n/2]，则返回n/2;

如果x < a[n/2]，则在a[0]到a[n/2-1]中进行查找；

如果x > a[n/2]，则在a[n/2+1]到a[n-1]中进行查找；

优点是比较次数少，查找速度快，平均性能好；其缺点是要求待查表为有序表，且插入删除困难。

条件：查找的数组必须要为有序数组。

 

二种实现方式
 

1.递归
/*
归的二分查找
arrat：数组 ， low:上界；  high:下界;  target:查找的数据； 返回target所在数组的下标 
*/
int binarySearch(int array[], int low, int high, int target) {
	int middle = (low + high)/2;
	if(low > high) {
		return -1;
	}
	if(target == array[middle]) {
		return middle;
	}
	if(target < array[middle]) {
		return binarySearch(array, low, middle-1, target);
	}
	if(target > array[middle]) {
		return binarySearch(array, middle+1, high, target);
	} 
}


2.非递归（循环）
/*
非递归的二分查找 
arrat：数组 ， n:数组的大小;  target:查找的数据； 返回target所在数组的下标 
*/
int binarySearch2(int array[], int n, int target) {
	int low = 0, high = n, middle = 0;
	while(low < high) {
		middle = (low + high)/2;
		if(target == array[middle]) {
			return middle;
		} else if(target < array[middle]) {
			high = middle;
		} else if(target > array[middle]) {
			low = middle + 1;
		}
	}
	return -1;
}


推荐使用非递归的方式，因为递归每次调用递归时有用堆栈保存函数数据和结果。能用循环的尽量不用递归。