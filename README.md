![Imagem de Capa Artigo Moderno Linkedin Mensagem Motivacional Amarela  (2)](https://github.com/user-attachments/assets/97b644b8-201f-4a21-8075-b1fbcf1371fd)

Este repositório apresenta uma análise detalhada do problema de evasão de clientes (churn) da empresa fictícia Telecom X, com base em dados reais simulados e estruturados. A análise foi realizada utilizando Python e suas principais bibliotecas para manipulação de dados e visualização.

## Objetivo

A empresa Telecom X enfrenta um alto índice de cancelamentos e precisa entender os fatores que levam à perda de clientes. O desafio consistiu em:

- Coletar, tratar e analisar os dados

- Utilizar conceitos de ETL

- Extrair informações valiosas


## Dicionário de Dados

Apresentação dos principais campos disponíveis no dataset, com breve descrição de cada variável:

- **CustomerID**: Número de identificação único de cada cliente.

- **Churn**: Cliente deixou ou não a empresa ('Yes' para sim, 'No' para não).

- **Gender**: Gênero (masculino ou feminino).

- **SeniorCitizen**: Se o cliente tem 65 anos ou mais.

- **Partner**: Indica se o cliente possui parceiro(a).

- **Dependents**: Indica se o cliente possui dependentes.

- **Tenure**: Meses de contrato com a empresa.

- **PhoneService**: Se possui serviço telefônico.

- **MultipleLines**: Se possui múltiplas linhas telefônicas.

- **InternetService**: Tipo de serviço de internet.

- **OnlineSecurity**: Se possui serviço adicional de segurança online.

- **OnlineBackup**: Se possui serviço adicional de backup.

- **DeviceProtection**: Se possui proteção de dispositivo.

- **TechSupport**: Se possui suporte técnico adicional.

- **StreamingTV**: Se possui assinatura de TV.

- **StreamingMovies**: Se possui assinatura de filmes.

- **Contract**: Tipo de contrato (mensal, anual etc.).

- **PaperlessBilling**: Se recebe fatura digital.

- **PaymentMethod**: Forma de pagamento.

- **MonthlyCharges**: Valor gasto mensalmente.

- **TotalCharges**: Valor total gasto durante o período de contrato.

### **Variáveis derivadas**:

- **DailyCharges**: Gasto médio diário

- **ServiceCount**: Total de serviços contratados

- **AvgServiceCost**: Gasto médio por serviço ativo

- **TenureGroup**: Faixa de tempo de fidelidade

## Limpeza e Tratamento de Dados

- Conversão de tipos: `TotalCharges` para float, remoção de nulos com mediana

- Remoção de duplicatas (22 registros)

- Padronização de strings e substituição de categorias não informativas

- Conversão binária de `SeniorCitizen`

### Variáveis derivadas importantes foram criadas para enriquecer a análise:

Criação de variáveis derivadas:

`DailyCharges` = `TotalCharges` / `Tenure`

`ServiceCount`: número de serviços com valor 'Yes'

`AvgServiceCost`: custo médio por serviço

`TenureGroup`: faixa categórica de fidelidade

## Estatísticas Gerais

**Volume de registros:** 7032 clientes após tratamento

![image](https://github.com/user-attachments/assets/a0454a4c-b1c4-4a26-897a-2a7df3d588de)

# Análise Visual Detalhada

A seguir, são apresentadas visualizações que ilustram os principais padrões encontrados nos dados. Esses gráficos foram gerados com a biblioteca seaborn, com ajustes visuais refinados e exportados em alta resolução.

## Distribuição de Variáveis Numéricas por Churn

A análise de densidade (KDE) mostra diferenças marcantes entre os clientes que permaneceram e os que cancelaram o serviço:

- **Tenure**: Clientes que saem da empresa geralmente possuem até 24 meses de contrato.

- **MonthlyCharges**: Churn mais prevalente entre quem paga mensalidades acima de R$ 75.

- **TotalCharges**: Clientes com menor gasto total apresentam maior churn — comportamento comum em novos clientes.

- **DailyCharges**: Gasto diário elevado com baixa fidelização também aponta risco.

![kde_numerical_distributions png](https://github.com/user-attachments/assets/a82e0f58-f73c-4853-a914-3d2ddf54b4d5)

## Churn por Tipo de Contrato

- Contratos Mensais (Month-to-month): Apresentam o maior volume de churn (barra "Yes" significativamente mais alta), indicando alta rotatividade.
  
- Contratos Anuais (One year): Registram o menor volume absoluto de churn em comparação com os demais tipos de contrato.
  
- Contratos Bianuais (Two year): Também exibem um volume de churn muito baixo, similar aos contratos de "One year", com a vasta maioria dos clientes permanecendo.

- Fidelização: Há uma clara relação inversa entre a duração do contrato e a probabilidade de churn; contratos de maior duração (One year e Two year) demonstram maior fidelidade do cliente.

![churn_by_contract_type png](https://github.com/user-attachments/assets/94ff4559-3bcb-4c64-bcd5-32f6546d434f)

## Perfil Demográfico

- **Idosos (SeniorCitizen = Yes) apresentam mais churn:** O gráfico "Churn by SeniorCitizen" evidencia que, entre os "Yes" (idosos), a proporção de churn é maior do que entre os "No".

- **Solteiros e pessoas sem dependentes também têm maior evasão:**
  
  - No gráfico "Churn by Partner", a barra "Yes" (churn) é visivelmente mais alta para quem não tem parceiro ("No").

  - No gráfico "Churn by Dependents", a barra "Yes" (churn) é mais alta para quem não tem dependentes ("No").

- **O gênero e o uso de telefone não têm impacto significativo:**
  
  - No gráfico "Churn by Gender", as proporções de churn são muito semelhantes para "Female" e "Male".

  - No gráfico "Churn by PhoneService", as proporções de churn são igualmente similares entre "Yes" (com serviço de telefone) e "No" (sem serviço de telefone).

![demographic_profile png](https://github.com/user-attachments/assets/0b891ae6-fdd0-4689-889e-4869d60fbaa4)

## Quantidade de Serviços Contratados

- **Serviços Mínimos (0 ou 1):**
  
  - Clientes com zero serviços contratados (indicando talvez apenas um serviço base ou nenhuma adesão completa) apresentam a maior taxa de churn, superior a 40%.
Aqueles com apenas um serviço também exibem uma taxa de churn considerável, embora menor que a de zero serviços.

- **Dois Serviços:**
  - A taxa de churn aumenta novamente para clientes com dois serviços, tornando-se a segunda maior proporção de churn no gráfico.
   
- **Múltiplos Serviços (3 a 7):**
  
  - À medida que a quantidade de serviços contratados aumenta (de 3 a 7), a taxa de churn diminui consistentemente.
   
  - Clientes com 6 ou 7 serviços contratados demonstram as menores proporções de churn, indicando maior fidelização.
   
**Conclusão:** Há uma clara tendência de que quanto menos serviços o cliente contrata, maior a propensão ao churn. Aumentar a quantidade de serviços por cliente (upselling) parece ser uma estratégia eficaz para a retenção.

![churn_by_service_count png](https://github.com/user-attachments/assets/3ae94456-11a7-451a-a798-328d5bf7fc3d)

## Serviços Adicionais

- **Serviço de Múltiplas Linhas (MultipleLines):**
  
  - Clientes que não possuem o serviço de múltiplas linhas ("No") representam um volume maior tanto de clientes que permanecem quanto de clientes que cancelam, comparados àqueles que possuem ("Yes").
   
  - A proporção de churn para quem não tem múltiplas linhas é ligeiramente maior, mas não tão acentuada quanto em outros serviços de segurança/proteção.

- **Serviço de Internet (InternetService):**

  - Clientes com internet Fiber optic (fibra óptica) apresentam a maior proporção de churn em relação aos que permanecem, quando comparados a outras opções de internet (DSL) ou a não ter serviço de internet. Isso pode indicar problemas de qualidade ou custo percebido.

  - Clientes sem serviço de internet ("No") têm uma taxa de churn muito baixa.

- **Segurança Online (OnlineSecurity):**

  - Clientes que não utilizam o serviço de segurança online ("No") exibem um número consideravelmente maior de churn em comparação com aqueles que o utilizam ("Yes"). Isso sugere que a segurança online é um fator de retenção.
   
- **Backup Online (OnlineBackup):**
  - Similar à segurança online, clientes que não possuem o serviço de backup online ("No") demonstram uma proporção de churn visivelmente superior aos que o possuem ("Yes"), reforçando o valor desse serviço na retenção.
   
- **Proteção de Dispositivo (DeviceProtection):**
  
  - Clientes que não optam pela proteção de dispositivo ("No") também apresentam um volume e uma proporção de churn mais elevados quando comparados aos que utilizam o serviço ("Yes").

 - **Conclusão Geral sobre Serviços Adicionais:**

   - A ausência de serviços complementares, como OnlineSecurity, OnlineBackup e DeviceProtection, está claramente associada a um risco elevado de churn.
   
   - Isso corrobora a hipótese de que serviços adicionais (complementares) atuam como importantes fatores de fidelização, aumentando o "custo de saída" percebido pelo cliente e agregando valor ao pacote total.
   
   - A exceção notável é o serviço de internet Fiber optic, que, apesar de ser um serviço adicional, parece ter uma alta taxa de churn, sugerindo que fatores como preço, qualidade ou concorrência podem estar em jogo.

![subscribed_services png](https://github.com/user-attachments/assets/2b672bc0-7eb5-418e-9d19-9e5998900027)

## Suporte e Métodos de Pagamento

- **Suporte Técnico (TechSupport):** A ausência de suporte técnico está diretamente ligada a um maior churn.
  
- **Faturamento Sem Papel (PaperlessBilling):** Clientes que optam pelo faturamento sem papel apresentam uma maior propensão a cancelar o serviço.
Métodos de Pagamento:

- **Electronic check** é o método de pagamento com a maior taxa de churn.

- **Mailed check** é o segundo método com maior risco de churn.

- Métodos automáticos (cartão de crédito e transferência bancária) exibem menor churn, sugerindo maior estabilidade.
  
Essencialmente, a presença de suporte técnico e a escolha de métodos de pagamento automáticos são fatores de retenção, enquanto o faturamento sem papel e pagamentos por cheque eletrônico/correio indicam maior risco de churn.

![usage_payment png](https://github.com/user-attachments/assets/aabc5b7f-a74b-4b19-8b5c-26ddb7e74666)

## Fidelidade por Tempo de Contrato

- **Clientes com até 12 meses representam a maior parte dos cancelamentos:** A barra "0-12" mostra a maior proporção da seção "Yes" (churn), indicando que novos clientes têm maior probabilidade de cancelar.
  
- **Após 36 meses, a fidelização se estabiliza:** A partir do grupo "37-48" (ou visualmente após "25-36"), a proporção da seção "No" (permanência) nas barras empilhadas aumenta significativamente, e a seção "Yes" (churn) se torna muito pequena, quase marginal, nos grupos de tenure mais elevados ("49-60" e "61-72"). Isso denota que a taxa de churn diminui consideravelmente e se estabiliza em níveis muito baixos para clientes de longa data.
  
Essa análise complementa bem a observação anterior da análise KDE de "Tenure", onde a curva "Yes" (churn) tinha maior densidade nos primeiros 24 meses. O gráfico de barras empilhadas solidifica essa compreensão ao quantificar as proporções por grupos de tempo.

![churn_by_tenure_group png](https://github.com/user-attachments/assets/f98affdf-80b3-45b6-8288-4b434f1430ce)

## Distribuição de Serviços vs Churn (Boxplot)

- **Mediana de Serviços:** A mediana (linha central da caixa) para o grupo "Yes" (churn) está em 2 serviços, enquanto a mediana para o grupo "No" (não churn) está em 3 serviços. Isso corrobora que a maioria dos clientes que cancelam possui menos serviços.
  
- **Amplitude Interquartil (IQR):** A caixa do grupo "Yes" é mais "baixa" (concentrada em menos serviços) que a do grupo "No", indicando que 50% dos churners estão entre 1 e 4 serviços, enquanto para os não churners, esse intervalo é de 1 a 5 serviços.
  
- **Distribuição Geral:** O boxplot confirma que a distribuição da quantidade de serviços para clientes que fazem churn ("Yes") é majoritariamente inclinada para um número menor de serviços, enquanto para os clientes que permanecem ("No"), a distribuição se estende para um número maior de serviços.

O boxplot de "Service Count vs Churn" visualiza de forma clara o que já havia sido inferido pelos gráficos de barras de "Proporção de Churn por Quantidade de Serviços Contratados" e "Serviços Adicionais". Boxplot confirma que clientes com menos serviços têm maior propensão a cancelar. A mediana de serviços contratados por churners é menor que a dos clientes fiéis

![service_count_vs_churn](https://github.com/user-attachments/assets/f0593d9f-6922-49e7-974a-cc58c69fa200)

## Método de Pagamento

- **Electronic check:** Apresenta a maior proporção de churn, indicando alto risco de cancelamento.

- **Mailed check:** É o segundo método com maior taxa de churn, embora em menor volume.
  
- **Credit card (automatic):** Possui baixa proporção de churn, sinalizando maior retenção.

- **Bank transfer (automatic):** Similar ao cartão de crédito automático, demonstra baixa taxa de churn e maior estabilidade.
  
![churn_by_payment_method](https://github.com/user-attachments/assets/ad901644-3b3d-49ce-9591-c410651230aa)

# Conclusão e Soluções

Com base na análise exploratória realizada, é possível concluir que a evasão de clientes está fortemente associada à baixa adesão de serviços, contratos curtos, ausência de suporte e métodos de pagamento não automáticos. Recomendações práticas:

- Investir em estratégias de upselling para aumentar a quantidade de serviços contratados por cliente.

- Oferecer planos de fidelidade com contratos mais longos.

- Incentivar métodos de pagamento automáticos com benefícios.

- Promover serviços de segurança, backup e suporte técnico como diferenciais.

- Monitorar e melhorar a percepção do serviço de internet via fibra óptica.

## Exportação dos Dados Tratados

Após a etapa de limpeza, transformação e enriquecimento dos dados, o conjunto final foi exportado em dois formatos amplamente utilizados, com codificação e separadores adaptados ao padrão brasileiro:

**CSV:** Arquivo separado por ponto e vírgula (;), com vírgulas decimais (',') e codificação utf-8-sig, ideal para abertura no Excel em português.
```
python
df.to_csv('TelecomX_Data_Clean.csv', sep=';', decimal=',', index=False, encoding='utf-8-sig')
```
**Excel (.xlsx):** Arquivo compatível com o Microsoft Excel, contendo o DataFrame final sem a coluna de índice.
```
python
df.to_excel('TelecomX_Data_Clean.xlsx', index=False)
```
---

# 🤝 Agradecimentos

Este projeto foi desenvolvido como parte do programa **Oracle Next Education**, com apoio da **Oracle** e da **Alura Latam**, em uma iniciativa de capacitação em tecnologia baseada em desafios reais de negócios. A proposta do desafio foi elaborada com a colaboração da **Apple**, a fim de promover o aprendizado prático e orientado por projetos.

Agradeço a essas organizações pela oportunidade de colocar em prática conceitos de Ciência de Dados aplicados ao mundo corporativo.

---

# Certificado

https://cursos.alura.com.br/certificate/7e5e79af-899d-48c9-8974-2418d82b5fa0
 


  

