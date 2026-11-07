<script lang="ts">
    import { m } from '#lib/paraglide/messages.js';
    import { getCurrentWindow } from '@tauri-apps/api/window';
    import { Maximize, Minimize, Minus, X } from '@lucide/svelte';

    const iconSize = '1.25rem';
    let isFullScreen = $state(false);
    const appWindow = getCurrentWindow();

    const toggleFullScreen = () => {
        isFullScreen = !isFullScreen;
        return appWindow.toggleMaximize();
    };

    const dragOrMaximize = (e: MouseEvent) => {
        if (e.buttons === 1) {
            e.detail === 2 ? appWindow.toggleMaximize() : appWindow.startDragging();
        }
    };
</script>

<section>
    <h1>
        <button onmousedown={dragOrMaximize} tabindex="-1">{m.greenbox()}</button>
    </h1>
    <div>
        <button
            onclick={appWindow.minimize}
            aria-label={m.minimizeWindow()}
            title={m.minimizeWindow()}
        >
            <Minus size={iconSize} />
        </button>

        <button
            onclick={toggleFullScreen}
            aria-label={isFullScreen ? m.exitFullScreen() : m.enterFullScreen()}
            title={isFullScreen ? m.exitFullScreen() : m.enterFullScreen()}
        >
            {#if isFullScreen}
                <Minimize size={iconSize} />
            {:else}
                <Maximize size={iconSize} />
            {/if}
        </button>

        <button
            onclick={appWindow.close}
            aria-label={m.closeWindow()}
            title={m.closeWindow()}
            id="close"
        >
            <X size={iconSize} />
        </button>
    </div>
</section>

<style lang="scss">
    section {
        width: 100%;
        height: 100%;

        display: flex;
        align-items: center;
        justify-content: space-between;

        button {
            all: unset;
            cursor: pointer;
        }

        h1 {
            width: calc(100% - 7.5rem);
            height: 100%;

            display: flex;
            align-items: center;
            justify-content: space-between;

            color: #008000;

            button {
                width: 100%;
                height: 100%;

                cursor: grabbing;

                display: flex;
                align-items: center;

                padding-left: 1rem;

                font-weight: 400;
                font-size: 1.75rem;
                font-family: var(--font-cursive);
                font-family: var(--font-fantasy);
            }
        }

        div {
            width: 7.5rem;
            height: 100%;

            display: flex;
            align-items: center;
            justify-content: space-between;

            padding-bottom: 2px;

            button {
                width: 2.5rem;
                height: 2.5rem;

                display: flex;
                align-items: center;
                justify-content: space-around;
            }

            button:hover,
            button:focus,
            button:focus-visible {
                color: #00800090;
                background: #00800010;
            }

            #close:hover,
            #close:focus,
            #close:focus-visible {
                color: #800000;
                background: #80000010;
            }
        }
    }
</style>
