<template>
  <div>
    <p v-if="errors.length" class="erros">
      <b>Atenção!</b>
      <ul>
        <li v-for="(error, index) in errors" :key="index">{{ error }}</li>
      </ul>
    </p>
  <div class="helper">
    <a class="botao" @click="pegarNome">Primeiro Nome:</a> <span>{{ primeiroNome }}</span>
  </div>
  <div v-if="visivel === false" class="formulario">
    <form action="#" >
      <label for="nome">Nome:</label>
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
        <input type="checkbox" name="retirar-validacao" id="retirar-validacao" v-model="ignoreValidation">
      </div>
      <div class="enviar-limpar">
        <a class="botao" @click="checkForm">Enviar</a>
        <a class="botao" @click="reset">Limpar</a>
      </div>
    </form>
  </div>

    <div class="resumo" v-if="visivel === true">
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

  import Resultado from './Resultado.vue'

  export default {
    components: {
      'resultado': Resultado
    },
    data() {
      return{
        errors: [],
        nome: '',
        email: '',
        idade: '',
        celular: '',
        senha: '',
        confirmaSenha: '',
        primeiroNome: '',
        visivel: false,
        ignoreValidation: false,
    }
  },
    methods: {
      checkForm: function () {
        this.errors = [];
        if(!this.ignoreValidation) {
          if (!this.nome) this.errors.push("Nome é obrigatório.");
          if (this.nome.length > 20) this.errors.push("Nome tem mais de 20 caracteres.");
          if (!this.email) this.errors.push("E-mail  é obrigatório.");
          if (!this.idade) this.errors.push("Idade é obrigatório");
          if (!this.celular) this.errors.push("Celular é obrigatório");
          if (this.celular.length > 11) this.errors.push("Celular tem mais de 11 números");
          if (!this.senha) this.errors.push("Senha é obrigatório");
          if (!this.confirmaSenha) this.errors.push("Confirmação de senha é obrigatório");
          if (this.confirmaSenha != this.senha) this.errors.push("Senha é diferente da confirmação");
        }
        this.alternarVisivel();
      },
      pegarNome: function() {
        this.primeiroNome = this.nome.split(' ')[0]
      },
      alternarVisivel: function() {
        if(this.confirmaSenha === this.senha && this.errors.length === 0) {
          this.visivel = true;
        }
      },
      reset() {
        this.nome = '';
        this.email = '';
        this.idade = '';
        this.celular = '';
        this.senha = '';
        this.confirmaSenha = '';
        this.primeiroNome = '';
        this.ignoreValidation = false;
        this.errors =  [];
      }
  }
}
</script>
