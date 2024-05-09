<script>
    import {createEventDispatcher} from 'svelte';

    const dispatch = createEventDispatcher();
    let icon = "🌃"

    function changeMode() {
        dispatch('changeColorMode');

        if (icon === "🌃") {
            icon = "🏙"
        } else {
            icon = "🌃"
        }
    }

    let models = []

    fetch('http://localhost:11434/api/tags')
        .then(response => {
            return response.json();
        })
        .then(data => {
            data.models.forEach(element => {
                models.push(element.model)
            });
            models = models
        });

    const changeModel = (event) => {
        if (event.target.value !== "none") {
            let model = event.target.value
            dispatch("modelChange", model)
        }
    }

</script>

<div>
    <button class="new-chat">new-chat</button>
    <h1>Web-Ju-Aj</h1>
    <button class="theme" on:click={changeMode}>{icon}</button>
    <select on:change={changeModel} name="" id="select">
        <option value="none">none</option>
        {#each models as model}
            <option value={model}>{model}</option>
        {/each}
    </select>
</div>

<style>
    div {
        z-index: 1000;
        position: fixed;
        background-color: var(--header-color);
        width: 100%;
        height: 50px;
        color: var(--color-text);
        text-align: center;
    }

    h1 {
        display: inline-block;
        font-size: 20px;
        margin-top: 10px;
    }

    select {
        position: absolute;
        top: 9px;
        right: 200px;
        background-color: var(--header-color);
        color: var(--color-text);
        border-radius: 3px;
        padding: 7px;
    }

    select:hover {
        top: 8px;
    }

    .new-chat {
        align-items: center;
        background-clip: padding-box;
        background-color: #fa6400;
        border: 1px solid transparent;
        border-radius: .25rem;
        box-shadow: rgba(0, 0, 0, 0.02) 0 1px 3px 0;
        box-sizing: border-box;
        color: #fff;
        cursor: pointer;
        display: inline-flex;
        font-size: 15px;
        font-weight: 600;
        justify-content: center;
        line-height: 1.25;
        margin: 0;
        min-height: 2.1rem;
        padding: 5px;
        text-decoration: none;
        transition: all 250ms;
        user-select: none;
        -webkit-user-select: none;
        touch-action: manipulation;
        vertical-align: baseline;
        width: auto;
        position: absolute;
        left: 200px;
        top: 8px;
        -webkit-appearance: none;
        -moz-appearance: none;
        appearance: none;
    }

    .new-chat:hover,
    .new-chat:focus {
        background-color: #fb8332;
        box-shadow: rgba(0, 0, 0, 0.1) 0 4px 12px;
    }

    .new-chat:hover {
        transform: translateY(-1px);
    }

    .new-chat:active {
        background-color: #c85000;
        box-shadow: rgba(0, 0, 0, .06) 0 2px 4px;
        transform: translateY(0);
    }

    .theme {
        border: none;
        border-radius: 0;
        background-color: var(--header-color);
        position: relative;
        display: inline-block;
        font-size: 30px;
        top: 6px;
        cursor: pointer;
    }

    @media only screen and (max-width: 768px) {
        select {
            position: absolute;
            top: 15px;
            right: 10px;
            background-color: var(--header-color);
            color: var(--color-text);
            border-radius: 3px;
            padding: 7px;
            font-size: 13px;
        }

        select:hover {
            top: 15px;
        }

        .new-chat {
            left: 10px;
            top: 8px;
        }
    }
</style>