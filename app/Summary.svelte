<script>
    export let item;
</script>

<gridLayout columns="*, auto">
    <stackLayout col="0">
        <label class="post-title">{item.title}</label>
        <label class="post-domain">{item.domain}</label>
    </stackLayout>
    <label col="1" class="post-comment-count">{item.comments_count}</label>
</gridLayout>