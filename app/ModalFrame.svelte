<frame bind:this="{frame}"></frame>
<script>
    import { onMount } from 'svelte'
    import { navigate } from 'svelte-native'
    export let page;
    export let props;
    let frame;

    onMount(()=>{
        navigate({
            page: page,
            props: props,
            frame: frame,
        });
    })
</script>