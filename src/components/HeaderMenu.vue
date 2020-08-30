<template>
    <div class="headerMenuWrapper">
        <div :class="{
            link: true,
            linkActive: selectedLink === link ? true : false
        }" 
            v-for="link in slicedLinks" 
            :key="slicedLinks.indexOf(link)" 
            @click="selectLink(link)"
        >
            {{link}}
        </div>
        <div :class="{
            link: true,
            linkActive: selectedLink === 'Ещё' ? true : false
        }"
        @click="selectLink('Ещё')">
            Ещё
            <span class="arrow"></span>
        </div>
    </div>    
</template>

<script>
export default {
    data: () =>({
        links: ['Все', 'Суши', 'Пицца', 'Бургеры', 'Фастфуд', 'Шашлыки', 'Азиатская', 'Десерты', 'Здоровая еда'],
        window: {
            width: 0,
            height: 0
        },
        selectedLink: 'Все'
    }),
    created() {
        window.addEventListener('resize', this.handleResize);
        this.handleResize();
    },
    destroyed() {
        window.removeEventListener('resize', this.handleResize);
    },
    methods: {
        handleResize() {
            this.window.width = window.innerWidth;
            this.window.height = window.innerHeight;
        },
        selectLink(link){
            this.selectedLink = link;
        }
    },
    computed:{
        linksCount(){
            return Math.floor((this.window.width - 200)/140);
        },
        slicedLinks(){
            if(this.linksCount <= 1){
                return this.links;
            }
            return this.links.slice(0, this.linksCount-1);
        }
    }
}
</script>

<style scoped>
.headerMenuWrapper{
    min-height: 60px;
    margin: 0px;
    padding: 0px 100px 0px 100px;
    background: #9CCB3B;
    display: flex;
    align-items: center;
    justify-content: space-between;
    flex-wrap: wrap;
}

.link{
    position: relative;
    width: 140px;
    height: 40px;
    margin: 10px 0px 10px 0px;
    font-style: normal;
    font-weight: bold;
    font-size: 18px;
    line-height: 22px;
    text-align: center;
    color: #FFFFFF;
    display: flex;
    align-items: center;
    justify-content: center;
    cursor: pointer;
}
.linkActive{
    background: #FFFFFF;
    border-radius: 5px;
    color: #000000;
}
.arrow{
    background: url('../assets/arrow.svg') no-repeat center;
    display: inline-block;
    width: 18px;
    height: 10px;
    position: absolute;
    right: 1.39%;
    top: 42.5%;
}
</style>