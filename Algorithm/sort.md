## Bubble Sort

2750번 - 수 정렬하기

https://www.acmicpc.net/problem/2750



처음에는 arraylist를 사용했는데 시간도 많이걸리고 메모리도 많이 잡아먹어서 array로 변경.

```java
import java.util.Scanner;

public class BubbleSort {

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int count = sc.nextInt();
        int[] nums = new int[count];

        for(int i=0; i< count; i++){
            nums[i] += sc.nextInt();
        }

        bubbleSort(nums);
        for (int n : nums) {
            System.out.println(n);
        }
    }

    public static void bubbleSort(int[] nums) {
        int tmp;
        boolean checker = true;

        for(int j = nums.length; j > 1 ; j--){
            for(int k = 0; k < j-1; k++) {
                if (nums[k] > nums[k+1]) {
                    tmp = nums[k];
                    nums[k] = nums[k+1];
                    nums[k+1] = tmp;
                    checker = false;

                }
            }
            if (checker) {
                return ;
            }
        }
    }
}


```



## Heap Sort

2751번 - 수 정렬하기2

https://www.acmicpc.net/problem/2751

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class HeapSort {

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int count = Integer.parseInt(br.readLine());
        int[] nums = new int[count];

        for(int i=0; i< count; i++){
            nums[i] = Integer.parseInt(br.readLine());
        }
        heapSort(nums, count);

    }

    public static void heapSort(int[] nums, int n) {
        buildMinHeap(nums, n-1);

        while (n > 0) {
            int tmp;
            tmp = nums[0];
            nums[0] = nums[n-1];
            System.out.println(tmp);
            n--;
            minHeapify(nums, 0, n);
        }
    }

    public static void buildMinHeap(int[] nums, int n) {
        for (int i = n/2; i >= 0; i--) {
            minHeapify(nums, i, n);
        }
    }

    public static void minHeapify(int[] nums, int idx, int n) {
        int left = idx*2;
        int right = (idx*2)+1;
        int smaller;
        int tmp;

        if (right <= n) {
            if (nums[left] < nums[right]) {
                smaller = left;
            } else {
                smaller = right;
            }
        } else if (left <= n) {
            smaller = left;
        } else {
            return ;
        }
        if (nums[smaller] < nums[idx]) {
            tmp = nums[idx];

            nums[idx] = nums[smaller];
            nums[smaller] = tmp;

            minHeapify(nums, smaller, n);
        }
    }
}


```



## Merge Sort

1427번 - 소트 인사이드

https://www.acmicpc.net/problem/1427

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Scanner;

public class SortInside {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String line1 = br.readLine();

        int arr[] = new int[line1.length()];
        for (int i = 0; i < line1.length(); i++) {
            arr[i] = Integer.parseInt(line1.substring(i,i+1));
        }
        mergeSort(arr, 0, arr.length-1);

        for (int aa: arr
             ) {
            System.out.print(aa);
        }
    }

    private static void mergeSort(int[] arr, int s, int e) {
        if (s < e) {
            int m = (s+e)/2;
            mergeSort(arr, s, m);
            mergeSort(arr, m+1, e);
            merge(arr, s, m, e);
        }

    }
    private static void merge(int[] arr, int s, int m, int e) { // p q r
        int p = s;
        int q = m+1;
        int t = s;
        int tmp[] = new int[arr.length];

        while(p <= m && q <= e) {
            if (arr[p] > arr[q]) {
                tmp[t++] = arr[p++];
            }
            else {
                tmp[t++] = arr[q++];
            }
        }

        while(p <=m) {
            tmp[t++]= arr[p++];
        }

        while(q <=e) {
            tmp[t++]=arr[q++];
        }

        for (int i = s; i < t; i++) {
            arr[i] = tmp[i];
        }

    }

}
```

