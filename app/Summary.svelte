<script>
    import { createEventDispatcher } from 'svelte'
    export let item;
    
    let dispatch = createEventDispatcher();

    function show_comments() {
       dispatch('showcomments', {
           item: item
       })
    }
</script>

<gridLayout columns="*, 50" rows="*">
    <stackLayout col="0" row="0" class="post-detail-section">
        <label class="post-title" textWrap="{true}">{item.title}</label>
        <stackLayout orientation="horizontal" class="domain-row">
            <label class="post-rank">{item.points}</label>
            <label class="post-domain">{item.domain}</label>
        </stackLayout>
    </stackLayout>
    <label col="1" row="0" class="post-comment-count" on:tap="{show_comments}">{item.comments_count}</label>
</gridLayout>

<style>
    .post-detail-section {
        padding: 10;
    }

    .post-title {
        color: #000000;
        font-weight: bold;
        margin-bottom: 5;
    }

    .post-domain {
        font-size: 10;
        margin-left: 5;
        vertical-align: center;
    }

    .post-rank {
        padding: 2 5;
        background-color: #e0e0d9;
        font-size: 11;
        border-radius: 2;
    }

    .post-comment-count {
        background-color: #ecece1;
        text-align: center;
        padding-top: 10;
        font-size: 17;
    }
</style>