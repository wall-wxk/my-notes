# 快速排序

```javascript
function swap(array, left, right){
    [array[left], array[right]] = [array[right], array[left]];
}

function partition(array, left, right){
    let i = left;
    let j = right;
    const privot = array[Math.floor((left+right)/2)]
    
    while(i <= j){
        while(array[i] < privot){
            i++;
        }
        while(array[j] > privot){
            j--;
        }
        if(i <= j){
            swap(array, i, j);
            i++;
            j--;
        }
    }
    return i;
}

function quick(array, left, right){
    if(array.length > 1){
        let privotIndex = partition(array, left, right);

        if(left < privotIndex -1){
            quick(array, left, privotIndex-1);
        }
        if(privotIndex < right){
            quick(array, privotIndex, right);
        }

    }
}

function sort(originalArray){
    let array = [...originalArray];

    if(array.length < 2){
        return array;
    }

    quick(array, 0, array.length-1);

    return array;
}

export default sort;
```