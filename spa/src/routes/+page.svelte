<svelte:head>
    <title>SPA Cook</title>
</svelte:head>
<script lang="ts">
    import Titulo from "$lib/components/compartilhados/Titulo.svelte"
    import Tag from "$lib/components/compartilhados/Tag.svelte"
    import Categoria from "$lib/components/paginas/Categoria.svelte"

    import categorias from "$lib/json/categorias.json"

    import {beforeNavigate} from "$app/navigation"
    import { minhaLista } from "$lib/stores/minhaLista";


    beforeNavigate((navigation) => {
        if($minhaLista.length === 0 ){
            navigation.cancel()
        }
    })

</script>

<!-- <a href="/receitas">Ir para Receitas</a> -->
<!-- carrega uma pagina nova sem fazer uma requisiçao ao servidor -->

        <main>
            <div class="info">
                <Titulo tag='h1'>Ingredientes</Titulo>
                <p>Selecione abaixo os ingredientes que você deseja usar</p>
                <p>Considera-se que você tenha sal em casa, pimenta e água</p>
            </div>

            <ul class="categorias">
                {#each categorias as categoria (categoria.nome) }
                    <li>
                        <Categoria 
                        {categoria}
                        />
                    </li>
                {/each}
            </ul>

            <div class="buscar-receitas">
                <a href="/receitas">
                    <Tag ativa={true} tamanho="lg">Buscar Receitas!</Tag>
                </a>
            </div>
        </main>


<style>

    .info {
        margin-bottom: 3.375rem;
    }

    .info > p {
        line-height: 2rem;
    }
    .categorias {
        margin-bottom: 4.6875rem;

        display: flex;
        flex-wrap: wrap;
        justify-content: center;
        gap: 1.5rem;
    }

    .buscar-receitas {
        display: flex;
        justify-content: center;
    }

</style>