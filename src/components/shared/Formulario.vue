<template>
  <div>
    <p v-if="errors.length" class="erros">
      <b>Atenção!</b>
      <ul>
        <li v-for="error in errors">{{ error }}</li>
      </ul>
    </p>
  <div v-if="visivel" class="formulario">
    <form action="#" @submit="checkForm">
      <label for="nome">Nome:</label>
      <button id="primeiro-nome" v-on:click="pegarNome">Primeiro Nome: <span>{{ primeiroNome }}</span></button>
      <input type="text" name="nome" id="nome" v-model="nome">
      <label for="email">E-mail:</label>
      <input type="email" name="email" id="email" v-model="email">
      <label for="idade">Idade:</label>
      <input type="number" name="idade" id="idade" v-model="idade" max=60>
      <label for="celular">Celular:</label>
      <input type="number" name="celular" id="celular" v-model="celular">
      <label for="senha">Senha:</label>
      <input type="password" name="senha" id="senha" v-model="senha">
      <label for="confirma-senha">Confirme a senha:</label>
      <input type="password" name="confirma-senha" id="confirma-senha" v-model="confirmaSenha">
      <div class="retirar-validacao">
        <label for="retirar-validacao">Retirar Validação</label>
        <input type="checkbox" name="retirar-validacao" id="retirar-validacao" v-on:click="retirarValidacao">
      </div>
      <div class="enviar-limpar">
        <input type="submit" value="ENVIAR" v-on:click="alternarVisivel">
        <input type="reset" value="LIMPAR" id="limpar">
      </div>
    </form>
  </div>

    <div class="resumo" v-if="visivel === false">
      <p>Nome:
        <resultado class="resultado" :valor="nome"></resultado>
      </p>
      <p>Email:
        <resultado class="resultado" :valor="email"></resultado>
      </p>
      <p>Idade:
        <resultado class="resultado" :valor="idade"></resultado>
      </p>
      <p>Celular:
        <resultado class="resultado" :valor="celular"></resultado>
      </p>
      <p>Senha:
        <resultado class="resultado" :valor="senha"></resultado>
      </p>
      <p>Confirmação de Senha:
        <resultado class="resultado" :valor="confirmaSenha"></resultado>
      </p>
    </div>

  </div>
</template>

<script>

  const formulario = document.querySelector('.formulario');
  const nome = document.querySelector('#nome');
  const primeiroNome = document.querySelector('#pegar-nome');
  const email = document.querySelector('#email');
  const idade = document.querySelector('#idade');
  const celular = document.querySelector('#celular');
  const senha = document.querySelector('#senha');
  const confirmaSenha = document.querySelector('#confirma-senha');

  import Resultado from './Resultado.vue'

  export default {
    components: {
      'resultado': Resultado
    },
    data() {
      return{
        errors: [],
        nome: nome,
        email: email,
        idade: idade,
        celular: celular,
        senha: senha,
        confirmaSenha: confirmaSenha,
        primeiroNome: nome,
        visivel: true
    }
  },
    methods: {
      checkForm: function (e) {
        this.errors = [];
        if (!this.nome) this.errors.push("Nome é obrigatório.");
        if (this.nome.length > 20) this.errors.push("Nome tem mais de 20 caracteres.");
        if (!this.email) this.errors.push("E-mail  é obrigatório.");
        if (!this.idade) this.errors.push("Idade é obrigatório");
        if (!this.celular) this.errors.push("Celular é obrigatório");
        if (this.celular.length > 11 || this.celular.length < 11) this.errors.push("Celular tem mais de 11 números");
        if (!this.senha) this.errors.push("Senha é obrigatório");
        if (!this.confirmaSenha) this.errors.push("Confirmação de senha é obrigatório");
        if (this.confirmaSenha != this.senha) this.errors.push("Senha é diferente da confirmação");
        e.preventDefault();
      },
      retirarValidacao: function() {
        this.checkForm = '';
    },
      pegarNome: function() {
        this.primeiroNome = this.nome.split(' ')[0]
      },
      alternarVisivel: function() {
        if(this.confirmaSenha === this.senha && this.errors.length === 0) {
        return this.visivel = false;
      }
    }
  }
}
</script>
