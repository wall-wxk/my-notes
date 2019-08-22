# 两个数不使用四则运算得出和

```javascript
function sum(a, b){
    if(a == 0){
        return b;
    }
    if(b == 0){
        return a;
    }

    const newA = a ^ b; // 算出不用进位的数
    const newB = (a & b) << 1; // 算出1+1要进位的数

    return sum(newA, newB);
}
```