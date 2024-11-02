<!-- src/components/ThemeSwitcher.svelte -->
<script>
    import { onMount, onDestroy } from 'svelte';

    let colorScheme = 'light'; // Default value

    // Function to set the color scheme
    const setColorScheme = (scheme) => {
        colorScheme = scheme;
        if (scheme === 'light dark') {
            // Automatic: Sync with system preferences
            const prefersDark = window.matchMedia("(prefers-color-scheme: dark)").matches;
            document.body.classList.toggle("dark-mode", prefersDark);
        } else {
            // Set specific light or dark mode
            document.body.classList.toggle("dark-mode", scheme === "dark");
        }
        localStorage.setItem('colorScheme', colorScheme);
    };

    // Listen for system theme changes when "Automatic" is selected
    const systemColorSchemeListener = (e) => {
        if (colorScheme === 'light dark') {
            document.body.classList.toggle("dark-mode", e.matches);
        }
    };

    // Use onMount to initialize theme and add system color scheme listener
    onMount(() => {
        const savedColorScheme = localStorage.getItem('colorScheme');
        if (savedColorScheme) {
            colorScheme = savedColorScheme;
        } else {
            const prefersDark = window.matchMedia("(prefers-color-scheme: dark)").matches;
            colorScheme = prefersDark ? 'dark' : 'light';
        }
        setColorScheme(colorScheme);

        // Listen to changes in the system color scheme
        const mediaQuery = window.matchMedia("(prefers-color-scheme: dark)");
        mediaQuery.addEventListener("change", systemColorSchemeListener);

        // Cleanup event listener on component destroy
        onDestroy(() => {
            mediaQuery.removeEventListener("change", systemColorSchemeListener);
        });
    });

    // Handle theme change from the select dropdown
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

<style>
    /* Additional styles for the theme switcher */
    .dark-mode {
        background-color: #121212; /* Dark mode background */
        color: white; /* Dark mode text color */
    }
</style>
