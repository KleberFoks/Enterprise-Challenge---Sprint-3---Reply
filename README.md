# Enterprise Challenge – Sprint 3

**Aluno:** Kleber Foks – **RM562225**

## 📌 Introdução

Este projeto faz parte do Enterprise Challenge em parceria com a Hermes Reply.
O objetivo da Sprint 3 foi:

1. Modelar um banco de dados relacional para armazenar dados de sensores, campos, plantios e colheitas.
2. Criar um modelo básico de Machine Learning capaz de prever a produtividade agrícola (`YIELD_KG_PER_HA`) a partir de variáveis simuladas.

---

## 🗄️ Modelagem do Banco de Dados

### DER

<img width="1086" height="607" alt="der_model" src="https://github.com/user-attachments/assets/b8023549-7d4b-4027-b6d2-49b8b5bc9cb9" />

### Descrição das principais tabelas

* **SENSOR\_TYPES**: tipos de sensores e unidade de medida.
* **SENSORS**: sensores físicos instalados.
* **FIELDS**: campos agrícolas (talhões).
* **CROPS**: culturas (soja, milho, trigo).
* **PLANTINGS**: plantios em cada campo/cultura.
* **HARVESTS**: colheitas e produtividade obtida.
* **SENSOR\_INSTALLATIONS**: histórico de instalação de sensores em campos.
* **READINGS**: leituras numéricas dos sensores.

### Scripts

* `sql/create_schema.sql` → criação do schema completo com tabelas, PK/FK, constraints e views.
* Views criadas:

  * `VW_ACTIVE_INSTALLATIONS` → mostra sensores ainda ativos.
  * `VW_READINGS_ENRICHED` → junta leituras com tipo de sensor e campo.

---

## 📊 Dados Utilizados

Não havia dados reais suficientes, então foi criado um **dataset sintético** em CSV com **1200 registros**.

* Variáveis simuladas:

  * Área do campo
  * Cultura (soja, milho, trigo)
  * Data de plantio
  * Densidade de sementes
  * Temperatura média
  * Umidade média
  * pH do solo
  * Chuva total
  * NDVI médio (índice de vegetação)
* Variável alvo:

  * `YIELD_KG_PER_HA` (produtividade agrícola em kg/ha)

O CSV é gerado automaticamente pelo notebook `ml/model_previsao_safra.ipynb` e salvo em `data/dataset_safra_simulada.csv`.

---

## 🤖 Machine Learning

No notebook foram testados **4 modelos de regressão**:

1. Regressão Linear
2. Random Forest
3. XGBoost Regressor
4. Rede Neural (MLPRegressor)

### Principais métricas (teste)

| Modelo            | R²    | RMSE  | MAE   |
| ----------------- | ----- | ----- | ----- |
| **XGBoost**       | 0.919 | 365.3 | 275.3 |
| Random Forest     | 0.915 | 372.9 | 277.7 |
| Linear Regression | 0.896 | 413.3 | 320.7 |
| MLP Regressor     | 0.883 | 437.1 | 329.8 |

### Visualização – XGBoost

<img width="580" height="455" alt="XGB_REAL_X_PREVISTO" src="https://github.com/user-attachments/assets/8d041a95-20b4-42ff-b616-73ff2ed57a1f" />

---

## ✅ Conclusão

* O banco de dados foi estruturado para armazenar leituras de sensores e informações agrícolas de forma normalizada e escalável.
* O dataset sintético gerado atendeu à exigência de ter mais de 500 registros por sensor/plantio.
* Foram treinados quatro modelos de regressão. O **XGBoost** obteve o melhor desempenho, com R² ≈ 0,92, sendo selecionado como o modelo final.
* A análise mostrou que variáveis ambientais e de plantio têm relação não linear com a produtividade, e modelos baseados em árvores capturaram melhor essa complexidade.

---

## ▶️ Vídeo

LINK [Enterprise Challenge Sprint 3 Reply](https://youtu.be/MQdEH-NsO7s)

---

## 📂 Estrutura do Repositório

```
/docs
   der.png
   xgb_real_vs_previsto.png
/sql
   create_schema.sql
/data
   dataset_safra_simulada.csv
/ml
   model_previsao_safra.ipynb
README.md
```
