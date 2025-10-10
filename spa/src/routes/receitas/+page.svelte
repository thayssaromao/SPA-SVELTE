<svelte:head>
    <title>SPA Cook | Receitas</title>
</svelte:head>

<script lang="ts">
    import Titulo from "$lib/components/compartilhados/Titulo.svelte"
    import Receita from "$lib/components/receitas/Receita.svelte"
    import { minhaLista } from "$lib/stores/minhaLista";
    import Tag from "$lib/components/compartilhados/Tag.svelte"

    import receitas from "$lib/json/receitas.json"

    $: receitasFiltradas = receitas.filter((receita) => (
        receita.ingredientes.some((ingrediente) => (
            $minhaLista.includes(ingrediente)
        ))
    ))
</script>

<main>
    <Titulo tag='h1'>Receitas</Titulo>

    <div class="info">
        <p class="verde">
            Resultados Encontrados: {receitasFiltradas.length}
        </p>

        <ul class="receitas">
            {#each receitasFiltradas as receita (receita.nome)}
                <li>
                    <Receita {receita}/>
                </li>
            {/each}
        </ul>
    </div>
</main>

<div class="buscar-receitas">
    <a href="/">
        <Tag ativa={true} tamanho="lg">Voltar</Tag>
    </a>
</div>
 
<style>

       .buscar-receitas {
        display: flex;
        justify-content: center;
    }
        .info {
        margin-bottom: 4.375rem;
    }

    .info > p {
        line-height: 2rem;
    }

    .info > p.verde {
        color: var(--verde);
    }

    .receitas {
        text-align: start;
        margin-bottom: 3.75rem;

        display: flex;
        flex-wrap: wrap;
        justify-content: center;
        padding-top: 60px;
        gap: 1.5rem;
    }
</style>