<template translate="no" class="py-5">
  <div id="app">
            <div class="container">
            <div class="row">
                <div class="col-md-8 mx-auto">
                    <div class="d-flex flex-row justify-content-between">
                        <div class="title">Rock . Paper . Scissor .</div>
                        <div class="d-flex scores flex-row">
                            <div class="d-flex align-items-center you mr-3 justify-content-between">
                                <span class="text">You</span><span class="score font-weight-bold" :class="yourScore >= computerScore ? 'text-success' : 'text-danger'"> {{yourScore}}</span>
                            </div>
                            <div class="d-flex align-items-center computer">
                                <span class="text">Computer</span><span class="score font-weight-bold" :class="computerScore >= yourScore ? 'text-success' : 'text-danger'"> {{computerScore}}</span>
                            </div>   
                        </div>
                    </div>
                </div>
            </div>
         </div>
                     <div class="row">
                <div class="col-md-6 mx-auto">
                    <div class="d-flex flex-row justify-content-between align-items-center">
                        <div class="options">
                            <div class="r" :class="yourWeapon == 'Rock' ? 'checked' : ''" @click="changeWeapon('Rock')"></div>
                            <div class="p" :class="yourWeapon == 'Paper' ? 'checked' : ''" @click="changeWeapon('Paper')"></div>
                            <div class="s" :class="yourWeapon == 'Scissor' ? 'checked' : ''" @click="changeWeapon('Scissor')"></div>
                        </div>
                        <div class="game">
                            <div class="chooseWeapon" v-if="!yourWeapon">Choose your Weapon</div>
                                
                            <div class="fighting" v-if="fighting">
                                <div class="spinner-border text-danger" role="status">
                                    <span class="sr-only">Loading...</span>
                                </div>
                            </div>
                            <div class="result" :class="result" v-if="result">{{result.toUpperCase()}}</div>
                        </div>
                        <div class="it">
                            <div v-show="computerWeapon === 'Rock'" class="r"></div>
                            <div v-show="computerWeapon === 'Paper'" class="p"></div>
                            <div v-show="computerWeapon === 'Scissor'" class="s"></div>
                        </div>
                    </div>
                    <div class="d-flex flex-row justify-content-center text-center controls shadow rounded">
                        <div class="flex-fill">
                            <button type="button" class="btn btn-info">
                                Rounds <span class="badge badge-light">{{totalRounds}}</span>
                            </button>
                        </div>
                        <div class="flex-fill"><button @click="reset" class="btn btn-warning">Reset</button>
                        </div>
                    </div>
                </div>
                </div>
            </div>           

</template>







<script >
export default {
  name: 'App',
          data() {
            return{
            options: ['Rock', 'Paper', 'Scissor'],
            yourWeapon: '',
            computerWeapon: '',
            result: '',
            yourScore: 0,
            computerScore: 0,
            totalRounds: 0,
            fighting : false,
          }
        },
         methods:{
            fight(){
                this.fighting = true;
                this._pretendProcessing();
            },
            _fight(){
                this.computerWeapon = this.options[Math.floor(Math.random() * this.options.length)]; 
                if(this.yourWeapon === this.computerWeapon)
                    this._draw();
                if(this.computerWeapon === 'Rock'){
                    if(this.yourWeapon === 'Paper'){
                        this._win();
                    }
                    if(this.yourWeapon === 'Scissor'){
                        this._lost();
                    }
                }
                if(this.computerWeapon === 'Paper'){
                    if(this.yourWeapon === 'Rock'){
                        this._lost();
                    }
                    if(this.yourWeapon === 'Scissor'){
                        this._win();
                    }
                }
                if(this.computerWeapon === 'Scissor'){
                    if(this.yourWeapon === 'Rock'){
                        this._win();
                    }
                    if(this.yourWeapon === 'Paper'){
                        this._lost();
                    }
                }
            },
            

            changeWeapon(weapon){
                if(this.fighting)
                   return;                  
                this.yourWeapon = weapon;
                this.result = '';
                this.computerWeapon = '';
            },

            _pretendProcessing(){
                var x = 0;
                var intervalID = setInterval(() =>{

                    this.computerWeapon = this.options[Math.floor(Math.random() * this.options.length)];

                    if (++x === 10) {
                        window.clearInterval(intervalID);
                        this._fight();
                        this.fighting = false;
                    }
                }, 100);
            },

            _draw(){
                this.result = 'draw',
                this.totalRounds++;
            },

            _win(){
                this.result = 'won';
                this.yourScore++;
                this.totalRounds++;
            },

            _lost(){
                this.result = 'lost';
                this.computerScore++;
                this.totalRounds++;
            },

            reset(){
                this.computerScore = 0;
                this.yourScore = 0;
                this.result = '';
                this.yourWeapon = '';
                this.computerWeapon = '';
                this.totalRounds= 0;
            }

        }
    }





        
</script>














<style>
</style>
