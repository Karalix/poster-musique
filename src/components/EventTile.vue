<template>
    <div class="event-tile" :class="{alone : nbEvents === 1}">
        <div class="event-info">
            <h2>{{event.Nom}}</h2>
            <p v-if="this.event.Date"><strong>{{localeDate}}</strong> à {{localeTime}}</p>
            <p v-html="parsedDesc"></p>

        </div>
        <div class="event-img-wrapper">
            <img :src="event.Image[0].url">
        </div>
    </div>
</template>

<script>
import md from 'markdown-it'


export default {
    props: ['event','nbEvents'],
    computed: {
        localeDate: function () {
            const options = { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric'}
            const dateobj = new Date(this.event.Date)
            return dateobj.toLocaleString(undefined, options)
        },
        localeTime: function () {
            const options = { hour: 'numeric', minute: 'numeric'}
            const dateobj = new Date(this.event.Date)
            return dateobj.toLocaleString(undefined, options)
        },
        parsedDesc: function () {
            return md().render(this.event.Description)
        }
    }
}
</script>

<style scoped>
.event-tile {
    display: grid;
    grid-template-columns: 2fr 1fr;
    background: #252525;
    box-shadow: inset 0px 4px 4px rgba(0, 0, 0, 0.25);
    border-radius: 20px;
    margin-left: 50px;
    margin-top: 22px;
    padding-left: 22px;
    padding-right: 22px;
    width: 39vw;
    min-height: 250px;
    float: left;
}

.alone {
    width: 90vw;
}

.event-info {
    text-align: left;
    font-size: 20px;
    margin-right: 10px;
}

.event-info h2 {
    margin-left: 0px;
    font-size: 30px;
    font-weight: bold;
    line-height: unset;
}

.event-img-wrapper img {
    height: 180px;
    width: 180px;
    object-fit: cover;
    border-radius: 10px;
    margin-top: 35px;
}
</style>