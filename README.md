# 🍅 Classificação da Qualidade de Tomates com Redes Neurais Convolucionais

## 📌 Sobre o Projeto

Este projeto tem como objetivo desenvolver um modelo de **Inteligência Artificial capaz de classificar tomates a partir de imagens**, utilizando Redes Neurais Convolucionais (CNN — *Convolutional Neural Networks*).

A aplicação utiliza técnicas de *Deep Learning* para identificar características visuais dos tomates e classificá-los em quatro categorias: danificado, velho, maduro e verde.

Além da classificação, o projeto permite capturar imagens diretamente pela webcam e coletar feedback do usuário sobre as previsões realizadas pelo modelo.

A iniciativa está relacionada ao uso de Inteligência Artificial na agricultura de precisão, contribuindo para o estudo de técnicas automatizadas de análise visual de alimentos.

## 🎯 Objetivos

- Desenvolver um modelo de classificação de imagens utilizando redes neurais convolucionais.
- Aplicar técnicas de pré-processamento de imagens para preparar os dados para o treinamento.
- Treinar uma rede neural para reconhecer diferentes condições visuais dos tomates.
- Realizar classificações a partir de imagens capturadas pela webcam.
- Coletar feedback do usuário para identificar previsões incorretas.
- Salvar imagens corrigidas em suas respectivas categorias para possibilitar a ampliação do conjunto de treinamento.

## 🧠 Classes de Classificação

O modelo trabalha com quatro categorias:

| Classe | Descrição |
|---|---|
| `damage` | Tomates com sinais visuais de danos. |
| `old` | Tomates com características visuais de envelhecimento. |
| `ripe` | Tomates visualmente maduros. |
| `unripe` | Tomates visualmente verdes ou não maduros. |

**Observação:** a classificação é baseada nas características visuais aprendidas durante o treinamento. O modelo não comprova a segurança alimentar do tomate nem determina, isoladamente, se ele está próprio para consumo.

## 🛠️ Tecnologias Utilizadas

- **Python:** linguagem utilizada no desenvolvimento.
- **TensorFlow:** biblioteca para treinamento e execução da rede neural.
- **Keras:** construção e configuração do modelo de Deep Learning.
- **NumPy:** manipulação de arrays e obtenção das classes previstas.
- **Matplotlib:** visualização das imagens classificadas.
- **Kaggle API:** download do conjunto de dados.
- **Google Colab:** ambiente de execução do notebook e acesso à webcam.

## 🗂️ Estrutura do Projeto

```text
classificacao-tomates/
│
├── main.ipynb          # Notebook de treinamento e classificação
├── README.md           # Documentação do projeto
└── requirements.txt    # Dependências do projeto (opcional)
```

O conjunto de imagens é baixado do Kaggle e extraído durante a execução do notebook.

## 📊 Conjunto de Dados

O projeto utiliza o conjunto de dados **Tomatoes Dataset**, disponibilizado no Kaggle.

Fonte: [enalis/tomatoes-dataset](https://www.kaggle.com/datasets/enalis/tomatoes-dataset)

Os dados são organizados em diretórios correspondentes às classes de classificação, permitindo que o Keras carregue automaticamente as imagens e seus respectivos rótulos.

### Pré-processamento

Antes de serem utilizadas no treinamento, as imagens passam pelas seguintes etapas:

1. **Redimensionamento:** todas as imagens são ajustadas para 150 × 150 pixels.
2. **Normalização:** os valores dos pixels são divididos por 255, convertendo-os para uma escala entre 0 e 1.
3. **Organização por classes:** as imagens são carregadas de acordo com a estrutura de diretórios do conjunto de dados.
4. **Agrupamento:** as imagens são processadas em lotes de 32 amostras.

Essas etapas padronizam a entrada da rede neural e facilitam o processamento dos dados.

## 🏗️ Arquitetura da Rede Neural

O modelo foi construído utilizando a API Sequential do Keras, com camadas convolucionais responsáveis pela extração de características visuais das imagens.

A arquitetura implementada é composta por:

| Camada | Configuração | Função |
|---|---|---|
| Conv2D | 32 filtros, kernel 3 × 3 | Extrai características visuais iniciais. |
| MaxPooling2D | Pooling 2 × 2 | Reduz as dimensões das representações. |
| Conv2D | 64 filtros, kernel 3 × 3 | Aprende características visuais mais complexas. |
| MaxPooling2D | Pooling 2 × 2 | Reduz novamente as dimensões espaciais. |
| Flatten | — | Transforma as representações em um vetor. |
| Dense | 128 neurônios | Aprende combinações das características extraídas. |
| Dense | 4 neurônios, Softmax | Produz as probabilidades das quatro classes. |

### Configuração do treinamento

O treinamento utiliza os seguintes parâmetros:

- **Otimizador:** Adam.
- **Função de perda:** Categorical Crossentropy.
- **Métrica:** Accuracy.
- **Número de épocas:** 10.
- **Tamanho das imagens:** 150 × 150 pixels.
- **Tamanho do lote:** 32 imagens.

O modelo aprende a associar as características visuais presentes nas imagens às respectivas categorias durante o treinamento.

## ⚙️ Como Executar o Projeto

### 1. Acesse o Google Colab

Abra o Google Colab e importe o arquivo `main.ipynb`.

Acesse: https://colab.research.google.com/

O projeto foi estruturado para execução nesse ambiente.

### 2. Configure o acesso ao Kaggle

Para baixar o conjunto de dados, é necessário configurar a autenticação da API do Kaggle.

1. Crie uma conta no Kaggle, caso ainda não possua uma.
2. Gere suas credenciais de API nas configurações da conta.
3. Obtenha o arquivo `kaggle.json`.
4. Envie o arquivo para o ambiente do Google Colab, conforme indicado no notebook.

**Importante:** não publique o arquivo `kaggle.json` no GitHub, pois ele contém credenciais de acesso.

### 3. Instale as dependências

O notebook instala a biblioteca Kaggle. As demais bibliotecas necessárias devem estar disponíveis no ambiente de execução.

Caso precise instalá-las manualmente, utilize:

```bash
pip install kaggle tensorflow numpy matplotlib
```

### 4. Execute o download dos dados

Execute as células responsáveis por baixar e extrair o conjunto de dados.

O notebook utiliza o identificador:

```text
enalis/tomatoes-dataset
```

Os arquivos são extraídos para o diretório configurado no código.

### 5. Treine o modelo

Execute as células de preparação dos dados, construção da arquitetura e treinamento.

O treinamento é realizado pela instrução:

```python
history = model.fit(
    train_generator,
    epochs=10
)
```

Ao final, o modelo estará disponível na memória da sessão para realizar classificações.

### 6. Realize uma classificação

Com o modelo treinado, execute a última célula do notebook.

A aplicação solicitará acesso à webcam para capturar uma imagem. Em seguida, a imagem será pré-processada e enviada ao modelo para obter a classe prevista.

O resultado será apresentado junto à imagem capturada.

### 7. Forneça feedback

Após a classificação, o usuário poderá informar se a previsão está correta.

Caso esteja incorreta, será possível indicar a classe correta. O código salva a imagem na pasta correspondente à categoria informada.

Essa funcionalidade permite organizar novas imagens para uso posterior no conjunto de treinamento.

**Nota:** o código atual salva a imagem corrigida, mas não realiza automaticamente um novo treinamento do modelo.

## 🔄 Fluxo de Funcionamento

```text
          Conjunto de dados
                  |
                  v
       Download e extração
                  |
                  v
      Pré-processamento das
             imagens
                  |
                  v
       Construção da CNN
                  |
                  v
        Treinamento do modelo
                  |
                  v
          Captura pela webcam
                  |
                  v
      Pré-processamento da foto
                  |
                  v
        Classificação da CNN
                  |
                  v
       Apresentação do resultado
                  |
                  v
          Feedback do usuário
                  |
                  v
       Correção da classificação
                  |
                  v
     Salvamento da imagem corrigida
```

## 📈 Avaliação do Modelo

O notebook utiliza a métrica *Accuracy* para acompanhar o desempenho durante o treinamento.

Entretanto, a implementação atual não possui uma etapa independente de validação ou teste. Por isso, os resultados obtidos durante o treinamento não devem ser interpretados como uma medida definitiva da capacidade de generalização do modelo.

Como evolução do projeto, recomenda-se:

- Separar os dados em conjuntos de treinamento, validação e teste.
- Acompanhar as curvas de perda e acurácia.
- Calcular precisão, revocação (*recall*) e F1-score por classe.
- Construir uma matriz de confusão para identificar os erros de classificação.
- Testar o modelo com imagens que não participaram do treinamento.
- Avaliar o desempenho em diferentes condições de iluminação e captura.

Essas melhorias permitirão avaliar de maneira mais confiável a capacidade do modelo de classificar novas imagens.

## 🚀 Possíveis Melhorias Futuras

- Implementar a separação automática dos dados em treinamento, validação e teste.
- Aplicar técnicas de aumento de dados (*data augmentation*).
- Comparar a CNN implementada com arquiteturas pré-treinadas, como MobileNetV2.
- Salvar o modelo treinado para reutilização sem a necessidade de treinar novamente a cada sessão.
- Criar uma interface web para facilitar a utilização da aplicação.
- Implementar um histórico das classificações realizadas.
- Automatizar a organização das imagens corrigidas e o processo de re treinamento.
- Investigar métricas adicionais para avaliar a qualidade das classificações.

## ⚠️ Limitações Conhecidas

- A execução depende da disponibilidade do conjunto de dados e da configuração correta do Kaggle.
- A captura de imagens utiliza recursos específicos do Google Colab.
- O modelo classifica imagens com base em padrões visuais aprendidos, podendo apresentar erros em condições diferentes das observadas durante o treinamento.
- O feedback do usuário não atualiza automaticamente os pesos da rede neural.
- O código não implementa uma avaliação independente com dados de teste.
- A classificação visual não substitui uma avaliação adequada da segurança alimentar.

## 👨‍💻 Autor

**Gustavo Henrique**

Tecnólogo em automação industrial integrado ao ensino médio - IFSP Suzano-SP.
Estudante de Análise e Desenvolvimento de Sistemas — FATEC Mogi das Cruzes.

TCC desenvolvido no IFSP — Rede Neural Convolucional para detecção automática de defeitos em hortaliças com Python. Apresentado em feiras científicas regionais.

Suzano -SP - 10/2024