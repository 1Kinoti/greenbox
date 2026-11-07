<script lang="ts">
    import '#lib/styles/reset.css';
    import '#lib/styles/fonts.css';
    import { page } from '$app/state';
    import { resolve } from '$app/paths';
    import type { Path } from '$app/types';
    import type { LayoutProps } from './$types';
    import { locales, localizeHref, setLocale } from '#lib/paraglide/runtime.js';

    import Bar from '#lib/pieces/Bar.svelte';
    import Nav from '#lib/pieces/Nav.svelte';

    let { children }: LayoutProps = $props();

    setLocale('en');
    // setLocale('zh-cn');
</script>

<svelte:head>
    <link rel="icon" href="/favicon.svg" />
</svelte:head>

<section>
    <header><Bar /></header>
    <main>
        <nav><Nav /></nav>
        <article>{@render children()}</article>
    </main>
</section>

<div style="display:none">
    {#each locales as locale (locale)}
        <a href={resolve(localizeHref(page.url.pathname, { locale }) as Path)}>{locale}</a>
    {/each}
</div>

<style>
    /* <style lang="scss"> */
    section {
        width: 100vw;
        height: 100vh;

        display: flex;
        flex-direction: column;

        font-family: var(--font-serif);

        header {
            width: 100%;
            height: 2.5rem;

            display: flex;

            border-bottom: 2px solid #008000;
            background: #00800005;
        }

        main {
            width: 100%;
            height: calc(100% - 2.5rem);

            display: flex;

            nav {
                width: 11rem;
                height: 100%;

                display: flex;
            }

            article {
                width: calc(100% - 11rem);
                height: 100%;

                display: flex;
            }
        }
    }
</style>
