---
title: " Criar uma conta dos Serviços de Multimédia do Azure com o portal do Azure | Microsoft Docss"
description: "Este tutorial orienta-o ao longo dos passos para criar uma conta dos Serviços de Multimédia do Azure no portal do Azure."
services: media-services
documentationcenter: 
author: Juliako
manager: erikre
editor: 
ms.assetid: c551e158-aad6-47b4-931e-b46260b3ee4c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/10/2017
ms.author: juliako
translationtype: Human Translation
ms.sourcegitcommit: 7ef0383ae88dcb8beb4b30792eaf60dec2911507
ms.openlocfilehash: 08b8629502f99fc46fbe28ad17cd173f11259721


---
# <a name="create-an-azure-media-services-account-using-the-azure-portal"></a>Criar uma conta dos Serviços de Multimédia do Azure com o Portal do Azure
> [!div class="op_single_selector"]
> * [Portal](media-services-portal-create-account.md)
> * [PowerShell](media-services-manage-with-powershell.md)
> * [REST](https://docs.microsoft.com/rest/api/media/mediaservice)
> 
> [!NOTE]
> Para concluir este tutorial, precisa de uma conta do Azure. Para obter mais detalhes, consulte [Avaliação Gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/). 
> 
> 

O portal do Azure proporciona uma forma para criar rapidamente uma conta dos Serviços de Multimédia do Azure (AMS). Pode utilizar a sua conta para aceder aos Media Services que permitem armazenar, encriptar, codificar, gerir e transmitir conteúdo no Azure. No momento em que cria uma conta de Media Services, também cria uma conta do Storage associada (ou utilize uma já existente) na mesma região geográfica da conta de Media Services.

Este artigo explica alguns conceitos comuns e mostra como criar uma conta dos Serviços de Multimédia no portal do Azure.

## <a name="concepts"></a>Conceitos
O acesso aos Media Services requer duas contas associadas:

* Uma conta dos Media Services. A sua conta dá-lhe acesso a um conjunto de Media Services baseados na nuvem disponíveis no Azure. Uma conta de Media Services não armazena conteúdo de multimédia real. Em vez disso, armazena os metadados sobre o conteúdo de multimédia e as tarefas de processamento de multimédia na sua conta. No momento que criar a conta, seleciona uma região de Media Services disponível. A região que selecionou é um datacenter que armazena os registos de metadados para a sua conta.
  
    As regiões dos Media Services Disponíveis (AMS) incluem: Europa do Norte, Europa Ocidental, EUA Oeste, EUA Leste, Sudeste Asiático, Ásia Oriental, Oeste do Japão, Leste do Japão. Os Media Services não utilizam grupos de afinidade.
  
    O AMS está, agora, disponível também nos seguintes datacenters: Sul do Brasil, Índia Ocidental, Índia do Sul e Índia Central. Agora, pode utilizar o portal do Azure para criar contas do Serviço de Multimédia e realizar várias tarefas descritas aqui. No entanto, o Live Encoding não está ativado nestes centros de dados. Além disso, nem todos os tipos de Unidades de Codificação Reservadas estão disponíveis nestes centros de dados.
  
  * Sul do Brasil: só estão disponíveis as Unidades de Codificação Reservadas Standard e Básicas.
  * Índia Ocidental, Índia do Sul: 
* Uma conta de armazenamento do Azure. As contas de armazenamento têm de estar localizadas na mesma região geográfica que a conta dos Serviços de Multimédia. Quando cria uma conta de Media Services, pode optar por uma conta do Storage existente na mesma região ou pode criar uma nova conta do Storage na mesma região. Se eliminar uma conta de Media Services, os blobs na sua conta do Storage relacionada não são eliminados.

## <a name="create-an-ams-account"></a>Criar uma conta do AMS
Os passos nesta secção explicam como criar uma conta dos AMS.

1. Inicie sessão no [Portal do Azure](https://portal.azure.com/).
2. Clique em **+Novo** > **Web + Móvel** > **Serviços de Multimédia**.
   
    ![Criar Media Services](./media/media-services-create-account/media-services-new1.png)
3. Em **CRIAR CONTA DE MEDIA SERVICES**, Introduza os valores necessários.
   
    ![Criar Media Services](./media/media-services-create-account/media-services-new3.png)
   
   1. Em **Nome da Conta**, introduza o nome da nova conta de AMS. Um nome de conta dos Serviços de Multimédia é composto por letras minúsculas ou números sem espaços, com 3 a 24 carateres de comprimento.
   2. Na subscrição, selecione entre as diferentes subscrições do Azure disponíveis para si.
   3. Em **Grupo de Recursos**, selecione o recurso novo ou existente.  Um grupo de recursos é uma coleção de recursos que partilham o ciclo de vida, as permissões e as políticas. Sabia mais [aqui](../azure-resource-manager/resource-group-overview.md#resource-groups).
   4. Em **Localização**, selecione a região geográfica que será utilizada para armazenar os registos de metadados da conta de Media Services. Esta região será utilizada para processar e transmitir em fluxo a sua multimédia. Apenas as regiões dos Media Services disponíveis são apresentadas na caixa de lista pendente. 
   5. Em **Conta do Storage**, selecione uma conta do Storage para fornecer o Blob Storage do conteúdo de multimédia da conta de Media Services. Pode selecionar uma conta de armazenamento existente na mesma região geográfica da conta dos Serviços de Multimédia ou pode criar uma conta de armazenamento. É criada uma nova conta do Storage na mesma região. As regras para os nomes da conta do Storage são iguais às das contas dos Media Services.
      
       Saiba mais sobre armazenamento [aqui](../storage/storage-introduction.md).
   6. Selecione **Afixar no dashboard** para ver o progresso da implementação da conta.
4. Clique em **Criar** na parte inferior do formulário.
   
    Depois de criar a conta com êxito, a página de descrição geral é carregada. Na tabela do ponto final de transmissão em fluxo, a conta terá um ponto final de transmissão em fluxo predefinido no estado **Parado**. 

    >[!NOTE]
    >Quando a sua conta AMS é criada, é adicionado um ponto final de transmissão em fluxo **predefinido** à sua conta no estado **Parado**. Para começar a transmitir o seu conteúdo em fluxo e a tirar partido do empacotamento e encriptação dinâmicos, o ponto final de transmissão em fluxo a partir do qual quer transmitir conteúdo tem de estar no estado **Em execução**. 
   
    ![Definições dos Media Services](./media/media-services-create-account/media-services-settings.png)
   
    Para gerir a sua conta de AMS (por exemplo, carregar vídeos, codificar elementos, monitorizar o progresso da tarefa) utilize a janela **Definições**.

## <a name="manage-keys"></a>Gerir Chaves
Necessita do nome da conta e das informações da chave primária para aceder programaticamente à conta de Media Services.

1. No Portal do Azure, selecione a sua conta. 
   
    A janela **Definições** aparece à direita. 
2. Na janela **Definições**, selecione **Chaves**. 
   
    A janela **Gerir chaves** mostra o nome da conta e as chaves primária e secundária são apresentadas. 
3. Prima o botão Copiar para copiar os valores.
   
    ![Chaves dos Media Services](./media/media-services-create-account/media-services-keys.png)

## <a name="next-steps"></a>Passos seguintes
Agora, pode carregar ficheiros para a sua conta do AMS. Para obter mais informações, veja [Carregar ficheiros](media-services-portal-upload-files.md).

## <a name="media-services-learning-paths"></a>Percursos de aprendizagem dos Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Enviar comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]




<!--HONumber=Feb17_HO2-->


