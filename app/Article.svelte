<script>
    import { closeModal } from 'svelte-native'
    import { isIOS } from 'tns-core-modules/platform'
    export let item
    export let showComments = false


    function toggle_comments() {
        showComments = !showComments;
    }
</script>

<frame>
    <page>
        <actionBar class="{showComments ? 'comments' : ''}" >
            {#if isIOS }
                <actionItem icon="~/chevron-left-dark.png" ios.position="left" on:tap="{closeModal}" />
            {:else}
                <navigationButton icon="res://chevron_left_dark" on:tap="{closeModal}"></navigationButton>
            {/if}

            <stackLayout>
                <label class="actiontitle {showComments ? 'comments' : ''}" text="{(showComments ? 'Comments' : 'Article')}"
                    on:tap="{toggle_comments}"></label>
            </stackLayout>

            <actionItem icon="~/message-square-dark.png" visibility="{ showComments ? 'collapse' : 'visible' }" />
            <actionItem icon="~/file-dark.png" visibility="{ showComments ? 'visible' : 'collapse' }" />

        </actionBar>
        {#if showComments}
        <label text="comments go here"></label>
    {:else}
        <webView src="{item.url}"></webView>
    {/if}
</page>
</frame>
<style>
    actionBar {
        background-color: #dddddd;
    }
    actionBar.comments {
        background-color: #ff6600;
    }

    .actiontitle {
        font-size: 25;
        color: #222222;
    }

    .actiontitle.comments {
        color: #FFFFFF;
    }
</style>