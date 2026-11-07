<script lang="ts">
    import { m } from '#lib/paraglide/messages.js';
    import { Search, X } from '@lucide/svelte';

    let query = $state('');
</script>

<section>
    <article class="find">
        <article>
            <input bind:value={query} type="text" placeholder={m.search()} />
            <button
                id="clear"
                onclick={() => {
                    query = '';
                }}
                style:display={query == '' ? 'none' : 'flex'}
            >
                <X />
            </button>
            <button id="search"><Search /></button>
        </article>
    </article>
    <article class="view"></article>
    <article class="info"></article>
</section>

<style lang="scss">
    section {
        width: 100%;
        height: 100%;

        display: flex;
        flex-direction: column;
    }

    .find {
        width: 100%;
        height: 3rem;

        display: flex;
        align-items: center;
        justify-content: space-around;

        article {
            width: 50%;
            height: 2.25rem;

            position: relative;

            input {
                width: 100%;
                height: 100%;

                font-size: 0.85rem;
                padding: 0.25rem 4rem 0.25em 2rem;

                border-radius: 1.5rem;
                border: 1px solid grey;

                background: #00800005;

                outline: none;
            }

            button {
                all: unset;
                display: flex;
                align-items: center;
                flex-direction: space-around;

                color: grey;

                position: absolute;

                width: 2rem;
                height: 2rem;
            }

            #clear {
                top: 5%;
                right: 2rem;
            }

            #search {
                top: 5%;
                right: 0;
            }
        }
    }

    .view {
        width: 100%;
        height: calc(100% - 5.5rem);
    }

    .info {
        width: 100%;
        height: 2.5rem;

        border-top: 2px solid #008000;
        background: #00800005;
    }
</style>
