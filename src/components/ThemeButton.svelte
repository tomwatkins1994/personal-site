<script lang="ts">
    import { onMount } from "svelte";

    let darkMode = $state(false);
    let body: HTMLBodyElement;

    onMount(() => {
        darkMode = document.documentElement.classList.contains("dark");
        body = document.querySelector("body") as HTMLBodyElement;
    });

    function handleClick() {
        body.style.transition = "color .1s, background-color .3s";
        document.documentElement.classList.toggle("dark", !darkMode);
        localStorage.theme = darkMode ? "light" : "dark";
        darkMode = !darkMode;
    }
</script>

<button
    class="dark-mode-button"
    aria-label={`Switch to ${darkMode ? "light" : "dark"} mode`}
    onclick={handleClick}
>
</button>

<style>
    .dark-mode-button {
        height: 1.5rem;
        aspect-ratio: 1;
        background-image: url("../assets/moon.svg");
        cursor: pointer;
    }

    :global(:root.dark) .dark-mode-button {
        background-image: url("../assets/sun.svg");
    }
</style>
