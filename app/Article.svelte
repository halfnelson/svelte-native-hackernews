<script>
    import { closeModal } from 'svelte-native'

    export let item
    export let showComments = false


    function toggle_comments() {
        showComments = !showComments;
    }
</script>

<page>
    <actionBar backgroundColor="{showComments ? '#ff6600' : '#DDDDDD'}"
        class="action-bar {showComments ? 'comments' : ''}">
        <navigationButton text="Back" android.systemIcon="ic_menu_back" on:tap="{closeModal}"></navigationButton>
        <stackLayout>
            <label class="actiontitle" text="{(showComments ? 'Comments' : 'Article')}"
                on:tap="{toggle_comments}"></label>
        </stackLayout>
    </actionBar>
    {#if showComments}
        <label text="comments go here"></label>
    {:else}
        <webView src="{item.url}"></webView>
    {/if}
</page>

<style>
    .actiontitle {
        font-size: 40;
        color: red;
    }
</style>