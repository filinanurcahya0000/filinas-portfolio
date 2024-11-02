<script>
    import { onMount, onDestroy } from 'svelte';

    let colorScheme = 'light';

    const setColorScheme = (scheme) => {
        colorScheme = scheme;

        if (scheme === 'light dark') {
            // Automatic based on system preference
            const prefersDark = window.matchMedia("(prefers-color-scheme: dark)").matches;
            document.body.classList.toggle("dark-mode", prefersDark);
        } else {
            // Toggle dark-mode class based on selected scheme
            document.body.classList.toggle("dark-mode", scheme === "dark");
        }
        localStorage.setItem('colorScheme', colorScheme);
    };

    const systemColorSchemeListener = (e) => {
        if (colorScheme === 'light dark') {
            document.body.classList.toggle("dark-mode", e.matches);
        }
    };

    onMount(() => {
        const savedColorScheme = localStorage.getItem('colorScheme');
        colorScheme = savedColorScheme || (window.matchMedia("(prefers-color-scheme: dark)").matches ? 'dark' : 'light');
        setColorScheme(colorScheme);

        const mediaQuery = window.matchMedia("(prefers-color-scheme: dark)");
        mediaQuery.addEventListener("change", systemColorSchemeListener);

        onDestroy(() => {
            mediaQuery.removeEventListener("change", systemColorSchemeListener);
        });
    });

    const handleChange = (event) => {
        setColorScheme(event.target.value);
    };
</script>

<label class="color-scheme" style="position: absolute; top: 1rem; right: 1rem; font-size: 0.8rem;">
    Theme:
    <select bind:value={colorScheme} on:change={handleChange}>
        <option value="light">Light</option>
        <option value="dark">Dark</option>
        <option value="light dark">Automatic</option>
    </select>
</label>
