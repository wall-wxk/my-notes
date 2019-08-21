# 冒泡排序

```javascript
function swap(array, left, right){
    [array[left], array[right]] = [array[right], array[left]];
}

function sort(originalArray){
    const array = [...originalArray];
    let arrayLength = array.length;

    for(let i = 1; i < arrayLength; i++){
        for(let j = 0; j < arrayLength-i; j++){
            if(array[j] < array[j+1]){
                swap(array, j, j+1);
            }
        }
    }

    return array;
}

export default sort;
```