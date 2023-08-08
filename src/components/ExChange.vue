<script>
export default {
    props: ["rate"],
    data() {
        return {
            inp: null,
            result:null,
            s1: null,
            s2: null,
            Oldsl: null,
            dataList2:[],
            show: false

        }
    },
    methods: {
        //交換按鈕
        change() {
            this.Oldsl = this.s1
            this.s1 = this.s2
            this.s2 = this.Oldsl
            this.show = false

        },
        //轉換按鈕
        switch2() {
            // fetch(`https://open.exchangerate-api.com/v6/latest/${this.s1}`)
            // .then(res => res.json())
            // .then(data => {
            //     // console.log(data);
            //     this.dataList2 = data.rates
            //     //this.dataList[this.s2]   <<<<倍率
            //     // result = input直 * 倍率
            //     console.log(this.dataList2[this.s2]);
            //     // console.log(this.dataList2.AED);
            // })
            
            if (this.s1 === this.s2) {
                alert("請選擇不同的幣別");
            } else {
                // 右邊的值丟到左邊的變數
                this.result = this.inp * this.dataList2[this.s2]
                this.show = true;


                // console.log(this.inp*this.rate[this.s2]);
            }  
            
   
        },
        // 重製按鈕
        reset(){
            window.location.reload();
        }
    },
    watch:{
        inp(){
            this.show = false;
        },
        s1(){
            this.show = false;
        },
        s2(){
            this.show = false;
        },

    },
    //生命週期
    updated() {
        fetch(`https://open.exchangerate-api.com/v6/latest/${this.s1}`)
            .then(res => res.json())
            .then(data => {
                console.log(data);
                this.dataList2 = data.rates
    

    
            })
        
        
    },
    

}
</script>


<template>
    <div class="note">
        
    </div>
    <div class="container">
        <!-- 篩選器1轉換前 -->
        <select name="Currency" id="before" v-model="s1">
            <option value="">請選擇幣別</option>
            <option v-for="(item, index) in rate" :value="index" key="item">{{ index }}</option>
        </select>
        <button v-on:click="change" type="button" class="exchange-btn">互換按鈕</button>
        <!-- 篩選器2轉換後 -->
        <select name="Currency" id="after" v-model="s2">
            <option value="">請選擇幣別</option>
            <option v-for="(item, index) in rate" :value="index" key="item">{{ index }}</option>
        </select>
        <input v-model="inp" type="number" class="input">←請選擇初始幣別的金額

       
        <button v-on:click="reset" type="button" class="reset-btn">Reset</button>
        
    </div>
    <div class="btn-aera">
        <div class="moji1-aera1">
            <p>↑</p>
            <p class="mojo1">請選擇初始幣別</p>
        </div>
        <div class="moji1-aera2">
            <p>↑</p>
            <p class="mojo2">請選擇要轉換幣別</p>
        </div>
 
        <button v-on:click="switch2" class="change-btn" type="button">轉換</button>
    </div>
    
    <h2>轉換結果</h2>
    <div class="result-aera">

        
        <span v-show="show" class="text-result">{{ inp }}</span>
        <div class="kabe"></div>
        <span v-show="show" class="text-result">{{ s1 }}</span>
        <div class="kabe"></div>
        <span v-show="show" value="ture" class="text-result">   =   </span>
        <div class="kabe"></div>
        <span v-show="show" class="text-result">{{ result }}</span>
        <div class="kabe"></div>
        <span v-show="show" class="text-result">{{ s2 }}</span>



    </div>
    
</template>


<style lang="scss">
.container {
    display: flex;
    justify-content: center;

    .result {
        width: 100px;
        height: 20px;
        border: 3px solid black;
    }
    
    .input{
        margin: 0 1rem;
    }
    .result{
        margin: 0 1rem;

    }
    .exchange-btn{
        margin: 0 1rem;
    }
    .reset-btn{
        margin: 0 1rem;
    }
}
h2{
    margin-top: 40px;
    display: flex;
    justify-content: center;
}
.result-aera{
    display: flex;
    justify-content: center;
    margin-top: 60px;

    .kabe{
        width: 10px;
        height: 20px;
        // border: 2px solid red;
    }
    
    .text-result{
        font-size: 40px;
    }
}
.btn-aera{
    margin-top: 10px;
    display: flex;
    justify-content: center;
    width: 100vw;
    p{
        font-weight: bold;
    }
    .mojo1{
        margin-right: 100px;
    }
    .mojo2{
        margin-right: 250px;
    }
    .change-btn {
    display: block;
    margin: 0 1rem;
    width: 80px;
    height: 80px;
    border-radius: 100px;
    cursor: pointer;
    transition: 0.2s;
    border: none;
    font-weight: bold;
    background-color: rgb(255, 255, 0);
    font-size: 20px;

    &:hover {
        scale: 1.05;
        
    }

    &:active {
        scale: 0.95;
        background-color: rgb(251, 251, 107);
        
    }

    }

}

</style>


