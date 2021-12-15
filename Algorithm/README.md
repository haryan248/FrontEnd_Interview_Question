## Sorting Algorithm

Sorting 알고리즘은 크게 Comparisons 방식과 Non-Comparisons 방식으로 나눌 수 있다.

### Comparisons Sorting Algorithm (비교 방식 알고리즘)

`Bubble Sort`, `Selection Sort`, `Insertion Sort`, `Merge Sort`, `Heap Sort`, `Quick Sort` 를 소개한다.

### Bubble Sort

n 개의 원소를 가진 배열을 정렬할 때, In-place sort 로 인접한 두 개의 데이터를 비교해가면서 정렬을 진행하는 방식이다. 가장 큰 값을 배열의 맨 끝에다 이동시키면서 정렬하고자 하는 원소의 개수 만큼을 두 번 반복하게 된다.

| Space Complexity | Time Complexity |
| :--------------: | :-------------: |
|       O(1)       |     O(n^2)      |

#### [code](https://github.com/JaeYeopHan/algorithm_basic_java/blob/master/src/test/java/sort/BubbleSort.java)

```
function bubbleSort(array) {
    for (let i = 0; i < array.length; i++) {
        let swap;
        for (let j = 0; j < array.length - 1 - i; j++) {
            if (array[j] > array[j + 1]) {
                swap = array[j];
                array[j] = array[j + 1];
                array[j + 1] = swap;
            }
        }
        console.log(`${i}회전: ${array}`);
        if (!swap) {
            break;
        }
    }
    return array;
}
```

</br>

### Selection Sort

n 개의 원소를 가진 배열을 정렬할 때, 계속해서 바꾸는 것이 아니라 비교하고 있는 값의 index 를 저장해둔다. 그리고 최종적으로 한 번만 바꿔준다. 하지만 여러 번 비교를 하는 것은 마찬가지이다.

| Space Complexity | Time Complexity |
| :--------------: | :-------------: |
|       O(1)       |     O(n^2)      |

```
function selectionSort(array) {
    for (let i = 0; i < array.length; i++) {
        let minIndex = i;
        for (let j = i + 1; j < array.length; j++) {
            if (array[minIndex] > array[j]) {
                minIndex = j;
            }
        }
        // 뒤에서 최소를 선택한다음 맨앞과 swap
        // minIndex <-> i
        if (minIndex !== i) {
            let swap = array[minIndex];
            array[minIndex] = array[i];
            array[i] = swap;
        }
        console.log(`${i}회전: ${array}`);
    }
    return array;
}
// console.log(selectSort([5, 4, 3, 2, 1]));
```

#### [code](https://github.com/JaeYeopHan/algorithm_basic_java/blob/master/src/test/java/sort/SelectionSort.java)

</br>

### Insertion Sort

n 개의 원소를 가진 배열을 정렬할 때, i 번째를 정렬할 순서라고 가정하면, 0 부터 i-1 까지의 원소들은 정렬되어있다는 가정하에, i 번째 원소와 i-1 번째 원소부터 0 번째 원소까지 비교하면서 i 번째 원소가 비교하는 원소보다 클 경우 서로의 위치를 바꾸고, 작을 경우 위치를 바꾸지 않고 다음 순서의 원소와 비교하면서 정렬해준다. 이 과정을 정렬하려는 배열의 마지막 원소까지 반복해준다.

| Space Complexity | Time Complexity |
| :--------------: | :-------------: |
|       O(1)       |     O(n^2)      |

```

function insertionSort(array) {
    // console.log(`${0}회전: ${array}`);

    for (let i = 1; i < array.length; i++) {
        let cur = array[i];
        let left = i - 1;
        // 현재값(cur) 이 left값보다 작으면 계속 true
        while (left >= 0 && array[left] > cur) {
            array[left + 1] = array[left];
            left--;
            console.log(i, array);
        }
        // left + 1는 들어갈 자리
        array[left + 1] = cur;
        console.log(`${i}회전: ${array} left + 1: ${left + 1}, cur :${cur}`);
    }
    return array;
}
// console.log(insertionSort([5, 4, 2, 3, 1]));
```

#### [code](https://github.com/JaeYeopHan/algorithm_basic_java/blob/master/src/test/java/sort/InsertionSort.java)

</br>

### Merge Sort

기본적인 개념으로는 n 개의 원소를 가진 배열을 정렬할 때, 정렬하고자 하는 배열의 크기를 작은 단위로 나누어 정렬하고자 하는 배열의 크기를 줄이는 원리를 사용한다. `Divide and conquer`라는, "분할하여 정복한다"의 원리인 것이다. 말 그대로 복잡한 문제를 복잡하지 않은 문제로 분할하여 정복하는 방법이다. 단 분할(divide)해서 정복했으니 정복(conquer)한 후에는 **결합(combine)** 의 과정을 거쳐야 한다.

`Merge Sort`는 더이상 나누어지지 않을 때 까지 **반 씩(1/2)** 분할하다가 더 이상 나누어지지 않은 경우(원소가 하나인 배열일 때)에는 자기 자신, 즉 원소 하나를 반환한다. 원소가 하나인 경우에는 정렬할 필요가 없기 때문이다. 이 때 반환한 값끼리 **`combine`될 때, 비교가 이뤄지며,** 비교 결과를 기반으로 정렬되어 **임시 배열에 저장된다.** 그리고 이 임시 배열에 저장된 순서를 합쳐진 값으로 반환한다. 실제 정렬은 나눈 것을 병합하는 과정에서 이뤄지는 것이다.

결국 하나씩 남을 때까지 분할하는 것이면, 바로 하나씩 분할해버리면 되지 않을까? 재귀적으로 정렬하는 원리인 것이다. 재귀적 구현을 위해 1/2 씩 분할한다.

| Space Complexity | Time Complexity |
| :--------------: | :-------------: |
|       O(n)       |    O(nlogn)     |

</br>

### Heap Sort

`binary heap` 자료구조를 활용할 Sorting 방법에는 두 가지 방법이 존재한다. 하나는 정렬의 대상인 데이터들을 힙에 넣었다가 꺼내는 원리로 Sorting 을 하게 되는 방법이고, 나머지 하나는 기존의 배열을 `heapify`(heap 으로 만들어주는 과정)을 거쳐 꺼내는 원리로 정렬하는 방법이다. `heap`에 데이터를 저장하는 시간 복잡도는 `O(log n)`이고, 삭제 시간 복잡도 또한 `O(log n)`이 된다. 때문에 힙 자료구조를 사용하여 Sorting 을 하는데 time complexity 는 `O(log n)`이 된다. 이 정렬을 하려는 대상이 n 개라면 time complexity 는 `O(nlogn)`이 된다.

`Heap`자료구조에 대한 설명은 [DataStructure - Binary Heap](https://github.com/JaeYeopHan/Interview_Question_for_Beginner/tree/master/DataStructure#binary-heap)부분을 참고하면 된다.

| Space Complexity | Time Complexity |
| :--------------: | :-------------: |
|       O(1)       |    O(nlogn)     |

</br>

### Quick Sort

Sorting 기법 중 가장 빠르다고 해서 quick 이라는 이름이 붙여졌다. **하지만 Worst Case 에서는 시간복잡도가 O(n^2)가 나올 수도 있다.** 하지만 `constant factor`가 작아서 속도가 빠르다.

`Quick Sort` 역시 `Divide and Conquer` 전략을 사용하여 Sorting 이 이루어진다. Divide 과정에서 `pivot`이라는 개념이 사용된다. 입력된 배열에 대해 오름차순으로 정렬한다고 하면 이 pivot 을 기준으로 좌측은 pivot 으로 설정된 값보다 작은 값이 위치하고, 우측은 큰 값이 위치하도록 `partition`된다. 이렇게 나뉜 좌, 우측 각각의 배열을 다시 재귀적으로 Quick Sort 를 시키면 또 partition 과정이 적용된다.이 때 한 가지 주의할 점은 partition 과정에서 pivot 으로 설정된 값은 다음 재귀과정에 포함시키지 않아야 한다. 이미 partition 과정에서 정렬된 자신의 위치를 찾았기 때문이다.

#### Quick Sort's worst case

그렇다면 어떤 경우가 Worst Case 일까? Quick Sort 로 오름차순 정렬을 한다고 하자. 그렇다면 Worst Case 는 partition 과정에서 pivot value 가 항상 배열 내에서 가장 작은 값 또는 가장 큰 값으로 설정되었을 때이다. 매 partition 마다 `unbalanced partition`이 이뤄지고 이렇게 partition 이 되면 비교 횟수는 원소 n 개에 대해서 n 번, (n-1)번, (n-2)번 … 이 되므로 시간 복잡도는 **O(n^2)** 이 된다.

```

function quickSort(array, left = 0, right = array.length - 1) {
    if (left >= right) {
        return;
    }
    const mid = Math.floor((left + right) / 2);
    const pivot = array[mid];
    const partition = divide(array, left, right, pivot);
    quickSort(array, left, partition - 1);
    quickSort(array, partition, right);

    function divide(array, left, right, pivot) {
        while (left <= right) {
            while (array[left] < pivot) {
                left++;
            }
            while (array[right] > pivot) {
                right--;
            }

            if (left <= right) {
                let temp = array[left];
                array[left] = array[right];
                array[right] = temp;
                left++;
                right--;
            }
        }
        return left;
    }
    return array;
}
// console.log(quickSort([1, 12, 5, 26, 7, 14, 3, 7]));

let arry = [1, 2, 3];
arry.sort((next, now) => {
    console.log(next, now);
});
```

#### Balanced-partitioning

자연스럽게 Best-Case 는 두 개의 sub-problems 의 크기가 동일한 경우가 된다. 즉 partition 과정에서 반반씩 나뉘게 되는 경우인 것이다. 그렇다면 Partition 과정에서 pivot 을 어떻게 정할 것인가가 중요해진다. 어떻게 정하면 정확히 반반의 partition 이 아니더라도 balanced-partitioning 즉, 균형 잡힌 분할을 할 수 있을까? 배열의 맨 뒤 또는 맨 앞에 있는 원소로 설정하는가? Random 으로 설정하는 것은 어떨까? 특정 위치의 원소를 pivot 으로 설정하지 않고 배열 내의 원소 중 임의의 원소를 pivot 으로 설정하면 입력에 관계없이 일정한 수준의 성능을 얻을 수 있다. 또 악의적인 입력에 대해 성능 저하를 막을 수 있다.

#### Partitioning

정작 중요한 Partition 은 어떻게 이루어지는가에 대한 이야기를 하지 않았다. 가장 마지막 원소를 pivot 으로 설정했다고 가정하자. 이 pivot 의 값을 기준으로 좌측에는 작은 값 우측에는 큰 값이 오도록 해야 하는데, 일단 pivot 은 움직이지 말자. 첫번째 원소부터 비교하는데 만약 그 값이 pivot 보다 작다면 그대로 두고 크다면 맨 마지막에서 그 앞의 원소와 자리를 바꿔준다. 즉 pivot value 의 index 가 k 라면 k-1 번째와 바꿔주는 것이다. 이 모든 원소에 대해 실행하고 마지막 과정에서 작은 값들이 채워지는 인덱스를 가리키고 있는 값에 1 을 더한 index 값과 pivot 값을 바꿔준다. 즉, 최종적으로 결정될 pivot 의 인덱스를 i 라고 했을 때, 0 부터 i-1 까지는 pivot 보다 작은 값이 될 것이고 i+1 부터 k 까지는 pivot 값보다 큰 값이 될 것이다.

| Space Complexity | Time Complexity |
| :--------------: | :-------------: |
|    O(log(n))     |    O(nlogn)     |

#### [code](https://github.com/JaeYeopHan/algorithm_basic_java/blob/master/src/test/java/sort/QuickSort.java)
