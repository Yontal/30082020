<template>
    <div>
        <div class="headerWrapper">
            <div class="left">
                <div class="logoContainer">
                    <span class="logo"></span>
                </div>
                <div class="locationContainer" 
                        v-if="!changeAdress" 
                        @click="changeAdress = !changeAdress"
                >
                    <span class="location"></span>
                    {{selectedAdress}}
                </div>
                <div class="locationChangeContainer" 
                        v-else
                >
                    <div class="leftInput">
                        <span class="location"></span>
                        <input  
                            type="text" 
                            class="input" 
                            placeholder="Введите адрес доставки" 
                            autofocus
                            v-model="typedAdress"
                        />
                    </div>
                    <div class="rightInput">
                        <span class="lineInput"></span>
                        <span class="cross" @click="changeAdress = !changeAdress"></span>
                    </div>
                    <div class="adressList">
                        <div 
                            v-for="adress in filteredAdresses" 
                            :key="filteredAdresses.indexOf(adress)"
                            class="adress"
                            @click="selectAdress(adress)"
                        >
                            <span class="locationRounded"></span>
                            {{adress}}
                        </div>
                    </div>
                </div>
            </div>
            <div class="right">
                <div class="searchContainer">
                    <span class="search"></span>
                    Поиск
                </div>
                <div class="exitContainer">
                    <span class="exit"></span>
                    Войти
                </div>
                <div class="cartContainer">
                    <span class="cart"></span>
                </div>
            </div>
        </div>
        <div>
            <HeaderMenu />
        </div>
    </div>
</template>

<script>
import HeaderMenu from '../components/HeaderMenu'

export default {
    components:{
        HeaderMenu
    },
    data: () => ({
        selectedAdress: 'ул. Петровско-Разумовская 17',
        changeAdress: false,
        adressList: [
            'ул. Петровско-Разумовская 17',
            'ул. Сибирский проезд 10, к.2',
            'ул. Перервинский бульвар 27, к.1',
        ],
        typedAdress: '',
    }),
    methods:{
        selectAdress(adress){
            this.selectedAdress = adress;
            this.changeAdress = false;
        }
    },
    computed:{
        filteredAdresses(){
            return this.adressList.filter(adress => {
                return adress.indexOf(this.typedAdress) != -1 ? true : false;
            })
        }
    }
}
</script>

<style scoped>
.left, .right {
    display: flex;
}
.headerWrapper{
    display: flex;
    align-items: center;
    justify-content: space-between;
    height: 89px;
    padding: 0px;
    max-width: 1400px;
    padding: 0px 100px 0px 100px;
    font-weight: 600;
    font-size: 18px;
    line-height: 22px;
}
.logoContainer, .locationContainer, .searchContainer, .exitContainer, .cartContainer{
    display: flex;
    align-items: center;
    cursor: pointer;
}
.logoContainer{
    margin-right: 127px;
}
.searchContainer, .exitContainer{
    margin-right: 75px;  
}
.locationChangeContainer{
    background: #F5F5F5;
    border-radius: 5px;
    display: flex;
    align-items: center;
    width: 450px;
    height: 40px;
    justify-content: space-between;
}
.logo{
    background: url('../assets/logo.svg') no-repeat center;
    display: inline-block;
    width: 180px;
    height: 40px;
}
.location{
    background: url('../assets/cil_location-pin.svg') no-repeat center;
    display: inline-block;
    width: 32px;
    height: 31px;
    margin-left: 11px;
}
.search{
    background: url('../assets/search.svg') no-repeat center;
    display: inline-block;
    width: 25px;
    height: 25px;
    margin-right: 13px;
}
.exit{
    background: url('../assets/exit.svg') no-repeat center;
    display: inline-block;
    width: 21px;
    height: 16px;
    margin-right: 13px;
}
.cart{
    background: url('../assets/cart.svg') no-repeat center;
    display: inline-block;
    width: 28px;
    height: 24px;
}
.input{
    position: relative;
    border: 0px;
    background: #F5F5F5;
    font-family: 'proxima';
    font-style: normal;
    font-weight: 600;
    font-size: 18px;
    line-height: 24px;
    width: 335px;
    margin-left: 15px;
}
.lineInput{
    background: url('../assets/lineInput.svg') no-repeat center;
    display: inline-block;
    width: 1px;
    height: 30px;
}
.adressList{
    position: absolute;
    background: #FFFFFF;
    box-shadow: 2px 6px 20px rgba(119, 119, 119, 0.18);
    border-radius: 5px;
    width: 450px;
    top: 65px;
    z-index: 2;
    font-style: normal;
    font-weight: 600;
    font-size: 16px;
    line-height: 24px;

color: #979797;
}
.locationRounded{
    background: url('../assets/cil_location-pin-rounded.svg') no-repeat center;
    display: inline-block;
    width: 24px;
    height: 24px;
    padding-left: 14px;
    padding-bottom: 9px;
    padding-right: 13px;
    padding-bottom: 10px;
    cursor: pointer;
}
.adress{
    display: flex;
    align-items: center;
    cursor: pointer;
}
.cross{
    background: url('../assets/cross.svg') no-repeat center;
    display: inline-block;
    width: 16px;
    height: 17px;
    padding: 15px;
    cursor: pointer;
}
.leftInput, .rightInput{
    display: flex;
    align-items: center;
}
::-webkit-input-placeholder {
    color: #979797;    
    font-family: 'proxima';
    font-style: normal;
    font-weight: 600;
    font-size: 18px;
    line-height: 24px;}
::-moz-placeholder          {
    color: #979797;
    font-family: 'proxima';
    font-style: normal;
    font-weight: 600;
    font-size: 18px;
    line-height: 24px;}
:-moz-placeholder           {
    color: #979797;    
    font-family: 'proxima';
    font-style: normal;
    font-weight: 600;
    font-size: 18px;
    line-height: 24px;}
:-ms-input-placeholder      {
    color: #979797;    
    font-family: 'proxima';
    font-style: normal;
    font-weight: 600;
    font-size: 18px;
    line-height: 24px;}
</style>