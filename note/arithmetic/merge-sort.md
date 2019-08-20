# 归并排序

```javascript
type TNumberArray = number[];

function mergeSortedArray(leftArray: TNumberArray, rightArray: TNumberArray): TNumberArray{
    let sortedArray: TNumberArray = [];
    while(leftArray.length && rightArray.length){
        let minElement: number | undefined;
        if(leftArray[0] < rightArray[0]){
            minElement = leftArray.shift();
        }else{
            minElement = rightArray.shift();
        }
        if(typeof minElement !== 'undefined'){
            sortedArray.push(minElement);
        }
    }

    if(leftArray.length){
        sortedArray = sortedArray.concat(leftArray);
    }
    if(rightArray.length){
        sortedArray = sortedArray.concat(rightArray);
    }

    return sortedArray;
}

function sort(originalArray: TNumberArray): TNumberArray{
    if(originalArray.length <= 1){
        return originalArray;
    }

    const middleIndex = Math.floor(originalArray.length / 2);
    const leftArray = originalArray.slice(0, middleIndex);
    const rightArray = originalArray.slice(middleIndex, originalArray.length);

    const leftSortedArray = sort(leftArray);
    const rightSortedArray = sort(rightArray);

    return mergeSortedArray(leftSortedArray, rightSortedArray);
}



export default sort;
```