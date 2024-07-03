<script setup >
import { ref, defineExpose, toRefs } from "vue"

const props = defineProps({
  result: Array,
  show:Boolean
 
})

const {show, result} = toRefs (props)


</script>

<template>
    <div  v-if="show" >

    <h1 >RESULTADO</h1>
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