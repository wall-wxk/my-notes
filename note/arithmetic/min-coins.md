# 硬币找零

```javascript
class MinCoinChange{
    private coins: number[];
    private cache: any;
    protected constructor(coins){
        this.coins = coins;
        this.cache = {};
    }
    public makeChange(amount: number){
        const self = this;
        if(!amount){
            return [];
        }
        if(self.cache[amount]){
            return self.cache[amount];
        }
        let min: number[] = [];
        let newMin: number[] = [];
        let newAmount: number;
        const coins = self.coins;

        for(let i = 0; i < coins.length; i++){
            let coin = coins[i];
            newAmount = amount - coin;

            if(newAmount >= 0){
                newMin = self.makeChange(newAmount);
            }
            if(newAmount >= 0 && (newMin.length < min.length -1 || !min.length) && (newMin.length || !newAmount)){
                min = [coin].concat(newMin);
                console.log(`new Min ${min} for ${amount}`);
            }
        }
        return (self.cache[amount] = min);
    }
}

export default MinCoinChange;
```