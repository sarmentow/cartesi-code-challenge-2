# Cartesi Rollups Code Challenge

## Descrição

Este desafio de código é parte da masterclass do @cartesiproject no Brasil, realizada no Inteli. Os participantes devem documentar todo o processo em um README e compartilhar um vídeo no Twitter|X.

## Instruções do Desafio

1.  **Encontrar os Valores Corretos**:
    
    -   Utilize o código fornecido para identificar o valor correto que deve ser adivinhado (guess), bem como outro valor que advém de uma "charada" (birth_year_minus_the_guess). Assim que você conseguir gerar o output correto, mostre-o no explorer que roda na rota: http://localhost:8080/explorer/, faça o "decode" da payload (hex) e mostre a string gerada. Corra! Você precisa ser o primeiro a postar no Twitter|X juntamente com um README.md e um vídeo refazendo os inputs até o decode da string para ganhar o prêmio.

2.  **Documentar o Processo**:
    
    -   Crie um README documentando cada passo que você tomou para encontrar o guess correto. Inclua como você utilizou as funções notice, report e inspect durante o processo. Se possível, use referências para a documentação da Cartesi: https://docs.cartesi.io/.

3.  **Postagem no Twitter|X**:
    
    -   Faça uma postagem no Twitter|X com um vídeo demonstrando a resolução do desafio e o link para o README.md com a explicação. Use o template de mensagem fornecido abaixo e sinta-se à vontade para comentar sobre a experiência da masterclass.


## Template de Mensagem
```text
Estou participando da masterclass da @cartesiproject no Brasil, que está acontecendo no Inteli. 
Aqui está um vídeo demonstrando a resolução do code challenge apresentado hoje. Acesse o link [hyperlink], para ver o README onde explico como resolvi esse desafio. #RollupWithCartesi #CartesiMasterclass
```

## Dicas

-   Você pode utilizar o nonodo para testar mais rapidamente. Nesse caso, o endereço a ser utilizado no `cartesi send` é: 0x70ac08179605AF2D9e75782b8DEcDD3c22aA4D0C
-   Em modo de produção, você pode utilizar o endereço padrão: 0xab7528bb862fb57e8a2bcd567a2e929a0be56a5e

## Passo a Passo

### 1. Configuração do Ambiente

1.  Clone o repositório:
    
```bash
git clone https://github.com/henriquemarlon/cartesi-code-challenge-2.git
```

### 2. Rodando o Código

```bash
cd challenge
cartesi build
cartesi run
```

### 3. Interaja com o dApp:

```bash
cartesi send generic \
    --dapp=<endereço-do-dapp> \
    --chain-id=31337 \
    --rpc-url=http://127.0.0.1:8545 \
    --mnemonic-passphrase='test test test test test test test test test test test junk' \
    --input='{"guess": <valor-aqui>, "birth_year_minus_the_guess": <valor-aqui>}'
```

Envie quantas inputs achar necessário para encontrar os valores certos!

### 4. Encontrando o Guess

Leia o código!
Hint 3: O output esperado é um notice! ;)

### 5. Postagem no Twitter

Grave um vídeo demonstrando o processo e poste no Twitter|X utilizando o template fornecido, junto a um link para um README.md com a explicação da resolução.

## Observações Finais

Boa sorte, Cartesians!