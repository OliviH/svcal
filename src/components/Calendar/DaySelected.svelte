<script>
    import { createEventDispatcher } from 'svelte'
    import moment from 'moment'
    const fr = moment().locale('fr')
    const dispatch = createEventDispatcher()
    export let day = {}

    const sayDate = (dt, format) => moment(dt).locale('fr').format(format)
    
</script>
<button class="svcal__button" on:click={() => {dispatch("esc")}}><svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em">
    <use xlink:href="#return"></use>
</svg></button>
{sayDate(day.date,'L')}