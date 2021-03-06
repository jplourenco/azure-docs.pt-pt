---
title: "Tutorial: criar um pipeline com o Assistente de Cópia | Microsoft Docs"
description: "Neste tutorial, irá criar um pipeline do Azure Data Factory com uma Atividade de Cópia com o Assistente de Cópia suportado pelo Data Factory"
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: b87afb8e-53b7-4e1b-905b-0343dd096198
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 02/02/2017
ms.author: spelluru
translationtype: Human Translation
ms.sourcegitcommit: fbf77e9848ce371fd8d02b83275eb553d950b0ff
ms.openlocfilehash: 5a50f583831b398ae22416e7ade23c33846de55c


---
# <a name="tutorial-create-a-pipeline-with-copy-activity-using-data-factory-copy-wizard"></a>Tutorial: Criar um pipeline com Atividade de Cópia com o Assistente de Cópia do Data Factory
> [!div class="op_single_selector"]
> * [Descrição geral e pré-requisitos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [Assistente de Cópia](data-factory-copy-data-wizard-tutorial.md)
> * [Portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)
> * [Modelo do Azure Resource Manager](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [API REST](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [API .NET](data-factory-copy-activity-tutorial-using-dotnet-api.md)
> 
> 

O **Assistente de Cópia** do Azure Data Factory permite-lhe criar rápida e facilmente um pipeline que implementa o cenário de ingestão/movimento de dados. Consequentemente, recomendamos que o utilize como primeiro passo para criar um pipeline de exemplo para o cenário de movimento de dados. Este tutorial mostra-lhe como criar uma fábrica de dados do Azure, iniciar o Assistente de Cópia e passar por uma série de passos para fornecer os detalhes sobre o seu cenário de ingestão/movimento de dados. Após concluir os passos do assistente, este cria automaticamente um pipeline com uma Atividade de Cópia para copiar dados de um armazenamento de blobs do Azure para uma base de dados SQL do Azure. Veja o artigo [Atividades de Movimentos de Dados](data-factory-data-movement-activities.md) para obter detalhes sobre a Atividade de Cópia. 

## <a name="prerequisites"></a>Pré-requisitos
- Leia a [Descrição Geral e Pré-requisitos do Tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obter uma descrição geral do tutorial e concluir os passos de **pré-requisitos**.


## <a name="create-data-factory"></a>Criar fábrica de dados
Neste passo, irá utilizar o Portal do Azure para criar uma fábrica de dados do Azure com o nome **ADFTutorialDataFactory**.

1. Depois de iniciar sessão no [portal do Azure](https://portal.azure.com), clique em **+ NOVA**, no canto superior esquerdo, clique em **Informações + Análises** e clique em **Data Factory**. 
   
   ![Novo -> DataFactory](./media/data-factory-copy-data-wizard-tutorial/new-data-factory-menu.png)
2. No painel **Nova fábrica de dados**:
   
   1. Introduza **ADFTutorialDataFactory** como **nome**.
       O nome do Azure Data Factory deve ser globalmente exclusivo. Se receber o erro: **Nome "ADFTutorialDataFactory" da fábrica de dados não disponível**, altere o nome (por exemplo, seunomeADFTutorialDataFactory) e tente criar novamente. Veja o tópico [Data Factory – Naming Rules (Data Factory – Regras de Nomenclatura)](data-factory-naming-rules.md) para obter as regras de nomenclatura dos artefactos do Data Factory.  
      
       ![Nome do Data Factory não disponível](./media/data-factory-copy-data-wizard-tutorial/getstarted-data-factory-not-available.png)
      
      > [!NOTE]
      > O nome da fábrica de dados pode ser registado como um nome DNS no futuro e, por conseguinte, ficar publicamente visível.
      > 
      > 
   2. Selecione a sua **subscrição** do Azure.
   3. No Grupo de Recursos, siga um destes passos: 
      
      - Selecione **Utilizar existente** para selecionar um grupo de recursos já existente.
      - Selecione **Criar novo** para introduzir um nome para um grupo de recursos.
         
          Alguns dos passos deste tutorial pressupõe que utiliza o nome: **ADFTutorialResourceGroup** para o grupo de recursos. Para saber mais sobre os grupos de recursos, veja [Utilizar grupos de recursos para gerir os recursos do Azure](../azure-resource-manager/resource-group-overview.md).
   4. Selecione uma **localização** para a fábrica de dados.
   5. Selecione a caixa de verificação **Afixar ao dashboard**, na parte inferior do painel.  
   6. Clique em **Criar**.
      
       ![Painel Nova fábrica de dados](media/data-factory-copy-data-wizard-tutorial/new-data-factory-blade.png)            
3. Após concluir a criação, verá o painel **Data Factory**, conforme apresentado na imagem seguinte:
   
   ![Home page da fábrica de dados](./media/data-factory-copy-data-wizard-tutorial/getstarted-data-factory-home-page.png)

## <a name="launch-copy-wizard"></a>Inicie o Assistente de Cópia
1. Na home page do Data Factory, clique no mosaico **Copiar dados** para iniciar o **Assistente de Cópia**. 
   
   > [!NOTE]
   > Se vir que o browser bloqueia enquanto estiver a "A autorizar…", desative/desmarque a definição **Bloquear cookies de terceiros e dados do site** (ou) mantenha-a ativada e crie uma exceção para **login.microsoftonline.com** e, em seguida, tente iniciar novamente o assistente.
   > 
   > 
2. Na página **Propriedades**:
   
   1. Introduza **CopyFromBlobToAzureSql** para **Nome da tarefa**
   2. Introduza **Descrição** (opcional).
   3. Altere a **hora de data de início** e a **hora de data de fim**, para que a data de fim esteja definida como a data de hoje e a de início como cinco dias antes do dia atual.  
   4. Clique em **Seguinte**.  
      
      ![Página Ferramenta Copiar – Propriedades](./media/data-factory-copy-data-wizard-tutorial/copy-tool-properties-page.png) 
3. Na página **Arquivo de dados de origem**, clique no mosaico **Blob Storage do Azure**. Utilize esta página para especificar o arquivo de dados de origem para a tarefa de cópia. Pode utilizar um serviço ligado do arquivo de dados existente (ou) especificar um novo arquivo de dados. Para utilizar um serviço ligado existente, clique em **A PARTIR DE SERVIÇOS LIGADOS EXISTENTES** e selecione o serviço ligado correto. 
   
    ![Página Ferramenta Copiar – Arquivo de dados de origem](./media/data-factory-copy-data-wizard-tutorial/copy-tool-source-data-store-page.png)
4. Na página **Especificar a conta de armazenamento de blobs do Azure**:
   
   1. Introduza **AzureStorageLinkedService** para **Nome do serviço ligado**.
   2. Confirme que a opção **A partir de subscrições do Azure** está selecionada para o **Método de seleção de contas**.
   3. Selecione a sua **subscrição** do Azure.  
   4. Selecione uma **Conta de armazenamento do Azure** na lista das contas de armazenamento do Azure disponíveis na subscrição selecionada. Também pode optar por introduzir manualmente as definições da conta de armazenamento selecionando a opção **Introduzir manualmente** para **Método de seleção de contas** e, em seguida, clicar em **Seguinte**. 
      
      ![Ferramenta Copiar – Especificar a conta de armazenamento de blobs do Azure](./media/data-factory-copy-data-wizard-tutorial/copy-tool-specify-azure-blob-storage-account.png)
5. Na página **Escolher o ficheiro ou pasta de entrada**:
   
   1. Navegue até à pasta **adftutorial**.
   2. Selecione **emp.txt** e clique em **Escolher**
   3. Clique em **Seguinte**. 
      
      ![Ferramenta Copiar – Escolha o ficheiro ou pasta de entrada](./media/data-factory-copy-data-wizard-tutorial/copy-tool-choose-input-file-or-folder.png)
6. Na página **Escolher o ficheiro ou pasta de entrada**, clique em **Seguinte**. Não selecione **Cópia binária**. 
   
    ![Ferramenta Copiar – Escolha o ficheiro ou pasta de entrada](./media/data-factory-copy-data-wizard-tutorial/chose-input-file-folder.png) 
7. Na página **Definições do formato de ficheiro**, pode ver os delimitadores e o esquema que é detetado automaticamente pelo assistente ao analisar o ficheiro. Também pode introduzir os delimitadores manualmente para o Assistente de Cópia parar a deteção automática ou para substituir. Clique em **Seguinte** depois de rever os delimitadores e pré-visualizar os dados. 
   
    ![Ferramenta Copiar – Definições do formato de ficheiro](./media/data-factory-copy-data-wizard-tutorial/copy-tool-file-format-settings.png)  
8. Na página de Arquivo de dados de destino, selecione ** Base de Dados SQL do Azure** e clique em **Seguinte**.
   
    ![Ferramenta Copiar - escolher arquivo de destino](./media/data-factory-copy-data-wizard-tutorial/choose-destination-store.png)
9. Na página **Especificar a base de dados SQL do Azure**:
   
   1. Introduza **AzureSqlLinkedService** no campo **Nome da ligação**.
   2. Confirme que a opção **A partir de subscrições do Azure** está selecionada para o **Método de seleção de servidor/base de dados**.
   3. Selecione a sua **subscrição** do Azure.  
   4. Selecione **Nome do servidor** e **Base de dados**.
   5. Introduza o **Nome de utilizador** e a **Palavra-passe**.
   6. Clique em **Seguinte**.  
      
      ![Ferramenta Copiar - especificar a base de dados SQL do Azure](./media/data-factory-copy-data-wizard-tutorial/specify-azure-sql-database.png)
10. Na página **Mapeamento de tabelas**, selecione **emp** para o campo **Destino** na lista pendente, clique na **seta para baixo** (opcional) para ver o esquema e pré-visualizar os dados.
    
     ![Ferramenta Copiar – Mapeamento da tabelas](./media/data-factory-copy-data-wizard-tutorial/copy-tool-table-mapping-page.png) 
11. Na página **Mapeamento de esquemas**, clique em **Seguinte**.
    
    ![Ferramenta Copiar - mapeamento de esquema](./media/data-factory-copy-data-wizard-tutorial/schema-mapping-page.png)
12. Na página **Definições de desempenho**, clique em **Seguinte**. 
    
    ![Ferramenta Copiar - definições de desempenho](./media/data-factory-copy-data-wizard-tutorial/performance-settings.png)
13. Reveja as informações na página **Resumo** e clique em **Concluir**. O assistente cria dois serviços ligados, dois conjuntos de dados (entrada e saída) e um pipeline na fábrica de dados (a partir da qual iniciou o Assistente de Cópia). 
    
    ![Ferramenta Copiar - definições de desempenho](./media/data-factory-copy-data-wizard-tutorial/summary-page.png)

## <a name="launch-monitor-and-manage-application"></a>Iniciar o Monitor e Gerir a Aplicação
1. Na página **Implementação**, clique na ligação: `Click here to monitor copy pipeline`.
   
   ![Ferramenta Copiar – Implementação concluída com êxito](./media/data-factory-copy-data-wizard-tutorial/copy-tool-deployment-succeeded.png)  
2. Siga as instruções em [Monitorizar e gerir o pipeline com a Aplicação de Monitorização](data-factory-monitor-manage-app.md) para saber como monitorizar o pipeline que acabou de criar. Clique no ícone **Atualizar** na lista **JANELAS DE ATIVIDADE** para ver o setor. 
   
   ![Aplicação de Monitorização](./media/data-factory-copy-data-wizard-tutorial/monitoring-app.png) 
   
   
   Clique no botão **Atualizar** na lista **JANELAS DE ATIVIDADE**, na parte inferior, para ver o estado mais recente. Não é atualizado automaticamente. 

> [!NOTE]
> O pipeline de dados neste tutorial copia dados a partir de um arquivo de dados de origem para um arquivo de dados de destino. Não transforma dados de entrada para produzir dados de saída. Para ver um tutorial sobre como transformar dados através do Azure Data Factory, consulte [Tutorial: Build your first pipeline to transform data using Hadoop cluster (Tutorial: Criar o seu primeiro pipeline para transformar dados com o cluster do Hadoop)](data-factory-build-your-first-pipeline.md).
> 
> Pode encadear duas atividades (executar uma atividade após a outra) ao definir o conjunto de dados de saída de uma atividade como o conjunto de dados de entrada da outra atividade. Consulte [Scheduling and execution in Data Factory (Agendamento e execução no Data Factory)](data-factory-scheduling-and-execution.md) para obter informações detalhadas.

## <a name="see-also"></a>Veja também
| Tópico | Descrição |
|:--- |:--- |
| [Pipelines](data-factory-create-pipelines.md) |Este artigo ajuda-o a compreender os pipelines e as atividades no Azure Data Factory e como os utilizar para construir fluxos de dados ponto a ponto condicionados por dados para o seu cenário ou empresa. |
| [Conjuntos de dados](data-factory-create-datasets.md) |Este artigo ajuda-o a compreender os conjuntos de dados no Azure Data Factory. |
| [Agendamento e execução](data-factory-scheduling-and-execution.md) |Este artigo explica os aspetos de agendamento e execução do modelo da aplicação do Azure Data Factory. |




<!--HONumber=Feb17_HO1-->


