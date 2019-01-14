<template>
    <div class="componente">
        <h2>As Informações de Usuário</h2>
        <p>Vários detalhes...</p>
        <p>Nome do usuário: <strong>{{ inverterNome() }}</strong></p>
        <p>Idade do usuário: {{idade}}</p>
        <button @click="reiniciarNome">Reiniciar nome</button>
        <button @click="reiniciarFn()">Reiniciar Nome (Callback)</button> <!-- Two estrategies to talk with component father -->
    </div>
</template>

<script>
import barramento from '@/barramento'
export default {
    props: {
        nome: {
            type: String,
            default:'Anonimo'
        },
        reiniciarFn: Function,
        idade: Number
    }, 
    methods: {
        inverterNome() {
            return this.nome.split('').reverse().join('')
        },
        reiniciarNome() {
            const antigo = this.nome
            this.nome = 'Pedro'
            this.$emit('nomeMudou', {
                novo:this.nome,
                antigo
            }) // The simples way to emit an event 
        }
    },
    created() {
        barramento.quandoIdadeMudar( idade => {
            console.log('Entrou')
            this.idade = idade
        })
    }
    
}
</script>

<style scoped>
    .componente {
        flex: 1;
        background-color: #ec485f;
        color: #fff;
    }
</style>
