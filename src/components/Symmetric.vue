<style scoped>
.floatLeft {
  float: left;
}

.floatRight {
  float: right;
}
</style>

<template>
  <div class="row">
    <div class="col-md-12">
      <div class="row">
        <form action="#" class="col-md-6">
          <div class="form-group">
            <label class="floatLeft">Chave secreta:</label>
            <input type="text" v-model="secretkey" class="form-control" />
          </div>
          <div class="form-group">
            <label class="floatLeft">Mensagem original:</label>
            <textarea class="form-control" v-model="plaintext" rows="8" cols="50"></textarea>
          </div>
          <div class="form-group floatLeft">
            <button
              type="button"
              data-toggle="modal"
              ref="encrypt"
              @click="operation('encrypt')"
              class="btn btn-primary"
            >Criptografar</button>
          </div>
        </form>
        <form action="#" class="col-md-6">
          <div class="form-group">
            <label class="floatLeft">Mensagem criptografada:</label>
            <textarea class="form-control" v-model="ciphertext" rows="9" cols="50"></textarea>
          </div>
          <div class="form-group floatLeft">
            <button
              type="button"
              data-toggle="modal"
              ref="decrypt"
              @click="operation('decrypt')"
              class="btn btn-primary"
            >Descriptografar</button>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
import symmetric from "../crypto-lib/symmetric";

export default {
  name: "HashPage",
  data() {
    return {
      plaintext: "Essa é a sua mensagem secreta!",
      secretkey: "Senha1@",
      ciphertext: ""
    };
  },
  methods: {
    calculateHash: function() {
      return symmetric.sha256hashStr(this.plaintext);
    },
    operation: function(op) {
      try {
        let res = "";
        if (this.secretkey) {
          switch (op) {
            case "encrypt":
              if (this.plaintext != "") {
                res = symmetric.encryptData(this.secretkey, this.plaintext);
                this.ciphertext = res;
              } else {
                alert("Erro: Mensagem original vazia!");
              }
              break;
            case "decrypt":
              if (this.ciphertext != "") {
                res = symmetric.decryptData(this.secretkey, this.ciphertext);
                this.plaintext = res;
              } else {
                alert("Erro: Mensagem criptografada está vazia");
              }
              break;
            default:
          }
        } else {
          alert("Erro: Chave secreta ou Mensagem original está vazia");
        }
      } catch (e) {
        alert(`Erro : ${e.message}`);
      }
    }
  },
  computed: {
    // hashtext: function() {
    //   return this.calculateHash();
    // },
    // ciphertext: function() {
    //   return this.operation("encrypt");
    // },
  }
};
</script>


