<style scoped>
.blog {
  text-align: left;
  padding: 10px;
  height: 500px;
  overflow-y: auto;
}
</style>
<template>
  <div class="row">
    <div class="col-md-6">
      <div class="blog">
        <ul>
          <li>
            <a
              href="https://github.com/Vishwas1/crypto/blob/master/docs/README.md"
              target="_blank"
            >Conceitos básicos de criptografia</a>
            <ul>
              <li>Hashing</li>
              <li>Criptografia simétrica</li>
              <li>Criptografia assimétrica</li>
              <li>Assinatura digital</li>
              <!-- <li>Prova de conhecimento zero (de idade) [zk]</li> -->
            </ul>
          </li>
          <li>
            Foram usadas as seguintes bibliotecas
            <ul>
              <li>
                Hashing
                <ul>
                  <li>
                    <a href="https://www.npmjs.com/package/blakejs" target="_blank">Blakejs</a>
                  </li>
                  <li>
                    <a href="https://www.npmjs.com/package/sha.js" target="_blank">SHA js</a>
                  </li>
                </ul>
              </li>
              <li>
                Criptografia simétrica
                <ul>
                  <li>
                    <a href="https://www.npmjs.com/package/aes-js" target="_blank">Aes-js</a> com modo CTR
                  </li>
                </ul>
              </li>
              <li>
                Criptografia assimétrica
                <ul>
                  <li>
                    <a href="https://www.npmjs.com/package/tweetnacl" target="_blank">TweetNacl</a>
                  </li>
                  <li>
                    <a href="https://www.npmjs.com/package/ed2curve" target="_blank">Ed2Curve</a>
                  </li>
                </ul>
              </li>
            </ul>
          </li>
          <li>
            <a href="https://github.com/Alextnetto/crypto" target="_blank">Código fonte</a>
          </li>
        </ul>
      </div>
    </div>
    <div class="col-md-6">
      <p>
        <h5>Me apoie deixando uma <b>estrela</b> no repositório! </h5>
      </p>
      <div
        class="github-card"
        data-github="Alextnetto/crypto"
        data-width="400"
        data-height
        data-theme="default"
      ></div>
    </div>
  </div>
</template>

<script>
export default {
  name: "IntroductionPage",
  data() {
    return {};
  },
  created() {
    let ckeditor = document.createElement("script");
    ckeditor.setAttribute(
      "src",
      "//cdn.jsdelivr.net/github-cards/latest/widget.js"
    );
    document.head.appendChild(ckeditor);
  }
};
</script>