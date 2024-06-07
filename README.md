# Resolução - Cartesi Rollups Code Challenge
1. Análise do código: percebemos que o código fonte continha uma função obfuscada em python e percebemos pela nomenclatura das variáveis que precisávamos enviar o ano do nascimento de Descartés (nós da comunidade Cartesi somos Cartesianos!)[^1] subtraído de um outro valor que seria o guess.
3. Engenharia reversa: decompilamos o código binário e procuramos por constantes que pudessem nos indicar qual era o valor secreto. Porém devido a uma grande quantidade de instruções, deixamos essa estratégia de lado temporariamente.[^2]
4. Força bruta: executamos o código binário num script local que testava vários valores para o guess, porém devido às mensagens de erro quando a guess estavam erradas tivemos dificuldade em visualizar o momento em que a função retornava verdadeiro. Então reduzimos o número de tentativas e conseguimos achar o valor correto.
5. Double-check na engenharia reversa: reanalisando o código decompilado, vimos que as instruções LOAD_CONST indicavam poucos valores a serem testados (1, 2, 3 e 51). Como o valor correto estava entre esses valores, nos tornamos confiantes da solução.
6. Envio da solução: enviamos o valor achado localmente para a aplicação Cartesi utilizando o formato apropriado e obtivemos nossa mensagem de sucesso em formato de notice: ![Tela de sucesso](./assets/success.png)
7. Verificação do desafio: para verificar a veracidade do desafio, vamos usar o determinismo das máquinas Cartesi 😈. Com o primeiro input sendo o válido, podemos utilizar o GraphQL playground da máquina para conseguirmos a prova da nossa computação[^3].

```GraphQL
query {
  notice(noticeIndex: 0, inputIndex: 0) {
    index
    input {
      index
    }
    payload
    proof {
      validity {
        inputIndexWithinEpoch
        outputIndexWithinInput
        outputHashesRootHash
        vouchersEpochRootHash
        noticesEpochRootHash
        machineStateHash
        outputHashInOutputHashesSiblings
        outputHashesInEpochSiblings
      }
      context
    }
  }
}
```
E o resultado dessa query se torna
```GraphQL
{
  "data": {
    "notice": {
      "index": 0,
      "input": {
        "index": 0
      },
      "payload": "0x436f6e67726174756c6174696f6e73203078663339666436653531616164383866366634636536616238383237323739636666666239323236362120596f75206861766520736f6c76656420746865206368616c6c656e676521",
      "proof": {
        "validity": {
          "inputIndexWithinEpoch": 0,
          "outputIndexWithinInput": 0,
          "outputHashesRootHash": "0x089f45d1e623b81c08c848fdf445b95dcea852a6c711a6bf4ff24262e7941b97",
          "vouchersEpochRootHash": "0x3082c1cf077237c6952ddd7da61f97b794351479d29d1cbd88edec2419f5ab8f",
          "noticesEpochRootHash": "0x307195a0e56c289d0104cb9bf6d57259ae6c10b8fb26213dfc178146f500be4d",
          "machineStateHash": "0x4bc7805d194e7c1da62b457899127f426e45f68d70c661f16351fbf62e8baee5",
          "outputHashInOutputHashesSiblings": [
            "0xae39ce8537aca75e2eff3e38c98011dfe934e700a0967732fc07b430dd656a23",
            "0x3fc9a15f5b4869c872f81087bb6104b7d63e6f9ab47f2c43f3535eae7172aa7f",
            "0x17d2dd614cddaa4d879276b11e0672c9560033d3e8453a1d045339d34ba601b9",
            "0xc37b8b13ca95166fb7af16988a70fcc90f38bf9126fd833da710a47fb37a55e6",
            "0x8e7a427fa943d9966b389f4f257173676090c6e95f43e2cb6d65f8758111e309",
            "0x30b0b9deb73e155c59740bacf14a6ff04b64bb8e201a506409c3fe381ca4ea90",
            "0xcd5deac729d0fdaccc441d09d7325f41586ba13c801b7eccae0f95d8f3933efe",
            "0xd8b96e5b7f6f459e9cb6a2f41bf276c7b85c10cd4662c04cbbb365434726c0a0",
            "0xc9695393027fb106a8153109ac516288a88b28a93817899460d6310b71cf1e61",
            "0x63e8806fa0d4b197a259e8c3ac28864268159d0ac85f8581ca28fa7d2c0c03eb",
            "0x91e3eee5ca7a3da2b3053c9770db73599fb149f620e3facef95e947c0ee860b7",
            "0x2122e31e4bbd2b7c783d79cc30f60c6238651da7f0726f767d22747264fdb046",
            "0xf7549f26cc70ed5e18baeb6c81bb0625cb95bb4019aeecd40774ee87ae29ec51",
            "0x7a71f6ee264c5d761379b3d7d617ca83677374b49d10aec50505ac087408ca89",
            "0x2b573c267a712a52e1d06421fe276a03efb1889f337201110fdc32a81f8e1524",
            "0x99af665835aabfdc6740c7e2c3791a31c3cdc9f5ab962f681b12fc092816a62f"
          ],
          "outputHashesInEpochSiblings": [
            "0x290decd9548b62a8d60345a988386fc84ba6bc95484008f6362f93160ef3e563",
            "0x633dc4d7da7256660a892f8f1604a44b5432649cc8ec5cb3ced4c4e6ac94dd1d",
            "0x890740a8eb06ce9be422cb8da5cdafc2b58c0a5e24036c578de2a433c828ff7d",
            "0x3b8ec09e026fdc305365dfc94e189a81b38c7597b3d941c279f042e8206e0bd8",
            "0xecd50eee38e386bd62be9bedb990706951b65fe053bd9d8a521af753d139e2da",
            "0xdefff6d330bb5403f63b14f33b578274160de3a50df4efecf0e0db73bcdd3da5",
            "0x617bdd11f7c0a11f49db22f629387a12da7596f9d1704d7465177c63d88ec7d7",
            "0x292c23a9aa1d8bea7e2435e555a4a60e379a5a35f3f452bae60121073fb6eead",
            "0xe1cea92ed99acdcb045a6726b2f87107e8a61620a232cf4d7d5b5766b3952e10",
            "0x7ad66c0a68c72cb89e4fb4303841966e4062a76ab97451e3b9fb526a5ceb7f82",
            "0xe026cc5a4aed3c22a58cbd3d2ac754c9352c5436f638042dca99034e83636516",
            "0x3d04cffd8b46a874edf5cfae63077de85f849a660426697b06a829c70dd1409c",
            "0xad676aa337a485e4728a0b240d92b3ef7b3c372d06d189322bfd5f61f1e7203e",
            "0xa2fca4a49658f9fab7aa63289c91b7c7b6c832a6d0e69334ff5b0a3483d09dab",
            "0x4ebfd9cd7bca2505f7bef59cc1c12ecc708fff26ae4af19abe852afe9e20c862",
            "0x2def10d13dd169f550f578bda343d9717a138562e0093b380a1120789d53cf10",
            "0x776a31db34a1a0a7caaf862cffdfff1789297ffadc380bd3d39281d340abd3ad",
            "0xe2e7610b87a5fdf3a72ebe271287d923ab990eefac64b6e59d79f8b7e08c46e3",
            "0x504364a5c6858bf98fff714ab5be9de19ed31a976860efbd0e772a2efe23e2e0",
            "0x4f05f4acb83f5b65168d9fef89d56d4d77b8944015e6b1eed81b0238e2d0dba3",
            "0x44a6d974c75b07423e1d6d33f481916fdd45830aea11b6347e700cd8b9f0767c",
            "0xedf260291f734ddac396a956127dde4c34c0cfb8d8052f88ac139658ccf2d507",
            "0x6075c657a105351e7f0fce53bc320113324a522e8fd52dc878c762551e01a46e",
            "0x6ca6a3f763a9395f7da16014725ca7ee17e4815c0ff8119bf33f273dee11833b",
            "0x1c25ef10ffeb3c7d08aa707d17286e0b0d3cbcb50f1bd3b6523b63ba3b52dd0f",
            "0xfffc43bd08273ccf135fd3cacbeef055418e09eb728d727c4d5d5c556cdea7e3",
            "0xc5ab8111456b1f28f3c7a0a604b4553ce905cb019c463ee159137af83c350b22",
            "0x0ff273fcbf4ae0f2bd88d6cf319ff4004f8d7dca70d4ced4e74d2c74139739e6",
            "0x7fa06ba11241ddd5efdc65d4e39c9f6991b74fd4b81b62230808216c876f827c",
            "0x7e275adf313a996c7e2950cac67caba02a5ff925ebf9906b58949f3e77aec5b9",
            "0x8f6162fa308d2b3a15dc33cffac85f13ab349173121645aedf00f471663108be",
            "0x78ccaaab73373552f207a63599de54d7d8d0c1805f86ce7da15818d09f4cff62"
          ]
        },
        "context": "0x0000000000000000000000000000000000000000000000000000000000000000"
      }
    }
  }
}
```

[^1]: https://www.reddit.com/r/cartesi/comments/1d483oa/cartesians_unite_vote_for_our_dapps_on_the_dapp/
[^2]: https://docs.python.org/3/library/dis.html
[^3]: https://docs.cartesi.io/cartesi-rollups/1.3/rollups-apis/graphql/queries/list_notices/
