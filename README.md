# Análise Exploratória de dados em vendas Farmacêuticas
![image](https://github.com/user-attachments/assets/e512088c-ab1a-4fa5-876b-f6f0d6efdc17)

Este projeto consiste na análise dos dados públicos disponibilizados no [Portal de Dados abertos](https://dados.gov.br/dados/conjuntos-dados/venda-de-medicamentos-controlados-e-antimicrobianos---medicamentos-industrializados), com objetivo de entender a dinâmica das vendas de farmacêuticas.

## Etapas:

### **1 - Entendimento do negócio**

A análise de dados das vendas farmacêuticas em diferentes regiões e demografias pode proporcionar uma série de insights e resolver diversos problemas de negócios.

- **Alocação de Recursos:** Identificar as regiões geográficas que apresentam maior demanda por medicamentos específicos, possibilitando uma alocação mais eficiente de recursos de produção e distribuição.

- **Expansão de Mercado**: Identificar oportunidades de expansão de mercado em regiões subatendidas ou grupos demográficos com necessidades não atendidas.

- **Segmentação de Mercado:** Dividir a base de clientes em grupos demográficos (idade, gênero, etc.) para entender quais grupos são os maiores consumidores de diferentes tipos de medicamentos. Personalizar estratégias de marketing e vendas com base nessa segmentação.

- **Estoque e Logística:** Otimizar os níveis de estoque com base na oferta e demanda, reduzindo custos de armazenamento e riscos de falta de produtos.

- **Identificação de Tendências de Mercado:** Compreender as tendências de vendas ao longo do tempo, identificando picos sazonais e flutuações de demanda. Determinar quais produtos farmacêuticos têm maior demanda em diferentes épocas do ano.

- **Previsão de Demanda:** Prever a demanda futura de medicamentos com base em padrões históricos, permitindo que as empresas farmacêuticas ajustem suas estratégias de produção e estoque.

### **2 - Entendimento dos Dados**

Para a resolução do problema de negócio dado, serão analizados os "Dados Abertos de Venda de Medicamentos Industrializados do Sistema Nacional de Gerenciamento de Produtos Controlados (SNGPC) de Novembro de 2021".

Os quais podem ser encontrados através do link do [Portal de Dados Abertos](https://dados.gov.br/dados/conjuntos-dados/venda-de-medicamentos-controlados-e-antimicrobianos---medicamentos-industrializados)

Neste portal, estão disponíveis dados abertos com informações sobre a venda de medicamentos industrializados sujeitos à escrituração no SNGPC.

Os dados disponíveis são extraídos do banco de dados do sistema SNGPC, provenientes apenas de farmácias e drogarias privadas, conforme determina o parágrafo único, do Art. 3°, da RDC nº 22/2014.

Todas as farmácias e drogarias do país, que vendem medicamentos sujeitos à escrituração no SNGPC, devem enviar para a Anvisa, em formato eletrônico e periodicamente, os dados a respeito de todas as vendas realizadas desses tipos de medicamentos. Esses dados são processados pelo SNGPC e armazenados em seu banco de dados.

#### **2.1 - Sobre o SNGPC**

O Sistema Nacional de Gerenciamento de Produtos Controlados (SNGPC), monitora as movimentações de entrada (compras e transferências) e saída (vendas, transformações, transferências e perdas) de medicamentos sujeitos à escrituração no SNGPC comercializados em farmácias e drogarias privadas do país.

Entre 2007 e 2008, o sistema substituiu a escrituração em livro físico pela escrituração obrigatoriamente eletrônica, com transmissão dos dados à Anvisa.

Maiores informações a respeito do SNGPC podem ser encontradas na página do sistema no portal de serviços da Anvisa: http://portal.anvisa.gov.br/sngpc

#### **2.2 - Agência Nacional de Vigilância Sanitária - ANVISA**

Criada pela Lei nº 9.782, de 26 de janeiro 1999, a Agência Nacional de Vigilância Sanitária (Anvisa) é uma autarquia sob regime especial, que tem sede e foro no Distrito Federal, e está presente em todo o território nacional por meio das coordenações de portos, aeroportos, fronteiras e recintos alfandegados.

Tem por finalidade institucional promover a proteção da saúde da população, por intermédio do controle sanitário da produção e consumo de produtos e serviços submetidos à vigilância sanitária, inclusive dos ambientes, dos processos, dos insumos e das tecnologias a eles relacionados, bem como o controle de portos, aeroportos, fronteiras e recintos alfandegados.

#### **2.3 - Dicionário de Dados**

- `ANO_VENDA`: Ano da venda do medicamento.

- `MES_VENDA`: Mês da venda do medicamento.

- `UF_VENDA`: Unidade Federativa do endereço da farmácia ou drogaria, cadastrado no banco de dados da Anvisa, representando a UF onde ocorreu a venda.

- `MUNICIPIO_VENDA`: Município do endereço da farmácia ou drogaria, cadastrado no banco de dados da Anvisa, representando o Município onde ocorreu a venda.

- `PRINCIPIO_ATIVO`: Nome do princípio ativo do medicamento industrializado, conforme cadastrado no registro do medicamento, no banco de dados da Anvisa.

   Quando um medicamento tem mais de um princípio ativo, cada um deles é separado pelo caractere “+”.

   Ex.: “PRINCÍPIO ATIVO 1 + PRINCÍPIO ATIVO 2”

- `DESCRICAO_APRESENTACAO`: Uma Apresentação de Medicamento representa O modo como um medicamento é apresentado na embalagem.
Exemplo:Medicamento X, pode ter duas apresentações diferentes:
   
   • Apresentação 1: Uma caixa com 1 blister de alumínio com 20 comprimidos, cada comprimido com 5 mg de princípio ativo.
   Nesse caso, a descrição da apresentação seria: “5 MG COM CT BL AL X 20”
   
   • Apresentação 2: Uma caixa com 1 frasco de vidro com 50 mL de um xarope, com concentração do princípio ativo de 15 mg por mL.
   
   Nesse caso, a descrição da apresentação seria: 15MG/ML XPE CT FR VD x 50 ML
   Esses exemplos representam descrições de apresentações diferentes para um mesmo medicamento.
   
   Os termos utilizados na descrição das apresentações seguem o disposto no Vocabulário Controlado da Anvisa, disponível no link: http://portal.anvisa.gov.br/documents/33836/2501339/Vocabul%C3%A1rio+Controlado/fd8fdf08-45dc-402a-8dcf-fbb3fd21ca75

- `QTD_VENDIDA`: Quantidade vendida de caixas ou frascos do medicamento.

- `UNIDADE_MEDIDA`: Indica se a quantidade vendida do medicamento foi de caixas ou frascos.

- `CONSELHO_PRESCRITOR`: Conselho de Classe do profissional que prescreveu o medicamento vendido.

- `UF_CONSELHO_PRESCRITOR`: Unidade Federativa do Conselho de Classe do profissional que prescreveu o medicamento vendido.

- `TIPO_RECEITUARIO`: Tipo de receituário utilizado na prescrição.
Valores e respectivos tipos de receituário:

   1 – Receita de Controle Especial em 2 vias (Receita Branca);

   2 – Notificação de Receita B (Notificação Azul);

   3 – Notificação de Receita Especial (Notificação Branca);

   4 – Notificação de Receita A (Notificação Amarela);

   5 – Receita Antimicrobiano em 2 vias.

- `CID10`: Classificação Internacional de Doença (aplicável apenas a medicamentos antimicrobianos).

- `SEXO`: Sexo do paciente (aplicável apenas a medicamentos antimicrobianos). Valor 1 para o sexo masculino, valor 2 para o sexo feminino.

- `IDADE`: Valor numérico que representa a idade do paciente, em meses ou anos (aplicável apenas a medicamentos antimicrobianos).

- `UNIDADE_IDADE`: Unidade de medida da idade do paciente, que pode ser em meses ou anos (aplicável apenas a medicamentos antimicrobianos). Valor 1 para unidade de medida em anos, valor 2 para unidade de medida em meses.

### **3 - Importações, Pré processamento e limpeza**

Nesta etapa iniciei realizando as importações necessárias (Pandas, Numpy, Matplotlib, Seaborn).

Após as importações fiz o carregamento da base, avaliando a sua estrutura e metadados, em seguida identifiquei quais colunas possuíam valores nulos e quais possuíam valores substituíveis. A seguir trarei um breve resumo:

`CID10`: Possuía 99% de valores nulos, fiz a remoção dessa coluna.

`SEXO`: Coluna do tipo inteiro, baseado no dicionário de dados fiz a substituição para categórico. Possuía 35.74% de valores nulos, como existiam apenas dois valores distintos, substituir pela moda traria um viés para as análises, por esse motivo optei por substituir os nulos por um valor simbólico facilmente identificado posteriormente.

`IDADE`: Possuía idades em Meses e Anos, realizei a padronização para Anos baseado na coluna `UNIDADE_IDADE`, ela tinha 35.74% de valores nulos, como o foco era a realização da EDA, optei por substitui-los por um valor simbólico que fosse facilmente identificado posteriormente.

`PRINCIPIO_ATIVO`: Possuía apenas 0.18% de valores nulos, uma quantidade praticamente insignificante, porém da mesma forma optei por substitui-los por um valor simbólico que fosse facilmente identificado posteriormente.

Após o tratamento dos valores nulos, fiz a remoção das colunas que não traziam informações para as análises:

`UNIDADE_IDADE`, `CID10`, `ANO_VENDA`, `MES_VENDA`

### **4 - Análise Exploratória dos dados (EDA)**

Aqui fiz todas as análises estatísticas Univariadas e Multivariadas dividindo em Numéricas e Categóricas. Realizando análises por Região, Estado, Produtos, Idades, Receituário e etc.

### **5 - Insights e Recomendações**

Após todas as análises gráficas e estatísticas, pontos importantes foram extraídos e insights gerados:

#### **5.1 - Insights sobre os hábitos de compra e padrões.**

- O Estado de SP lidera a compra e consumo de remédios com 586 mil vendas
- A Azitromicina di-hidratada foi a mais vendida com 177172 vendas
- Descricao 500 MG CAP DURA CT BL AL PLAS TRANS X 21 88157
remédios de 500mb são os mais consumidos
- As maiores compras foram as de caixa (2321681)
- A região Sudeste é a que mais compra (44.71% das vendas), seguida do Sul (21.2). 
- Nordeste possui a segunda maior
média de medicamentos por venda (3.74)
- Os Estados que menos venderam foram RR (7157) e AP (7031) e apresentam também as menores médias de medicamentos vendidos por venda
- Dos 27 Estados presentes na base, apenas  8 estão acima da média de vendas
- Dos 19 Estados abaixo da média de vendas, 2 deles (MA, DF) possuem a maior média de itens vendidos por venda (5.14 e 5.13, respectivamente) .
- Os remédios com os principios ativos mais vendidos foram AZITROMICINA DI-HIDRATADA (177172) (20%) e
AMOXICILINA TRI-HIDRATADA (118605) (13%). Amoxicilina aparece em 3 princípios ativos
- A faixa de idade que mais comprou foi a de 20-40 anos (apenas remédios antimicrobianos).
- O principio ativo mais consumido por idade foi a AZITROMICINA, seguida da DEXAMETASONA na faixa 20-30 anos
- A descrição mais comum por idade foi a de 3,0 MG/ML + 1,0 MG/ML SUS OFT CT FR GOT PLAS TRANS X 5 ML
- O Tipo receituario mais comercializado entre todas as idades foi o tipo 5
-Crianças de 0 a 5 anos possuem uma grande concentração de consumo (140k)
- Após os 40 anos podemos notar uma queda conforme a idade avança
- A classe econômicamente ativa (dos 20 aos 60) concentram a maior parte das vendas (mais de 1 milhão)

#### **5.2 - Recomendações**

##### **Padrões Geográficos**

*Região Sudeste*
- Como é a região que mais demanda remédios, temos uma oportunidade de abrir mais unidades, ou aplicar estratégias de vendas específicas para essa região
- Baseado nas analises podemos renegociar os preços com distribuídores locais ou otimizar logística das distribuição dos medicamentos

*Região Nordeste*

- É a região que tem a segunda maior média de itens por venda (3,74), o que nos mostra uma oportunidade de melhorar a quantidade de vendas, já que o volume é maior do que os demais (menos Sudeste)

*Região Sul*

- Mesmo sendo a segunda maior em Total de vendas realizadas, possuí a menor média de itens vendidos por venda, o que nos mostra um volume muito baixo. É interessante aplicar estratégias para aumentar esse volume, já que o Total de vendas está acima da média

*Regiões Centro-Oeste e Norte*

- São as que apresentam os menores números, é considerável havaliar as barreiras logísticas ou socioeconômicas que limitam as vendas e o acesso aos medicamentos

*Estados: MA, DF, CE, PI e PE* 
- São os que possuem a maior média de vendas. Seria interessante a área de negócio investigar mais a fundo esse fato procurando entender como é o mercado naquela região, se são compras volumosas mas com pouca recorrência, assim podemos visar planos para aumentar a recorrência dessas compras volumosas

##### **Principio ativo e Descrição dos medicamentos**
- Como a AZITROMICINA DI-HIDRATADA é a mais comercializavel existe uma necessidade de aumentar os estoques ou revisar o processo da logística da entrega desses medicamentos, junto da possibilidade de descontos

- Remédios de 500MG são os mais consumidos, o que da oportunidades de melhoria nos estoques, uma vez que sabemos que é a gramatura mais consumida, podemos manter uma rotatividade alta nos estoques

- AZITROMICINA: Como ela tem uma grande procura entre os jovens adultos, pode ser interessante focar estratégias de marketing ou distribuição para clínicas e farmácias de regiões mais urbanas ou de maior concentração dessa faixa etária

##### **Faixas etárias**

*0-20 anos:*
- Indicação do uso de medicamentos líquidos (provavelmente antibióticos ou tratamentos para infecções respiratórias)

*20-30 anos:*
- Essa faixa etária pode estar mais propensa ao uso de medicamentos para condições de saúde mais comuns, como infecções oculares ou respiratórias.

*30-50 anos:*

- Adultos mais velhos estão mais propensos a utilizar medicamentos de apresentação em cápsulas, como antibióticos, possivelmente para infecções respiratórias ou outros tipos de infecções bacterianas.

- Essa descrição está um pouco mais distribuída ao longo das faixas etárias, mas ainda assim apresenta picos consideráveis.


*60+ anos:*

- Maior uso de medicamentos que podem ser usados para tratar doenças crônicas ou infecções em idosos, com uma tendência maior de venda nas faixas etárias mais velhas.
