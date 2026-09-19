# 📊 Regressão Espectral com Otimização por Validação Cruzada

Aplicação desenvolvida em Java com interface gráfica (Swing) para modelagem e comparação de técnicas de regressão aplicadas a dados espectrais (ex: NIR, MIR). O software implementa a **Regressão Linear Múltipla (RLM)** e suas variações baseadas em *Ensemble Learning* (**Bagging** e **Subagging**), com otimização rigorosa de hiperparâmetros para evitar *data leakage* (vazamento de dados).

**Autor:** Wagner Oliveira de Araujo  
**Versão:** 3.0  

---

## 🎯 Funcionalidades Principais

* **Três Técnicas de Regressão:**
  1. **RLM Simples:** Regressão Linear Múltipla padrão via pseudoinversa de Moore-Penrose.
  2. **RLM + Bagging:** *Ensemble* com reamostragem *com reposição* (Bootstrap completo).
  3. **RLM + Subagging:** *Ensemble* com reamostragem *sem reposição* (Subconjuntos aleatórios).
* **Otimização Cega:** Busca em grade (*Grid Search*) dos hiperparâmetros $m$ (número de bags) e $k$ (fração da subamostra) usando **Validação Cruzada 5-Fold** aplicada *exclusivamente* ao conjunto de calibração.
* **Avaliação Independente:** Teste final dos modelos otimizados em um conjunto de teste isolado.
* **Métricas de Avaliação:** RMSE, MAE, R² e Tempo de Execução.
* **Visualização:** Geração automática de gráficos comparativos (Valores Reais vs. Preditos) via JFreeChart.
* **Reprodutibilidade:** Uso de semente fixa (`Random(42)`) para garantir que os resultados sejam replicáveis.
* **Relatórios:** Exportação automática do log completo em arquivo `.txt` com *timestamp*.

---

## 🔬 Metodologia Implementada

O protocolo metodológico segue estritamente três etapas para garantir a validade estatística dos modelos:

1. **Carregamento:** Leitura e validação das matrizes de calibração (`Xcal`, `Ycal`) e teste (`Xteste`, `Yteste`).
2. **Otimização (CV 5-Fold):** O conjunto de calibração é dividido em 5 folds. Os hiperparâmetros $m$ e $k$ são testados combinando 4 folds para treino e 1 para validação. O melhor modelo é escolhido com base no menor RMSE-CV.
3. **Avaliação Final:** Os modelos treinados com os *melhores hiperparâmetros* (usando todo o conjunto de calibração) são avaliados no conjunto de teste independente.

---

## 📦 Dependências Externas

O projeto utiliza duas bibliotecas externas que devem estar no *classpath* durante a compilação e execução:

1. **EJML (Efficient Java Matrix Library):** Para operações matriciais e cálculo da pseudoinversa.
   * *Site:* [ejml.org](https://ejml.org/)
2. **JFreeChart:** Para geração dos gráficos de dispersão/linhas.
   * *Site:* [jfree.org/jfreechart](https://www.jfree.org/jfreechart/)

---

## 🛠️ Como Compilar e Executar

### Opção 1: Via Linha de Comando (javac / java)
Certifique-se de ter os arquivos `.jar` do EJML e JFreeChart na mesma pasta do código (ou ajuste o caminho).

```bash
# Compilar
javac -cp ".:ejml-core.jar:jfreechart.jar" BaggingOptimized.java

# Executar (Linux/Mac)
java -cp ".:ejml-core.jar:jfreechart.jar" itensvisuais.BaggingOptimized

# Executar (Windows)
java -cp ".;ejml-core.jar;jfreechart.jar" itensvisuais.BaggingOptimized