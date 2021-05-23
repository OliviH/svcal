<script>
    import moment from 'moment'
    import DaySelected from './Calendar/DaySelected.svelte'
    export let cal = {}
    let displayed = "cal"
    let bexpanded = false
    let daySelected = {}
    export const selectmonth = (n) => {
		let mom = moment(n),
			date_cur,
			start,
			end
		cal.month_selected = mom.month()
		cal.days = []
		cal.firstDayMonth = {
			date: mom.startOf('month').format(),
			no: mom.startOf('month').days(),
			name: mom.startOf('month').format('dddd')
		}
		start = mom.startOf('month').format()
		end = mom.endOf("month").format()
		date_cur = moment(cal.firstDayMonth.date).subtract(cal.firstDayMonth.no, 'days').format()
		for (let i = 0; i < 42; i++) {
			cal.days.push({
				date: date_cur,
				name: moment(date_cur).format('dddd'),
				vis: (moment(date_cur).isSameOrAfter(start) && moment(date_cur).isSameOrBefore(end)),
			})
			date_cur = moment(date_cur).add(1, 'days').format()
		}
	}

    const handleMonthDayClick = (day, index) => {
		console.log(index, day)
        daySelected = day
        displayed = "detail"
	}

</script>
<div class="svcal__container" class:svcal--full={bexpanded}>
    <svg xmlns="http://www.w3.org/2000/svg" style="display:none;">
        <symbol fill="currentColor" viewBox="0 0 16 16" id="expand"><path fill-rule="evenodd" d="M5.828 10.172a.5.5 0 00-.707 0l-4.096 4.096V11.5a.5.5 0 00-1 0v3.975a.5.5 0 00.5.5H4.5a.5.5 0 000-1H1.732l4.096-4.096a.5.5 0 000-.707zm4.344-4.344a.5.5 0 00.707 0l4.096-4.096V4.5a.5.5 0 101 0V.525a.5.5 0 00-.5-.5H11.5a.5.5 0 000 1h2.768l-4.096 4.096a.5.5 0 000 .707z"></path></symbol>
        <symbol fill="currentColor" viewBox="0 0 16 16" id="contract"><path fill-rule="evenodd" d="M.172 15.828a.5.5 0 00.707 0l4.096-4.096V14.5a.5.5 0 101 0v-3.975a.5.5 0 00-.5-.5H1.5a.5.5 0 000 1h2.768L.172 15.121a.5.5 0 000 .707zM15.828.172a.5.5 0 00-.707 0l-4.096 4.096V1.5a.5.5 0 10-1 0v3.975a.5.5 0 00.5.5H14.5a.5.5 0 000-1h-2.768L15.828.879a.5.5 0 000-.707z"></path></symbol>
        <symbol fill="currentColor" viewBox="0 0 16 16" id="return"><path d="M5.921 11.9L1.353 8.62a.719.719 0 010-1.238L5.921 4.1A.716.716 0 017 4.719V6c1.5 0 6 0 7 8-2.5-4.5-7-4-7-4v1.281c0 .56-.606.898-1.079.62z"></path></symbol>
    </svg>
{#if displayed === "cal"}
    <div class="svcal__menu">
        <button on:click={()=>{bexpanded=!bexpanded}} class="svcal__button">
            {#if bexpanded}
            <svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em">
                <use xlink:href="#contract"></use>
            </svg>
            {:else}
            <svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em">
                <use xlink:href="#expand"></use>
            </svg>
            {/if}
        </button>
    </div>
    <div class="svcal__content svcal--month">
        {#if cal.days}
        <div class="svcal__dayname">Dimanche</div>
        <div class="svcal__dayname">Lundi</div>
        <div class="svcal__dayname">Mardi</div>
        <div class="svcal__dayname">Mercredi</div>
        <div class="svcal__dayname">Jeudi</div>
        <div class="svcal__dayname">Vendredi</div>
        <div class="svcal__dayname">Samedi</div>
        {#each cal.days as day, index}
        <div class="svcal__item" class:svcal--en={day.vis} on:click={handleMonthDayClick(day, index)}>{moment(day.date).format('DD')}</div>
        {/each}
        {/if}
    </div>
{/if}
{#if displayed === "detail"}
<DaySelected
    day={daySelected}
    on:esc={()=>{displayed = "cal"}}
/>
{/if}
</div>