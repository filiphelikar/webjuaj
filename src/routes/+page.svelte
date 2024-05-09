<script>
    import Header from "../components/header.svelte"
    import Main from "../components/main.svelte"

    const darkTheme = "--background-color: rgb(26, 26, 26); --header-color: rgb(34, 34, 34); --color-text: rgb(190, 190, 190); --main-color:rgb(22, 22, 22); --user-message-color: rgb(63, 0, 136); --message-color: rgb(0, 136, 125);"
    const lightTheme = "--background-color: rgb(229, 229, 229); --header-color: rgb(221, 221, 221); --color-text: rgb(65, 65, 65); --main-color:rgb(233, 233, 233); --user-message-color: rgb(167, 90, 255); --message-color: rgb(0, 181, 212);"
    let currentTheme = darkTheme

    const changeMode = () => {
        if (currentTheme === darkTheme) {
            currentTheme = lightTheme
        } else {
            currentTheme = darkTheme
        }
    }

    let model = ""

</script>

<div style={currentTheme}>
    <Header on:modelChange={(event) => {model = event.detail}} on:changeColorMode={changeMode}/>
    <Main currentModel={model}/>
</div>

<style>
    div {
        font-family: "Nunito", sans-serif;
        background-color: var(--background-color);
        width: 100%;
        min-height: 100vh;
        height: fit-content;
        padding-bottom: 60px;
    }
</style>