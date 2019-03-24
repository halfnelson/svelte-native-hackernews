<page class="page">
    <actionBar title="Svelte HN" icon="" class="action-bar"></actionBar>
    <gridLayout rows="auto, *">
        <listView row="0" items="{items}" on:loadMoreItems={loadNextPage} height="100%">
            <Template let:item>
                <Summary item={item}></Summary>
            </Template>
        </listView>
        <activityIndicator row="0" busy="{loading}" />
    </gridLayout>
</page>

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

    onMount(refresh);

</script>