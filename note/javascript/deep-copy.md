# 深拷贝

> 注意的点：
> 1. Symbol属性的拷贝（不可枚举）
> 2. 循环引用
> 3. 数组和对象的区分
> 4. 递归爆栈
> 5. 引用丢失(obj.a, obj.b 引用同一个对象，深拷贝后，变成2个不同的对象)

```javascript
function deepCopy(obj, hash = new WeakMap()){
    if(!isObject(option)){
        return option;
    }
    if(hash.has(option)){
        return has.get(option);
    }
    let target = Array.isArray(option) ? [...option] : {...option}; // 扩展运算符只能浅拷贝
    hash.set(option, target);

    Reflect.ownKeys(target).forEach(key => {
        if(isObject(option[key])){
            target[key] = deepCopy(option[key], hash);
        }else{
            target[key] = option[key];
        }
    })

    return target;
}
function isObject(option){
    if(typeof option ==== 'object' && option !== null){
        return true;
    }
    return false;
}
```