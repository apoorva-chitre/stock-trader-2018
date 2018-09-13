<template>
    <nav class="navbar navbar-expand-lg navbar-dark" style="background-color:#563d7c;">
        <div class="container-fluid">
                <router-link to="/" class="navbar-brand">Stock Trader</router-link>

                <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarNavDropdown" aria-controls="navbarNavDropdown" aria-expanded="false" aria-label="Toggle navigation">
                  <span class="navbar-toggler-icon"></span>
                </button>

            <div class="collapse navbar-collapse" id="navbarNavDropdown">

                <ul class="navbar-nav mr-auto">
                    <router-link to="/portfolio" class="nav-item" tag="li"><a class="nav-link">Portfolio</a></router-link>
                    <router-link  class="nav-item" to="/stocks"  tag="li"><a class="nav-link">Stocks</a></router-link>
                </ul>
                <ul class="nav navbar-nav ml-auto">
                    <li><strong class="navbar-text">Funds : {{ funds | currency }}</strong></li>
                    <li class="nav-item"><a class="nav-link" href="#" @click="endDay" >End Day</a></li>
                    <li
                            class="nav-item dropdown" >
                        <a
                                href="#"
                                class="nav-link dropdown-toggle"
                                id="navbarDropdownMenuLink"
                                data-toggle="dropdown"
                                role="button"
                                aria-haspopup="true"
                                aria-expanded="false">Save & Load <span class="caret"></span></a>
                        <ul class="dropdown-menu" aria-labelledby="navbarDropdownMenuLink">
                            <a class="dropdown-item" href="#" @click="saveData" >Save Data</a>
                            <a class="dropdown-item" href="#" @click="loadData">Load Data</a>
                        </ul>
                    </li>
                </ul>
            </div><!-- /.navbar-collapse -->
        </div><!-- /.container-fluid -->
    </nav>
</template>

<script>

    import { mapActions } from 'vuex';

    export default {

        data() {
            return{
                
            }
        },

        computed: {

            funds() {
                return this.$store.getters.funds;
            }
        },

        methods: {

            ...mapActions({
                
                randomizeStocks: 'randomizeStocks',
                fetchData: 'loadData'

            }),

            endDay() {
                this.randomizeStocks();
            },

            saveData() {

                const data = {
                    funds: this.$store.getters.funds,
                    stockPortfolio: this.$store.getters.stockPortfolio,
                    stocks: this.$store.getters.stocks
                };

                this.$http.put('data.json', data);
            },

            loadData() {

               this.fetchData();
            }
        }
    }
	
</script>

<style scoped>
  
  body {
    margin: 20px 0px 0px 0px;
  }

  .navbar-text {

        color: #f8f8ff;
  }

</style>
