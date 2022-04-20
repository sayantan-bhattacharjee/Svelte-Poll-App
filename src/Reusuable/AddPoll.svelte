<script>
  import pollStore from '../Store/pollStore';
  import {createEventDispatcher} from 'svelte'
  import Button from '../Reusuable/Button.svelte'

  let dispatch = createEventDispatcher()
  let fields = { question: "", answerA: "", answerB: "" }
  let errors = { question: "", answerA: "", answerB: "" }
  let valid = false

  let data = [{
    id: 1,
    question: 'Python or Javascript',
    answerA: 'Python',
    answerB: 'JavaScript',
    voteA: 9,
    voteB: 15,
  }]

  const submitHandler = () => {
    let valid = true
    if(fields.question.trim().length < 10) {
      valid=false
      errors.question = 'Question must be atleast 10 character long'
    } else {
      errors.question = ''
    }
    if(fields.answerA.trim().length < 5) {
      valid=false
      errors.answerA = 'AnswerA must be atleast 5 character long'
    } else {
      errors.answerA = ''
    }if(fields.answerB.trim().length < 5) {
      valid=false
      errors.answerB = 'AnswerB must be atleast 10 character long'
    } else {
      errors.answerB = ''
    }

    if(valid){
      let poll ={...fields, voteA: 0, voteB: 0, id: Math.random() }
      // dispatch('addPoll', poll) 
      // console.log('valid', fields)
      pollStore.update(currentPolls => {
        return [poll, ...currentPolls]
      })

      dispatch('addPoll') 
    }
  }
</script>

<div class="AddPoll">
  <div class="container">
    <form class="row g-3" on:submit|preventDefault={submitHandler}>
      <div class="col-md-6">
        <label for="PollQuestion" class="form-label text-start w-100"
          >Question</label
        >
        <input
          type="text"
          placeholder ='Please Raise Your Question'
          class="form-control"
          id="PollQuestion"
          bind:value={fields.question}
        />
        <div class='error'>{errors.question}</div>
      </div>
      <div class="col-md-6">
        <label for="PollAnswerA" class="form-label text-start w-100"
          >PollAnswerA</label
        >
        <input
          type="text"
          placeholder ='AnswerA'
          class="form-control"
          id="PollAnswerA"
          bind:value={fields.answerA}
        />
        <div class='error'>{errors.answerA}</div>
      </div>
      <div class="col-md-6">
        <label for="PollAnswerB" class="form-label text-start w-100"
          >PollAnswerB</label
        >
        <input
          type="text"          
          placeholder ='AnswerB'
          class="form-control"
          id="PollAnswerB"
          bind:value={fields.answerB}
        />
        <div class='error'>{errors.answerB}</div>
      </div>
      <div class="col-12 ">
        <Button type="secondary" flat={true} inverse={true} class="btn btn-success px-5">Add Poll</Button>
      </div>
    </form>
  </div>
</div>

<style>
  .AddPoll {
    padding: 10px 0px;
  }
  .error {
    color: red;
    text-align: end;
    font-weight: bold;
    font-size: 12px;
  }
</style>
