<h1 align="center">🔬 Classificação de Lesões de Pele com CNNs</h1>

<p align="center">
  <img src="https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white" alt="Python" />
  <img src="https://img.shields.io/badge/TensorFlow-FF6F00?style=for-the-badge&logo=tensorflow&logoColor=white" alt="TensorFlow" />
  <img src="https://img.shields.io/badge/Keras-D00000?style=for-the-badge&logo=Keras&logoColor=white" alt="Keras" />
  <img src="https://img.shields.io/badge/Google_Colab-F9AB00?style=for-the-badge&logo=googlecolab&logoColor=white" alt="Google Colab" />
</p>

> **Projeto Final de Processamento de Imagens** > Identificação e Classificação de 9 tipos distintos de lesões de pele (incluindo Melanoma) utilizando a arquitetura **DenseNet121**.

**Equipe:** Anny Vitoria Costa - UTFPR  

---

## 🔗 Links Importantes

- 💻 **Repositório do Código:** [GitHub](https://github.com/Annyyzinha/projeto-final-processamento-imagens)
- 🎥 **Vídeo de Apresentação:** [Clique aqui para assistir]([https://youtu.be/4JhbA8_G_U4])
- 📁 **Dataset Utilizado:** [Skin Cancer ISIC (9 classes) no Kaggle](https://www.kaggle.com/datasets/nodoubttome/skin-cancer9-classesisic)

---

## 🧠 Descrição da Abordagem

Para resolver este problema complexo de classificação de imagens médicas e cumprir os requisitos do edital (utilização de uma arquitetura diferente das abordadas em aula), optou-se pela **DenseNet121**. Esta arquitetura é reconhecida pela sua eficiência no reaproveitamento de características extraídas, conectando todas as camadas da rede entre si, o que a torna ideal para identificar padrões subtis nas bordas e texturas das lesões.

A metodologia baseou-se em **Transfer Learning / Fine-Tuning**:
1. Importação dos pesos pré-treinados da `ImageNet`.
2. Congelamento da base convolucional (`trainable = False`).
3. Substituição da camada de saída original por uma nova "cabeça" de classificação: `GlobalAveragePooling2D`, `Dropout(0.5)` (para evitar *overfitting*) e uma camada `Dense` final com 9 neurónios e função de ativação `Softmax`.
4. Aplicação de **Data Augmentation** no conjunto de treino (rotações de 20º, deslocamentos horizontais/verticais e espelhamento) para aumentar a robustez do modelo.

---

## 📊 Resultados e Métricas Obtidas

Num cenário médico altamente complexo com 9 doenças de pele visualmente muito semelhantes (onde o acerto aleatório seria de apenas ~11%), o modelo treinado por 10 épocas alcançou os seguintes resultados globais no conjunto de teste:

| Métrica | Valor Obtido |
| :--- | :---: |
| **Acurácia Global (Accuracy)** | **38%** |
| **Macro Avg (F1-Score)** | **34%** |
| **Weighted Avg (F1-Score)** | **32%** |

### 🎯 Destaques da Matriz de Confusão por Classe:

* **Vascular Lesion:** Excelente desempenho, atingindo **100% de Recall** e **75% de Precisão** (F1-Score: 0.86). O modelo não deixou escapar nenhum paciente com esta lesão.
* **Nevus:** Obteve o segundo melhor desempenho, com **75% de Recall** e **50% de Precisão** (F1-Score: 0.60).
* **Melanoma:** O modelo conseguiu identificar cerca de 44% dos casos reais (Recall 0.44), com uma precisão de 37%.
* **Squamous Cell Carcinoma:** O modelo revelou extrema dificuldade nesta classe (F1-Score 0.00), confundindo-a predominantemente com *Basal Cell Carcinoma* e *Pigmented Benign Keratosis*. Isto sublinha a forte semelhança visual nas texturas destas lesões, sugerindo a necessidade futura de um conjunto de dados mais vasto ou do descongelamento de camadas mais profundas (*Fine-Tuning* avançado).

---

## 🛠️ Instruções de Uso

Para reproduzir este projeto, siga os passos abaixo:

1. Aceda ao ficheiro `.ipynb` disponibilizado neste repositório e abra-o no **Google Colab**.
2. No menu do Colab, altere o tipo de ambiente de execução para **GPU (T4)** para acelerar significativamente o processamento.
3. Insira o seu Token da API do Kaggle na primeira célula do código:
   ```python
   os.environ['KAGGLE_API_TOKEN'] = "COLOQUE_O_SEU_TOKEN_AQUI"
   ```
4. Execute todas as células sequencialmente. O código irá automaticamente:
  * Baixar o dataset.
  * Preparar os geradores de imagem.
  * Construir a arquitetura DenseNet121.
  * Treinar a rede neural.
  * Gerar o Relatório de Classificação e a Matriz de Confusão na tela final.
---
**Desenvolvido por:** Anny Vitoria Costa - UTFPR
