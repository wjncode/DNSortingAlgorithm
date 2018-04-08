在计算机科学与数学中，一个排序算法（英语：Sorting algorithm）是一种能将一串数据依照特定排序方式进行排列的一种算法,这里总结几个常用算法的写法,包括冒泡排序,快速排序,插入排序,选择排序.
<!--more-->

### 冒泡排序
``` swift
func bubbleSort<T: Comparable> (oArr: [T]) -> [T] {
    var arr = oArr
    for outerIndex in (1...arr.count - 1).reversed() {
        for innerIndex in 0..<outerIndex {
            if arr[innerIndex] > arr[innerIndex + 1] {
                let temp = arr[innerIndex]
                arr[innerIndex] = arr[innerIndex + 1]
                arr[innerIndex + 1] = temp
            }
        }
    }
    return arr
}
```

### 快速排序
``` swift
extension Array {
    var decompose : (head: Element, tail: [Element])? {
    return (count > 0) ? (self[0], Array(self[1..<count])) : nil
    }
}

func quickSort<T: Comparable> (oArr: [T]) -> [T] {
    let arr = oArr
    if let (pivot, rest) = arr.decompose {
        let lesser  = rest.filter { $0 < pivot }
        let greater = rest.filter { $0 >= pivot }
        let les = quickSort(oArr: lesser)
        let gre = quickSort(oArr: greater)
        return les + [pivot] + gre
    } else {
        return []
    }
}
```

### 插入排序
``` swift
func insertionSort<T: Comparable> (oArr: [T]) -> [T] {
    var arr = oArr
    for outerIndex in 1..<arr.count {
        let temp = arr[outerIndex]
        var innerIndex = outerIndex
        while innerIndex > 0 && arr[innerIndex - 1] >= temp {
            arr[innerIndex] = arr[innerIndex - 1]
            innerIndex -= 1
        }
        arr[innerIndex] = temp
    }
    return arr
}
```

### 选择排序
``` swift
func selectSort<T: Comparable> (oArr: [T]) -> [T] {
    var arr = oArr
    var minIndex = 0 // 记录每次遍历的最小值位置
    for outerIndex in 0..<arr.count {
        minIndex = outerIndex
        for innerIndex in (outerIndex + 1)..<arr.count {
            if arr[minIndex] > arr[innerIndex] {
                minIndex = innerIndex // 判断最小值,记住下表
            }
            if minIndex != outerIndex {
                let temp = arr[outerIndex]
                arr[outerIndex] = arr[minIndex]
                arr[minIndex] = temp
            }
        }
    }
    return arr
}
```

更多的排序算法可以去[wiki百科](https://zh.wikipedia.org/wiki/%E6%8E%92%E5%BA%8F%E7%AE%97%E6%B3%95)看看
