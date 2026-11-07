<script lang="ts">
    import { page } from '$app/state';
    import { m } from '#lib/paraglide/messages.js';
    import { Settings, UserPlus, Users, UserX, Wallet, Send, ChevronRight } from '@lucide/svelte';

    const iconSize = '1.25rem';

    const isActive = $derived.by(() => {
        let path = page.url.pathname.split('/')[1];
        return {
            recruitment:
                path == 'requests' ||
                path == 'applications' ||
                path == 'interviews' ||
                path == 'onboarding',
            employees:
                path == '' ||
                path == 'work' ||
                path == 'leave' ||
                path == 'injury' ||
                path == 'discipline',
            separation: path == 'separation' || path == 'notice' || path == 'clearance',
            payroll: path == 'payroll',
            messaging: path == 'messaging',
            work: path == 'work',
            leave: path == 'leave',
            injury: path == 'injury',
            discipline: path == 'discipline',
            requests: path == 'requests',
            applications: path == 'applications',
            interviews: path == 'interviews',
            onboarding: path == 'onboarding',
            notice: path == 'notice',
            clearance: path == 'clearance',
        };
    });
</script>

<section>
    <ul>
        <li>
            <a href="/" class:active={isActive.employees}>
                <span class="icon"><Users size={iconSize} /></span>
                <span class="text">{m.employees()}</span>
            </a>
            <ol>
                <li>
                    <a href="/work" class:active={isActive.work}>
                        <span class="icon"><ChevronRight /></span>
                        <span class="text">{m.work()}</span>
                    </a>
                </li>
                <li>
                    <a href="/leave" class:active={isActive.leave}>
                        <span class="icon"><ChevronRight /></span>
                        <span class="text">{m.leave()}</span>
                    </a>
                </li>
                <li>
                    <a href="/injury" class:active={isActive.injury}>
                        <span class="icon"><ChevronRight /></span>
                        <span class="text">{m.injury()}</span>
                    </a>
                </li>
                <li>
                    <a href="/discipline" class:active={isActive.discipline}>
                        <span class="icon"><ChevronRight /></span>
                        <span class="text">{m.discipline()}</span>
                    </a>
                </li>
            </ol>
        </li>
        <li>
            <a href="/requests" class:active={isActive.recruitment}>
                <span class="icon"><UserPlus size={iconSize} /></span>
                <span class="text">{m.recruitment()}</span>
            </a>
            <ol>
                <li>
                    <a href="/requests" class:active={isActive.requests}>
                        <span class="icon"><ChevronRight /></span>
                        <span class="text">{m.requests()}</span>
                    </a>
                </li>
                <li>
                    <a href="/applications" class:active={isActive.applications}>
                        <span class="icon"><ChevronRight /></span>
                        <span class="text">{m.applications()}</span>
                    </a>
                </li>
                <li>
                    <a href="/interviews" class:active={isActive.interviews}>
                        <span class="icon"><ChevronRight /></span>
                        <span class="text">{m.interviews()}</span>
                    </a>
                </li>
                <li>
                    <a href="/onboarding" class:active={isActive.onboarding}>
                        <span class="icon"><ChevronRight /></span>
                        <span class="text">{m.onboarding()}</span>
                    </a>
                </li>
            </ol>
        </li>
        <li>
            <a href="/separation" class:active={isActive.separation}>
                <span class="icon"><UserX size={iconSize} /></span>
                <span class="text">{m.separation()}</span>
            </a>
            <ol>
                <li>
                    <a href="/notice" class:active={isActive.notice}>
                        <span class="icon"><ChevronRight /></span>
                        <span class="text">{m.notice()}</span>
                    </a>
                </li>
                <li>
                    <a href="/clearance" class:active={isActive.clearance}>
                        <span class="icon"><ChevronRight /></span>
                        <span class="text">{m.clearance()}</span>
                    </a>
                </li>
            </ol>
        </li>
        <li>
            <a href="/payroll" class:active={isActive.payroll}>
                <span class="icon"><Wallet size={iconSize} /></span>
                <span class="text">{m.payroll()}</span>
            </a>
        </li>
        <li>
            <a href="/messaging" class:active={isActive.messaging}>
                <span class="icon"><Send size={iconSize} /></span>
                <span class="text">{m.messaging()}</span>
            </a>
        </li>
    </ul>
    <footer>
        <a href="/settings"><Settings /></a>
    </footer>
</section>

<style lang="scss">
    section {
        width: 100%;
        height: 100%;

        display: flex;
        flex-direction: column;

        ul,
        ol {
            list-style: none;
            padding: 0;
        }

        ul {
            width: 100%;
            height: calc(100% - 2.5rem);

            padding-top: 3rem;

            background: #00800020;
        }

        ul > li {
            width: 100%;

            margin-bottom: 1px;

            a {
                height: 2.5rem;
                width: 100%;

                display: flex;
                align-items: center;

                padding-left: 0.5rem;

                color: #000000;
                text-decoration: none;

                .text {
                    font-size: 0.95rem;
                }

                .icon {
                    height: 2.5rem;
                    width: 2.5rem;

                    display: flex;
                    align-items: center;
                    justify-content: space-around;
                }
            }

            a:hover,
            a:focus {
                color: #008000;
                background: #00800015;

                outline: none;
            }

            a.active {
                .icon {
                    color: #008000;
                }

                .text {
                    color: #008000;
                    border-bottom: 2px solid #008000;
                }
            }
        }

        ol > li {
            width: 100%;

            a {
                height: 2rem;

                transition: padding-left 0.3s ease-in-out;
            }

            a.active {
                color: #008000;

                padding-left: 2rem;

                .text {
                    border: none;
                }
            }
        }

        footer {
            width: 100%;
            height: 2.5rem;

            border-top: 2px solid #008000;
            background: #00800005;

            padding-left: 0.5rem;

            display: flex;
            flex-direction: column;

            a {
                all: unset;
                cursor: pointer;

                width: 2.5rem;
                height: 2.5rem;

                display: flex;
                align-items: center;
                justify-content: space-around;
            }

            a:hover {
                color: #008000;
            }
        }
    }
</style>
