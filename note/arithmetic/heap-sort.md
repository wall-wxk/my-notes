# 堆排序

```javascript
// 堆排序
function swap(array, key1, key2){
    [array[key1], array[key2]] = [array[key2], array[key1]];
}

// 调整堆
function heapify(array, i){
    let left = i*2+1;
    let right = i*2+2;
    let largest = i;
    const heapSize = array.length;

    if(left < heapSize && array[left] > array[largest]){
        largest = left;
    }
    if(right < heapSize && array[right] > array[largest]){
        largest = right;
    }
    if(largest !== i){
        swap(array, i, largest);
        heapify(array, largest);
    }
}

// 初始化堆
function buildHeap(array){
    const heapSize = array.length;
    for(let i = Math.floor(heapSize/2); i >= 0; i--){
        heapify(array, i);
    }
}

function sort(array){
    let sortedArray: number[] = [];
    buildHeap(array);
    
    while(array.length > 0){
        swap(array, 0, array.length-1); // 最大值放到最后一个节点 
        sortedArray.push(array.pop());
        heapify(array, 0); // 重新构建最大堆
    }

    return sortedArray;
}

export default sort;
```