# **Curso do [DIO](https://web.dio.me) (BootCamp - Microsoft Azure AI Fundamentals)**

Azure Cognitive Search: Utilizando AI Search para indexação e consulta de Dados.

link importante: <https://microsoftlearning.github.io/mslearn-ai-fundamentals/Instructions/Labs/11-ai-search.html>


e necessario criar 3 labs antes de iniciar

<https://portal.azure.com/#create/hub>


Sendo a criação do labs, conta de armazenamento.

![](/img/001.png)

Azure ai services.

![](/img/002.png)

e azure ai services search.

![](/img/003.png)

Assim que fizer a **conta de armazenamento** é necessário configurá-lo para acesso anônimos, procure no canto da página o armazenamento (imagem abaixo).

![](/img/004.png)

acesse e procure o que foi criado, entre em suas configurações (imagem abaixo).

![](/img/005.png)

em ![](/img/006.png)  Procure Permitir acesso anônimo ao Blob (por padrão ele vem desabilitado, habilitado como na imagem).

![](/img/007.png)

Salve suas configurações, ainda em contêiner no menu ao lado procure por ![](/img/008.png)

Vamos agora trazer alguns arquivos para o nosso container, crie um novo container

![](/img/009.png)

e de o nome de “coffee-reviews”.

![](/img/010.png)

abra esse novo container e faça o upload dos arquivos do link <https://aka.ms/mslearn-coffee-reviews> (extraia e faça o upload dos mesmos). agora vá para o ai search e importe os dados.

por falta de tempo, **RESTO DA ABORDAGEM COPIADO DO LINK <https://microsoftlearning.github.io/mslearn-ai-fundamentals/Instructions/Labs/11-ai-search.html>**

## <a name="_7koowawlpmk7"></a>Indexar os documentos
Depois de armazenar os documentos, você poderá usar o Azure AI Search para extrair insights dos documentos. O portal do Azure fornece um *assistente de importação de dados* . Com este assistente, você pode criar automaticamente um índice e um indexador para fontes de dados suportadas. Você usará o assistente para criar um índice e importar seus documentos de pesquisa do armazenamento para o índice do Azure AI Search.

1. No portal do Azure, navegue até o recurso Azure AI Search. Na página Visão geral , selecione Importar dados.

   ![Captura de tela que mostra o assistente de importação de dados.](/img/011.png)

1. Na página Conectar-se aos seus dados , na lista Fonte de Dados , selecione Azure Blob Storage . Preencha os detalhes do armazenamento de dados com os seguintes valores:
   - Fonte de dados : Armazenamento de Blobs do Azure
   - Nome da fonte de dados : coffee-customer-data
   - Dados a extrair : Conteúdo e metadados
   - Modo de análise : Padrão
   - Cadeia de conexão : \*Selecione Escolha uma conexão existente . Selecione sua conta de armazenamento, selecione o contêiner de avaliações de café e clique em Selecionar .
   - Autenticação de identidade gerenciada : Nenhuma
   - Nome do contêiner : *esta configuração é preenchida automaticamente depois que você escolhe uma conexão existente* .
   - Pasta Blob : *deixe em branco* .
   - Descrição : Avaliações sobre Fourth Coffee Shops.
1. Selecione Próximo: Adicionar habilidades cognitivas (opcional) .
1. Na secção Anexar Serviços Cognitivos , selecione o seu recurso de serviços Azure AI.
1. Na seção Adicionar enriquecimentos :
   - Altere o nome da qualificação para coffee-skillset .
   - Marque a caixa de seleção Habilitar OCR e mesclar todo o texto no campo merged\_content .
   - Nota É importante selecionar Habilitar OCR para ver todas as opções de campo enriquecido.
   - Certifique-se de que o campo Dados de origem esteja configurado como merged\_content .
   - Altere o nível de granularidade de enriquecimento para Páginas (blocos de 5.000 caracteres) .
   - Não selecione *Habilitar enriquecimento incremental*
   - Selecione os seguintes campos enriquecidos:

|Habilidade Cognitiva|Parâmetro|Nome do campo|
| :- | :- | :- |
|Extraia nomes de locais| |Localizações|
|Extraia frases-chave| |frases chave|
|Detectar sentimento| |sentimento|
|Gerar tags de imagens| |imagemTags|
|Gere legendas de imagens| |legenda da imagem|

1. Em Salvar enriquecimentos em um armazenamento de conhecimento , selecione:
   - Projeções de imagem
   - Documentos
   - Páginas
   - Frases chave
   - Entidades
   - Detalhes da imagem
   - Referências de imagem

1. Nota Se aparecer um aviso solicitando uma cadeia de conexão de conta de armazenamento .

   ![Captura de tela que mostra o aviso de tela de conexão da conta de armazenamento com "Escolher uma conexão existente" selecionada.](/img/012.png)

   - Selecione Escolha uma conexão existente . Escolha a conta de armazenamento que você criou anteriormente.
   - Clique em + Container para criar um novo contêiner chamado armazenamento de conhecimento com o nível de privacidade definido como Private e selecione Create .
   - Selecione o contêiner de armazenamento de conhecimento e clique em Selecionar na parte inferior da tela.
1. Selecione projeções de blob do Azure: Documento . Uma configuração para *o nome do contêiner* com as exibições preenchidas automaticamente do contêiner *de armazenamento de conhecimento .* Não altere o nome do contêiner.
1. Selecione Próximo: Personalizar índice de destino . Altere o nome do índice para coffee-index .
1. Certifique-se de que a chave esteja configurada como metadata\_storage\_path . Deixe o nome do sugeridor em branco e o modo de pesquisa preenchido automaticamente.
1. Revise as configurações padrão dos campos de índice. Selecione filtrável para todos os campos que já estão selecionados por padrão.

   ![Captura de tela que mostra o painel de índice personalizado com o nome do índice inserido e 'Filtrável' selecionado para um campo de índice padrão.](/img/013.png)

1. Selecione Próximo: Criar um indexador .
1. Altere o nome do indexador para coffee-indexer .
1. Deixe a programação definida como Once .
1. Expanda as opções avançadas . Certifique-se de que a opção Base-64 Encode Keys esteja selecionada, pois as chaves de codificação podem tornar o índice mais eficiente.
1. Selecione Enviar para criar a fonte de dados, o conjunto de habilidades, o índice e o indexador. O indexador é executado automaticamente e executa o pipeline de indexação, que:
   - Extrai os campos de metadados do documento e o conteúdo da fonte de dados.
   - Executa o conjunto de habilidades cognitivas para gerar campos mais enriquecidos.
   - Mapeia os campos extraídos para o índice.
1. Volte à página de recursos do Azure AI Search. No painel esquerdo, em Gerenciamento de pesquisa , selecione Indexadores . Selecione o indexador de café recém-criado . Espere um minuto e selecione ↻ Atualize até que o Status indique sucesso.
1. Selecione o nome do indexador para ver mais detalhes.

   ![Captura de tela que mostra o indexador coffee-indexer criado com sucesso.](/img/014.png)

## <a name="_z4ema2awgrpg"></a>Consultar o índice
Use o Search Explorer para escrever e testar consultas. O explorador de pesquisa é uma ferramenta incorporada no portal do Azure que oferece uma maneira fácil de validar a qualidade do seu índice de pesquisa. Você pode usar o Search Explorer para escrever consultas e revisar resultados em JSON.

1. Na página *Visão geral* do serviço de pesquisa , selecione Explorador de pesquisa na parte superior da tela.

   ![Captura de tela de como encontrar o Search Explorer.](/img/015.png)

1. Observe como o índice selecionado é o *índice de café* que você criou. Abaixo do índice selecionado, altere a *visualização* para JSON view.

   ![Captura de tela do explorador de pesquisa.](/img/016.png)

No campo do editor de consultas JSON , copie e cole:

Códigocópia de

```
{

`    `"search": "\*",

`    `"count": true

}
```

- Selecione Pesquisar . A consulta de pesquisa retorna todos os documentos no índice de pesquisa, incluindo uma contagem de todos os documentos no campo @odata.count . O índice de pesquisa deve retornar um documento JSON contendo os resultados da pesquisa.
- Agora vamos filtrar por localização. No campo do editor de consultas JSON , copie e cole:
- Códigocópia de

```
{

` `"search": "locations:'Chicago'",

` `"count": true

}
```

- Selecione Pesquisar . A consulta pesquisa todos os documentos no índice e filtra revisões com localização em Chicago. Você deveria ver 3no @odata.countcampo.
- Agora vamos filtrar por sentimento. No campo do editor de consultas JSON , copie e cole:
- Códigocópia de

```
{

` `"search": "sentiment:'negative'",

` `"count": true

}
```

- Selecione Pesquisar . A consulta pesquisa todos os documentos no índice e filtra revisões com sentimento negativo. Você deveria ver 1no @odata.countcampo.
- Nota Veja como os resultados são classificados por @search.score. Esta é a pontuação atribuída pelo mecanismo de pesquisa para mostrar o quão próximos os resultados correspondem à consulta fornecida.
- Um dos problemas que podemos querer resolver é por que pode haver certas avaliações. Vamos dar uma olhada nas frases-chave associadas à avaliação negativa. O que você acha que pode ser a causa da revisão?
## <a name="_r7jubglenbjh"></a>Revise o armazenamento de conhecimento
Vamos ver o poder do armazenamento de conhecimento em ação. Ao executar o *assistente Importar dados* , você também criou um armazenamento de conhecimento. Dentro do armazenamento de conhecimento, você encontrará os dados enriquecidos extraídos pelas habilidades de IA que persistem na forma de projeções e tabelas.

1. No portal do Azure, navegue de volta para a sua conta de armazenamento do Azure.

1. No painel do menu esquerdo, selecione Containers. Selecione o contêiner de armazenamento de conhecimento .

   ![Captura de tela do contêiner de armazenamento de conhecimento.](/img/017.png)

1. Selecione qualquer um dos itens e clique no arquivo objectprojection.json .

   ![Captura de tela do objectprojection.json.](/img/018.png)

1. Selecione Editar para ver o JSON produzido para um dos documentos do seu armazenamento de dados do Azure.

   ![Captura de tela de como encontrar o botão de edição.](/img/019.png)

1. Selecione a localização atual do blob de armazenamento no canto superior esquerdo da tela para retornar à conta de armazenamento *Containers* .

   ![Captura de tela da localização atual do blob de armazenamento.](/img/020.png)

1. Em *Containers* , selecione o contêiner *coffee-skillset-image-projection* . Selecione qualquer um dos itens.

   ![Captura de tela do contêiner do conjunto de habilidades.](/img/021.png)

1. Selecione qualquer um dos arquivos *.jpg* . Selecione Editar para ver a imagem armazenada no documento. Observe como todas as imagens dos documentos são armazenadas desta forma.

   ![Captura de tela da imagem salva.](/img/022.png)

1. Selecione a localização atual do blob de armazenamento no canto superior esquerdo da tela para retornar à conta de armazenamento *Containers*.

1. Selecione Navegador de armazenamento no painel esquerdo e selecione Tabelas . Há uma tabela para cada entidade no índice. Selecione a tabela *coffeeSkillsetKeyPhrases*.

   Observe as frases-chave que o armazenamento de conhecimento conseguiu capturar do conteúdo das avaliações. Muitos dos campos são chaves, portanto você pode vincular as tabelas como um banco de dados relacional. O último campo mostra as frases-chave que foram extraídas pelo conjunto de habilidades.