# 实现Promise

```javascript
class MyPromise{
    private state: string;
    private data: any;
    private reason: any;
    public constructor(fn){
        if(typeof fn !== 'function'){
            throw new Error(`Promise resolver ${fn} is not a function`);
        }
        this.resolve = this.resolve.bind(this);
        this.reject = this.reject.bind(this);
        this.state = 'pending'; // promise状态
        this.data = undefined; // resolve信息
        this.reason = undefined; // reject信息

        try{
            fn(this.resolve, this.reject);
        }catch(e){
            this.catch(e);
        }
    }
    public resolve(res){
        if(this.state !== 'pending'){
            return;
        }

        this.state = 'fulfilled';
        this.data = res;
    }
    public reject(reason){
        if(this.state !== 'pending'){
            return;
        }

        this.state = 'rejected';
        this.reason = reason;
    }
    public then(resolve, reject): any{
        const self = this;
        switch(this.state){
            case 'fulfilled':
                return new Promise((nextResolve) => {
                    nextResolve(resolve(self.data));
                });
            case 'rejected':
                reject(this.reason);
                return new Promise(() => {});
            case 'pending':
                return this;
        }
    }
    public catch(err){
        console.log('promise catch：', err);
    }
}
export default MyPromise;
```