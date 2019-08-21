# 希尔排序

```javascript
function sort(originalArray){
    const array = [...originalArray];
    const arrayLength = array.length;
    let gap = Math.floor(array.length / 2);

    while(gap > 0){
        for(let i = 0; i < (arrayLength - gap); i++){
            let gapIndex = i+gap;
            let currentIndex = i;
            
            while(currentIndex >= 0){
                if(array[currentIndex] < array[gapIndex]){
                    [array[currentIndex], array[gapIndex]] = [array[gapIndex], array[currentIndex]];
                }
                // 检测插入位置是否合适
                gapIndex = currentIndex;
                currentIndex -= gap;
            }
        }
        
        gap = Math.floor(gap/2);
    }

    return array;
}

export default sort;
```