<script>
  import {createEventDispatcher} from 'svelte';
  import Button from "../Reusuable/Button.svelte";
  import pollStore from '../Store/pollStore';
  import Card from "./Card.svelte";

  export let polldata;
  const dispatch = createEventDispatcher();

  $: totalVotes = polldata.voteA + polldata.voteB;
  $: percentA = Math.floor(100 / totalVotes * polldata.voteA )
  $: percentB = Math.floor(100 / totalVotes * polldata.voteB )

  const handleVote = (option, id) => {
    // const {id, option} = e.detail;

    pollStore.update(currentPolls => {
      let updatedPolls = [...currentPolls];
      let upVotedPolls = updatedPolls.find((poll) => poll.id == id);

      if (option === 'a'){
        upVotedPolls.voteA++;
      }
      if (option === 'b'){
        upVotedPolls.voteB++;
      }
      return updatedPolls
    });
  };

  const handleDelete = (id) => {
    pollStore.update(currentPolls => {
      return currentPolls.filter(poll => poll.id !== id);
    });
  }

</script> 

<Card>
  <div class="poll_details w-100">
    <h3 class="text-start text_threedot">{polldata.question}</h3>
    <h6 class="text-start text_threedot">Total Votes: {totalVotes}</h6>
    <div class="answer" on:click={()=> handleVote('a', polldata.id)}>
      <div class="text-start percent percent-A" style="width: {percentA}%">
        <span class="text_threedot">
          {polldata.answerA} ({polldata.voteA})
        </span>
      </div>
    </div>
    <div class="answer" on:click={()=> handleVote('b', polldata.id)}>
      <div class="text-start percent percent-B" style="width: {percentB}%">
        <span class="text_threedot">
          {polldata.answerB} ({polldata.voteB})
        </span>
      </div>
    </div>
    <div class="delete">
      <Button flat={true} on:click={() => handleDelete(polldata.id)}>Delete</Button>
    </div>
  </div>
</Card>

<style>
  /* .poll_details {
    background-color: #c19898;
    padding: 20px;
    border-radius: 10px;
  } */
  h3 {
    margin: 0 auto;
    color: #555;
    padding-bottom: 10px;
  }
  .text_threedot {
    text-overflow: ellipsis;
    white-space: nowrap;
    display: block;
    overflow: hidden;
  }

  h6 {
    margin-top: 6px;
    font-size: 12px;
    color: #785b5b;
    margin-bottom: 20px;
  }
  .answer {
    background: #fafafa;
    cursor: pointer;
    margin: 10px auto;
    position: relative;
  }
  .answer:hover {
    opacity: 0.6;
  }
  span {
    display: inline-block;
    padding: 10px 20px;
  }
  .percent {
    height: 100%;
    /* position: absolute; */
    box-sizing: border-box;
  }
  .percent-A {
    border-left: 4px solid #d91b42;
    background: rgba(217,27,66,0.2 );
  }
  
  .percent-B {
    border-left: 4px solid #45c496;
    background: rgba(69,196,150,0.2 );
  }
  .delete {
    margin-top: 30px;
    text-align: center;
  }
</style>
