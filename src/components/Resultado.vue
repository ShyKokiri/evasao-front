<script>
import { ref, defineExpose } from "vue"



export default {

    setup() {

        const result = ref([
            {
                ano: 2010,
                taxaSucesso: 50,
                taxaEvasao: 50,
            },
            {
                ano: 2010,
                taxaSucesso: 50,
                taxaEvasao: 50,
            },
        ])

        return { result }
    }
}
</script>

<template>
    <div>

    <h1>RESULTADO</h1>
        <table>
            <tr>
                <th>
                    Ano
                </th>
                <th>
                    Taxa de Sucesso
                </th>
                <th>
                    Taxa de Evasão
                </th>
            </tr>

            <tr v-for="(r, index) in result" :key="index">
                <td>
                    {{r.ano}}
                </td>
                <td>
                    {{r.taxaSucesso}}
                </td>
                <td>
                    {{r.taxaEvasao}}
                </td>
            </tr>


        </table>

    </div>
</template>
<style>
table{
    border:1px solid white
}
th{
 border:1px solid white;
 padding: 10px;
}
td{
 border:1px solid white;
 padding: 10px;
}
</style>