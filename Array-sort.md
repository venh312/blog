## 1차원 배열 정렬
```java
int[] arr = {6,4,4,3,1,2};

Arrays.sort(arr);
```

## 2차원 배열 정렬

### 1. Comparator 익명 클래스 구현
```java
int[][] arr = {{7,40},{5,50},{2,30},{6,20},{3,10}};

Arrays.sort(arr, new Comparator<int[]>() {
    @Override
    public int compare(int[] o1, int[] o2) {
        return o1[0]-o2[0]; // 첫번째 숫자 기준 오름차순
        //return o2[0]-o1[0]; // 첫번째 숫자 기준 내림차순
        //return o1[1]-o2[1]; // 두번째 숫자 기준 오름차순
        //return o2[1]-o1[1]; // 두번째 숫자 기준 내림차순
    }
});
```

### 다중 조건 
```java
int[][] arr = {{7,40},{5,50},{2,30},{6,20},{3,10}};

Arrays.sort(arr, new Comparator<int[]>() { 
    @Override
    public int compare(int[] o1, int[] o2) {
        return o1[0]!=o2[0] ? o1[0]-o2[0] : o1[1]-o2[1]; // 첫번째 기준 오름차순, 두번째 기준 오름차순
        //return o1[0]!=o2[0] ? o1[0]-o2[0] : o2[1]-o1[1]; // 첫번째 기준 오름차순, 두번째 기준 내림차순
    }
});
```

### 2. Lambda 사용 - Java 8이상
```java
int[][] arr = {{7,40},{5,50},{2,30},{6,20},{3,10}};

Arrays.sort(arr, (o1, o2) -> {
    return o1[0]-o2[0]; // 첫번째 숫자 기준 오름차순
});
```

### 3. Comparator.comparing() 사용
```java
int[][] arr = {{7,40},{5,50},{2,30},{6,20},{3,10}};

Arrays.sort(arr, Comparator.comparingInt((int[] o) -> o[0]));            // 첫번째 숫자 기준 오름차순
Arrays.sort(arr, Comparator.comparingInt((int[] o) -> o[0]).reversed()); // 첫번째 숫자 기준 내림차순
Arrays.sort(arr, Comparator.comparingInt((int[] o) -> o[1]));            // 두번째 숫자 기준 오름차순
Arrays.sort(arr, Comparator.comparingInt((int[] o) -> o[1]).reversed()); // 두번째 숫자 기준 내림차순
```
