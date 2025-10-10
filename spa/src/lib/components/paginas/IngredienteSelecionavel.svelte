<!-- especialização de componentes  -->
<script lang="ts">
    // import { createEventDispatcher } from 'svelte';
    import Tag from '../compartilhados/Tag.svelte';
    import { minhaLista } from "$lib/stores/minhaLista";


    // const dispatch = createEventDispatcher<{
    //     adicionarIngrediente: string,
    //     remover: string
    // }>();

    export let ingrediente: string;

    $: selecionado = $minhaLista.includes(ingrediente);

    function aoClicar(){

        if (!selecionado){
            // dispatch('adicionarIngrediente', ingrediente)
            // $minhaLista = [...$minhaLista, ingrediente]
            minhaLista.update((valor) => [...valor, ingrediente])
        }else{
            // dispatch('remover', ingrediente)
            // $minhaLista = $minhaLista.filter(
            //     (item) => item !== ingrediente
            // )
            minhaLista.update((valor) => valor.filter(
                (item) => item !== ingrediente
            ))
        }
    }
</script>

<button on:click={aoClicar}>
    <Tag ativa={selecionado}>{ingrediente}</Tag>
</button>

<style>
    button{
        cursor: pointer;
    }
</style>