# Projeto Final - Processamento de Imagens
**Identificação e Classificação de Lesões de Pele (9 Classes) utilizando Redes Neuronais Convolucionais**

**Equipe:** Anny Vitoria Costa

---

## 🧠 Descrição da Abordagem
Neste projeto, optou-se pela utilização da abordagem baseada em Redes Neuronais Convolucionais (CNNs) para resolver um problema complexo de classificação de imagens médicas. 

Para cumprir os requisitos do edital (utilização de uma arquitetura diferente das abordadas em aula), utilizou-se a **DenseNet121**. Esta arquitetura é conhecida pela sua eficiência no reaproveitamento de características extraídas, conectando todas as camadas da rede entre si, o que a torna ideal para identificar padrões subtis em lesões de pele.

A metodologia baseou-se em **Transfer Learning / Fine-Tuning**:
* Foram importados os pesos pré-treinados da `ImageNet`.
* A base convolucional foi congelada (`trainable = False`).
* A camada de saída original foi substituída por uma nova "cabeça" de classificação composta por: `GlobalAveragePooling2D`, `Dropout(0.5)` para evitar overfitting, e uma camada `Dense` final com 9 neurónios e função de ativação `Softmax`.
* O conjunto de treino passou por **Data Augmentation** (rotações de 20º, shifts horizontais/verticais e espelhamento horizontal) para aumentar a robustez do modelo.

---

## 🔗 Links Importantes
* **Repositório do Código (GitHub):** [Github](https://github.com/Annyyzinha/projeto-final-processamento-imagens)
* **Vídeo de Apresentação:** [Video]()
* **Dataset Utilizado:** [Skin Cancer ISIC (9 classes)](https://www.kaggle.com/datasets/nodoubttome/skin-cancer9-classesisic)

---

## 📊 Resultados e Métricas Obtidas
O modelo foi treinado durante 10 épocas, utilizando o otimizador Adam e a função de perda *Categorical Crossentropy*. 

Num cenário complexo com 9 doenças de pele visualmente muito semelhantes (onde o acerto aleatório seria de apenas ~11%), o modelo conseguiu extrair padrões de forma muito superior à aleatoriedade, alcançando as seguintes métricas globais no conjunto de teste:

* **Acurácia Global (Accuracy):** 38%
* **Macro Avg (F1-Score):** 34%
* **Weighted Avg (F1-Score):** 32%

### Destaques da Matriz de Confusão por Classe:
* **Vascular Lesion:** Excelente desempenho, atingindo **100% de Recall** e **75% de Precisão** (F1-Score: 0.86). O modelo não deixou escapar nenhum paciente com esta lesão.
* **Nevus:** Obteve o segundo melhor desempenho, com **75% de Recall** e **50% de Precisão** (F1-Score: 0.60).
* **Melanoma:** O modelo conseguiu identificar cerca de 44% dos casos reais (Recall 0.44), com uma precisão de 37%.
* **Squamous Cell Carcinoma / Seborrheic Keratosis:** O modelo revelou extrema dificuldade nestas classes (F1-Score 0.00), confundindo-as predominantemente com *Basal Cell Carcinoma* e *Pigmented Benign Keratosis*. Tal indica uma forte semelhança visual nas texturas e bordas destas lesões específicas, sugerindo a necessidade futura de mais dados ou de um treino mais prolongado com descongelamento de camadas mais profundas.

---

## 🛠️ Instruções de Uso
1. Aceda ao ficheiro `.ipynb` disponibilizado neste repositório e abra-o no **Google Colab**.
2. Altere o tipo de ambiente de execução para **GPU (T4)** para acelerar o processo.
3. Certifique-se de introduzir o seu Token da API do Kaggle na primeira célula do código (`os.environ['KAGGLE_API_TOKEN'] = "SEU_TOKEN"`).
4. Execute todas as células sequencialmente. O código irá transferir o dataset, preparar os geradores, aplicar o *transfer learning* na DenseNet121, efetuar o treino e gerar o Relatório de Classificação e a Matriz de Confusão automaticamente.

---
**Desenvolvido por:** Anny Vitoria Costa - UTFPR
