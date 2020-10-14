<template>
    <div class="event-tile">
        <div class="event-info">
            <p v-html="escapedDesc"></p>
        </div>
        <div class="event-img-wrapper">
            <img :src="event.Image[0].url">
        </div>
    </div>
</template>

<script>
export default {
    props: ['event'],
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
        escapedDesc: function () {
            return this.event.Description.replaceAll(/\n/g,'<br/>')
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
    margin-top: 60px;
    padding-left: 22px;
    padding-right: 22px;
    padding-top: 20px;
    padding-bottom: 20px;
    width: 83vw;
    float: left;
}

.event-info {
    text-align: left;
    font-size: 20px;
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