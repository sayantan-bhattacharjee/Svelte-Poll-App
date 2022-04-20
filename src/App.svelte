<script>
  import Header from "./Components/Header.svelte"
  import Footer from "./Components/Footer.svelte"
  import Tabs from "./Reusuable/Tabs.svelte"
  import AddPoll from "./Reusuable/AddPoll.svelte"
  import PollList from "./Reusuable/PollList.svelte"

  // Polls Tabs
  let items = ["Add Poll", "Poll List"]
  let activeItems = "Add Poll"

  const tabChange = (e) => {
    activeItems = e.detail
  }

  // let polls= [{
  //   id: 1,
  //   question: 'Python or Javascript',
  //   answerA: 'Python', 
  //   answerB: 'Javascript',
  //   voteA: 9,
  //   voteB: 15,
  // }]
  const handleAdd = (e) => {
    // const poll = e.detail;
    // polls = [poll, ...polls]
    // console.log(polls)
    activeItems='Poll List'
  }

  // const handleVote = (e) => {
  //   const {id, option} = e.detail;
  //   let updatedPolls = [...polls];
  //   let upVotedPolls = updatedPolls.find((poll) => poll.id == id);

  //   if (option === 'a'){
  //     upVotedPolls.voteA++;
  //   }
  //   if (option === 'b'){
  //     upVotedPolls.voteB++;
  //   }
  //   console.log(updatedPolls)
  //   polls = updatedPolls
  // }

</script>

<Header />
<main>
  <Tabs {items} {activeItems} on:tabchange={tabChange} />
  {#if activeItems === "Add Poll"}
    <AddPoll on:addPoll={handleAdd}/>
  {:else if activeItems === "Poll List"}
    <!-- <PollList on:vote={handleVote}/> -->
    <PollList/>
  {/if}
</main>
<Footer />

<style>
  main {
    text-align: center;
    padding: 20px 0px;
    background: gainsboro;
  }
</style>
