<style>
</style>

<page>
    <actionBar title="Svelte Demo" />
    <scrollView>
        <stackLayout>
            {#each demos as demo}
                <button
                    text={demo.name}
                    on:tap={() => {
                        goToDemo(demo.component);
                    }} />
            {/each}
        </stackLayout>
    </scrollView>
</page>

<script lang="typescript">
    import { navigate } from 'svelte-native';
    import { onMount } from 'svelte';
    import { demos } from '../../demo-snippets/svelte/install';
    function goToDemo(component) {
        navigate({
            page: component,
            animated: true,
            transition: {
                name: 'slideLeft',
                duration: 200,
                curve: 'ease'
            }
        });
    }
    onMount(() => {
        if (isDevelopment) {
            const Development = demos.find(({ name }) => name === 'Development');
            if (Development) {
                setTimeout(() => {
                    navigate({
                        page: Development.component,
                        animated: false
                    });
                }, 0);
            }
        }
    });
</script>