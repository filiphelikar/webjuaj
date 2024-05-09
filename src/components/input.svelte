<script>
    import {createEventDispatcher} from 'svelte';

    const dispatch = createEventDispatcher();

    const sendMessage = () => {
        const input = document.getElementById("input");
        dispatch('createMessage', input.value);
        input.value = "";
    }

    const keyDown = (event) => {
        if (event.key === "Enter") {
            sendMessage()
        }
    }
</script>

<div>
    <input on:keydown={keyDown} id="input" type="text" placeholder="Aa">
    <button on:click={sendMessage}>send</button>
</div>

<style>
    div {
        position: fixed;
        bottom: 0;
        background-color: var(--header-color);
        width: 100%;
        padding: 10px 0;
        display: flex;
        justify-content: center;
    }

    input {
        border: none;
        border-radius: 30px;
        background-color: var(--main-color);
        min-width: 500px;
        height: 40px;
        color: var(--color-text);
        font-size: large;
        padding: 0 10px;
        word-wrap: break-word;
        margin-right: 10px;
        display: inline-block;
    }

    button {
        align-items: center;
        background-clip: padding-box;
        background-color: #fa6400;
        border: 1px solid transparent;
        border-radius: .25rem;
        box-shadow: rgba(0, 0, 0, 0.02) 0 1px 3px 0;
        box-sizing: border-box;
        color: #fff;
        cursor: pointer;
        font-size: 15px;
        font-weight: 600;
        justify-content: center;
        line-height: 1.25;
        min-height: 2.1rem;
        padding: 0 20px;
        text-decoration: none;
        transition: all 250ms;
        user-select: none;
        -webkit-user-select: none;
        touch-action: manipulation;
        width: auto;
        -webkit-appearance: none;
        -moz-appearance: none;
        appearance: none;
        display: inline-block;
    }

    button:hover,
    button:focus {
        background-color: #fb8332;
        box-shadow: rgba(0, 0, 0, 0.1) 0 4px 12px;
    }

    button:hover {
        transform: translateY(-1px);
    }

    button:active {
        background-color: #c85000;
        box-shadow: rgba(0, 0, 0, .06) 0 2px 4px;
        transform: translateY(0);
    }

    @media only screen and (max-width: 768px) {
        input {
            min-width: 200px;
            height: 35px;
        }
    }
</style>