<style scoped>
.floatLeft {
  float: left;
}
.fullWidth {
  width: 100%;
}
.fullbody {
  width: 500px;
}
</style>
<template>
  <div class="asymmetric">
    <div class="col-md-12">
      <div>
        <b-card no-body>
          <b-tabs card vertical nav-wrapper-class="w-30">
            <b-tab title="Par de chaves" active>
              <b-card-text>
                <div class="row">
                  <form action="#" class="col-md-12">
                    <div class="form-group floatLeft">
                      <button
                        type="button"
                        class="btn btn-primary"
                        @click="generatekp()"
                      >Gerar par de chaves</button>
                    </div>
                  </form>
                </div>
                <div class="row">
                  <form action="#" class="col-md-12">
                    <div class="form-group">
                      <table class="table table-bordered">
                        <tr>
                          <th>Chave pública de quem envia</th>
                          <td>
                            <input type="text" style="width:100%" v-model="senderPublicKey" disabled />
                          </td>
                        </tr>
                        <tr>
                          <th>Chave privada de quem envia</th>
                          <td>
                            <input type="text" style="width:100%" v-model="senderPrivateKey" disabled />
                          </td>
                        </tr>
                      </table>
                      <table class="table table-bordered">
                        <tr>
                          <th>Chave pública de quem recebe</th>
                          <td>
                            <input type="text" style="width:100%" v-model="recipientPublicKey" disabled />
                          </td>
                        </tr>
                        <tr>
                          <th>Chave privada de quem recebe</th>
                          <td>
                            <input type="text" style="width:100%" v-model="recipientPrivateKey" disabled />
                          </td>
                        </tr>
                      </table>
                    </div>
                  </form>
                </div>
              </b-card-text>
            </b-tab>
            <b-tab title="Encriptar">
              <b-card-text>
                <div class="row">
                  <form action="#" class="col-md-6">
                    <div class="form-group">
                      <label class="floatLeft">Mensagem original:</label>
                      <textarea class="form-control" v-model="plaintext" rows="8" cols="50"></textarea>
                    </div>
                    <div class="form-group">
                      <label class="floatLeft">Chave pública de quem recebe:</label>
                      <input type="text" v-model="recipientPublicKey" class="form-control" />
                    </div>
                    <div class="form-group floatLeft">
                      <button
                        type="button"
                        data-toggle="modal"
                        @click="operation('encrypt')"
                        class="btn btn-primary"
                      >Criptografar</button>
                    </div>
                  </form>
                  <form action="#" class="col-md-6">
                    <div class="form-group">
                      <label class="floatLeft">Mensagem criptografada:</label>
                      <textarea class="form-control" v-model="cipherText" rows="8" cols="50"></textarea>
                    </div>
                  </form>
                </div>
              </b-card-text>
            </b-tab>
            <b-tab title="Desencriptar">
              <b-card-text>
                <div class="row">
                  <form action="#" class="col-md-6">
                    <div class="form-group">
                      <label class="floatLeft">Mensagem criptografada:</label>
                      <textarea class="form-control" v-model="cipherText" rows="8" cols="50"></textarea>
                    </div>
                    <div class="form-group">
                      <label class="floatLeft">Chave privada de quem recebe:</label>
                      <input type="text" v-model="recipientPrivateKey" class="form-control" />
                    </div>
                    <div class="form-group floatLeft">
                      <button
                        type="button"
                        data-toggle="modal"
                        @click="operation('decrypt')"
                        class="btn btn-primary"
                      >Descriptografar</button>
                    </div>
                  </form>
                  <form action="#" class="col-md-6">
                    <div class="form-group">
                      <label class="floatLeft">Mensagem original:</label>
                      <textarea class="form-control" v-model="decryptPlaintext" rows="8" cols="50"></textarea>
                    </div>
                  </form>
                </div>
              </b-card-text>
            </b-tab>
            <b-tab title="Assinar">
              <b-card-text>
                <div class="row">
                  <form action="#" class="col-md-6">
                    <div class="form-group">
                      <label class="floatLeft">Mensagem original:</label>
                      <textarea class="form-control" v-model="plaintext" rows="8" cols="50"></textarea>
                    </div>
                    <div class="form-group">
                      <label class="floatLeft">Chave privada de quem envia:</label>
                      <input type="text" v-model="senderPrivateKey" class="form-control" />
                    </div>
                    <div class="form-group floatLeft">
                      <button
                        type="button"
                        data-toggle="modal"
                        @click="dsOperation('sign')"
                        class="btn btn-primary"
                      >Assinar</button>
                    </div>
                  </form>
                  <form action="#" class="col-md-6">
                    <div class="form-group">
                      <label class="floatLeft">Mensagem assinada digitalmente:</label>
                      <textarea class="form-control" v-model="signedMessage" rows="8" cols="50"></textarea>
                    </div>
                  </form>
                </div>
              </b-card-text>
            </b-tab>
            <b-tab title="Verificar">
              <b-card-text>
                <div class="row">
                  <form action="#" class="col-md-12">
                    <div class="row">
                      <div class="form-group col-md-6">
                        <label class="floatLeft">Mensagem assinada digitalmente:</label>
                        <textarea class="form-control" v-model="signedMessage" rows="8" cols="50"></textarea>
                      </div>
                      <div class="form-group col-md-6">
                        <label class="floatLeft">Mensagem original:</label>
                        <textarea class="form-control" v-model="plaintext" rows="8" cols="50"></textarea>
                      </div>
                    </div>
                    <div class="row">
                      <div class="form-group col-md-6">
                        <label class="floatLeft">Chave pública de quem envia:</label>
                        <input type="text" v-model="senderPublicKey" class="form-control" />
                      </div>
                      <div class="form-group col-md-6">
                        <button
                          type="button"
                          data-toggle="modal"
                          @click="dsOperation('verify')"
                          class="btn btn-primary floatLeft"
                        >Verificar</button>
                      </div>
                    </div>
                  </form>
                </div>
              </b-card-text>
            </b-tab>
          </b-tabs>
        </b-card>
      </div>
    </div>
  </div>
</template>

<script>
const asymmetric = require("../crypto-lib/asymmetric");
export default {
  name: "AssymetricPage",
  components: {},
  data() {
    return {
      plaintext: "Essa é a sua mensagem secreta!",
      recipientPublicKey: "",
      recipientPrivateKey: "",
      cipherText: "",
      decryptPlaintext: "",
      senderPrivateKey: "",
      signedMessage: "",
      senderPublicKey: ""
    };
  },
  created() {},
  methods: {
    generatekp: function() {
      const recipientKeys = asymmetric.generateKeyPair();
      this.recipientPublicKey = recipientKeys.publicKey;
      this.recipientPrivateKey = recipientKeys.secretKey;

      const senderKeys = asymmetric.generateKeyPair();
      this.senderPublicKey = senderKeys.publicKey;
      this.senderPrivateKey = senderKeys.secretKey;
    },
    operation: function(op) {
      try {
        let res = "";
        switch (op) {
          case "encrypt":
            if (this.recipientPublicKey != "" && this.plaintext != "") {
              res = asymmetric.encrypt(this.plaintext, this.recipientPublicKey);
              this.cipherText = JSON.stringify(res);
            } else {
              alert("Error: Plaintext or recipeint's public key is empty");
            }
            break;
          case "decrypt":
            if (this.cipherText != {}) {
              res = asymmetric.decrypt(
                this.recipientPrivateKey,
                JSON.parse(this.cipherText)
              );
              this.decryptPlaintext = JSON.stringify(res);
            } else {
              alert("Error: Ciphertext is empty");
            }
            break;
          default:
        }
      } catch (e) {
        alert(`Error : ${e.message}`);
      }
    },
    dsOperation: function(op) {
      try {
        let res = "";
        switch (op) {
          case "sign":
            if (this.senderPrivateKey != "" && this.plaintext != "") {
              res = asymmetric.sign(this.plaintext, this.senderPrivateKey);
              this.signedMessage = res;
            } else {
              alert("Error: Plaintext or recipeint's public key is empty");
            }
            break;
          case "verify":
            if (
              this.signedMessage != "" &&
              this.plaintext != "" &&
              this.senderPublicKey != ""
            ) {
              res = asymmetric.verify(
                this.plaintext,
                this.signedMessage,
                this.senderPublicKey
              );
              alert(res);
            } else {
              alert("Error: Ciphertext is empty");
            }
            break;
          default:
        }
      } catch (e) {
        alert(`Error : ${e.message}`);
      }
    }
  }
};
</script>
