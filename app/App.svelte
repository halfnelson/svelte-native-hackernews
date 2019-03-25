<page class="page">
    <actionBar title="Svelte HN" class="action-bar"></actionBar>
    <gridLayout rows="auto, *">
        <listView row="0" items="{items}" on:loadMoreItems={loadNextPage} height="100%" on:itemTap={on_show_article}>
            <Template let:item>
                <Summary item={item} on:showcomments={on_show_comments}></Summary>
            </Template>
        </listView>
        <activityIndicator row="0" busy="{loading}" />
    </gridLayout>
</page>
<style>
    .action-bar {
        background-color: #ff6600;
        color: #FFFFFF;
    }
    listView {
        background-color: #f6f6ef;
        color: #828282;
    }
</style>

<script>
    import { onMount } from 'svelte'
    import { Template } from 'svelte-native/components'
    import Summary from './Summary.svelte'

    let items = [];
    let page = 1;
    let loading = true;

    async function loadPage(page) {
        loading = true;
        return await fetch(`https://node-hnapi.herokuapp.com/news?page=${page}`)
            .then(r => r.json())
            .finally(loading = false);
    }

    async function refresh() {
        page = 1;
        items = await loadPage(1);
    }

    async function loadNextPage() {
        page = page + 1;
        items = items.concat(await loadPage(page));
    }

    function on_show_comments(e) {
        console.log('got show comment',e)
    }

    function on_show_article(e) {
        console.log('got show article', items[e.index])
    }

    onMount(refresh);

</script>