<script>
    import {fade, slide, scale} from 'svelte/transition';
    import {flip} from 'svelte/animate';
    // import {onMount, onDestroy} from 'svelte';
    import pollStore from "../Store/pollStore";
    import PollDetails from './PollDetails.svelte';

    // export let polls =[]

    // const unsub = pollStore.subscribe(data =>{
    //     polls = data
    // })

    // onMount(() => {
    //     console.log('component mounted')
    // });

    // onDestroy(() => {
    //     console.log('component destroyed')
    //     unsub();
    // })
</script>

<div class='poll_list container'>
    {#each $pollStore as polldata (polldata.id)}
        <div class="poll_crd_ht" in:fade out:scale|local animate:flip={{duration: 500}}>
            <!-- <PollDetails {polldata} on:vote/> -->
            <PollDetails {polldata} />
        </div>
    {/each}
</div>

<style>
    .poll_list {
        display: grid;
        grid-template-columns: repeat(4, 1fr);
        grid-column-gap: 25px
    }

    .poll_crd_ht {
        height: 280px;
        overflow: hidden;
    }

</style>