```java
/* 
在一个array里找size为k的subarray，subarray里的element不能重复，问subarray中sum的max是多少
*/

public class Main {
    /*
    Algo: Sliding Window
    Time complexity: O(n), traverse all elements in the array.
    Space complexity: O(k), the size of window is k.
    */
    public static long findMax(int[] arr, int k) {
        Set<Integer> set = new HashSet<>();
        long res = Integer.MIN_VALUE, sum = 0;
        for (int l = 0, r = 0; r < arr.length; r++) {
            sum += arr[r];
            while (set.contains(arr[r])) {  // judge the duplicate
                sum -= arr[l];
                set.remove(arr[l++]);
            }
            set.add(arr[r]);
            while (set.size() > k) {    // judge the size of the window
                sum -= arr[l];
                set.remove(arr[l++]);
            }
            if (r-l+1 == k)         // satisfy the size k
                res = Math.max(res, sum);   
        }
        return res == Integer.MIN_VALUE ? -1 : res;
    }
    public static void main(String[] args) {
        int[] arr1 = new int[]{0,0,0,0};
        int[] arr2 = new int[]{-1000000000, -1000000001};
        int[] arr3 = new int[]{1,2,3,4,3,5,6};
        int[] arr4 = new int[]{2,4};
        System.out.println(findMax(arr1, 3));
        System.out.println(findMax(arr2, 2));
        System.out.println(findMax(arr3, 4));
        System.out.println(findMax(arr4, 3));
    }
}
```







