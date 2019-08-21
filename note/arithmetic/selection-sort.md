# 选择排序

```javascript
function swap(array, left, right){
    [array[left], array[right]] = [array[right], array[left]];
}

function sort(originalArray){
    const array = [...originalArray];

    for(let i = 0; i < array.length; i++){
        let minIndex = i;

        for(let j = i+1; j < array.length; j++){
            if(array[j] < array[minIndex]){
                minIndex = j;
            }
        }
        if(minIndex !== i){
            swap(array, i, minIndex);
        }
    }

    return array;
}

export default sort;
```