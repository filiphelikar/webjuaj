<script>
    import Input from "../components/input.svelte"

    export let currentModel
    let messages = [];

    const createMessage = (event) => {
        if (currentModel) {
            const message = event.detail;
            messages.push({text: message, from: "input"});
            messages = messages /*forces Svelte to rerender*/

            let promptMessages = messages.map(item => {
                return {
                    role: item.from === "input" ? "user" : "assistant",
                    content: item.text
                };
            });

            fetch('http://localhost:11434/api/chat', {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json'
                },
                body: JSON.stringify({
                    model: currentModel,
                    messages: promptMessages,
                    stream: false 
                })
            })
                .then(response => {
                    return response.json();
                })
                .then(data => {
                    messages.push({text: data.message.content, from: "ai"});
                    messages = messages /*forces Svelte to rerender*/
                })
        }
    }
</script>


<h2>new-chat:</h2>
<div class="main-div">
    {#each messages as message}
        <div class={message.from}>
            {message.text}
        </div>
    {/each}

</div>
<Input on:createMessage={createMessage}/>
<style>
    .input {
        margin: 20px;
        text-align: left;
        color: var(--color-text);
        background-color: var(--user-message-color);
        border-radius: 10px;
        width: fit-content;
        max-width: 85%;
        padding: 10px;
        -webkit-box-shadow: 0px 0px 7px 0px var(--user-message-color);
        -moz-box-shadow: 0px 0px 7px 0px var(--user-message-color);
        box-shadow: 0px 0px 7px 0px var(--user-message-color);
        word-wrap: break-word;
    }

    .ai {
        margin: 10px;
        text-align: left;
        color: var(--color-text);
        background-color: var(--message-color);
        border-radius: 10px;
        width: fit-content;
        max-width: 85%;
        padding: 10px;
        -webkit-box-shadow: 0px 0px 7px 0px var(--message-color);
        -moz-box-shadow: 0px 0px 7px 0px var(--message-color);
        box-shadow: 0px 0px 7px 0px var(--message-color);
        word-wrap: break-word;
    }

    h2 {
        position: relative;
        top: 60px;
        color: var(--color-text);
        text-align: center;

    }

    .main-div {
        position: relative;
        grid-template-columns: repeat(2, 1fr);
        width: 90%;
        max-width: 1100px;
        min-height: 200px;
        margin: 0 auto;
        margin-top: 80px;
        background-color: var(--main-color);
        border-radius: 10px;
        padding: 10px 0;
    }

    @media only screen and (max-width: 768px) {
        .main-div {
            min-height: 300px;
        }
    }
</style>