# 插入排序

```javascript
function swap(array, left, right){
    [array[left], array[right]] = [array[right], array[left]];
}

function sort(originalArray){
    let array = [...originalArray];

    for(let i = 0; i < array.length; i++){
        let currentIndex = i;

        while(typeof array[currentIndex - 1] !== 'undefined' && array[currentIndex] < array[currentIndex - 1]){

            let prevIndex = currentIndex-1;
            swap(array, currentIndex, prevIndex);
            currentIndex = prevIndex;
        }
    }

    return array;
}

export default sort;
```