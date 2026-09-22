# Minha Primeira Rede Neural: Classificador de Categoria de Usuário com TensorFlow.js

Rede neural simples, construída com [TensorFlow.js](https://www.tensorflow.org/js) (`@tensorflow/tfjs-node`), que prevê a categoria de um usuário (`premium`, `medium` ou `basic`) a partir de idade, cor e localização.

Projeto de estudo para entender na prática os fundamentos de uma rede neural: camadas densas, ativação ReLU/softmax, loss, backpropagation e treinamento com epochs.

## Como funciona

1. **Entrada**: cada pessoa é transformada em um vetor de 7 números — idade normalizada (0 a 1) + cor em one-hot (3 posições) + localização em one-hot (3 posições).
2. **Modelo**: uma rede sequencial com duas camadas:
   - Camada oculta com 80 neurônios e ativação `relu`
   - Camada de saída com 3 neurônios (um por categoria) e ativação `softmax`, retornando as probabilidades de cada classe
3. **Treinamento**: otimizador `adam`, loss `categoricalCrossentropy`, 100 epochs, com shuffle dos dados a cada rodada.
4. **Predição**: dado um novo usuário (já normalizado no mesmo padrão do treino), o modelo retorna a probabilidade de cada categoria, ordenadas da mais provável para a menos provável.

## Tecnologias

- Node.js
- [@tensorflow/tfjs-node](https://www.npmjs.com/package/@tensorflow/tfjs-node)

## Instalação

```bash
npm install
```

## Uso

```bash
node index.js
```

Saída esperada (exemplo):

```
premium (72.15%)
medium (19.42%)
basic (8.43%)
```

## Estrutura do dado de entrada

| Posição | Significado                  |
|---------|-------------------------------|
| 0       | Idade normalizada             |
| 1       | Cor: azul                     |
| 2       | Cor: vermelho                 |
| 3       | Cor: verde                    |
| 4       | Localização: São Paulo        |
| 5       | Localização: Rio              |
| 6       | Localização: Curitiba         |

A idade é normalizada com base no min/max do dataset de treino: `(idade - idade_min) / (idade_max - idade_min)`.

## Limitações conhecidas

- **Dataset de treino muito pequeno** (apenas 3 exemplos): a rede tende a memorizar em vez de generalizar. Para um cenário real, é necessário um volume bem maior de dados.
- **Normalização e encoding manuais**: o vetor de entrada de uma pessoa nova é montado à mão, o que é propenso a erro de digitação (ex: marcar a cor errada). Idealmente isso deveria ser automatizado por uma função de encoding.
- **80 neurônios para 3 exemplos** é super-dimensionado; ideal para poucos dados é uma rede menor.

## Próximos passos sugeridos

- [ ] Automatizar normalização e one-hot encoding
- [ ] Ampliar o dataset de treino
- [ ] Separar dados em treino/validação
- [ ] Persistir o modelo treinado em disco (`model.save`)

## Licença

MIT
