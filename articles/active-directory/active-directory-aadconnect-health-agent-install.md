---
title: "Instalação do agente do Azure AD Connect Health | Microsoft Docs"
description: "Esta é a página do Azure AD Connect Health que descreve a instalação do agente para AD FS e sincronização."
services: active-directory
documentationcenter: 
author: karavar
manager: samueld
editor: curtand
ms.assetid: 1cc8ae90-607d-4925-9c30-6770a4bd1b4e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 10/18/2016
ms.author: vakarand
translationtype: Human Translation
ms.sourcegitcommit: dcda8b30adde930ab373a087d6955b900365c4cc
ms.openlocfilehash: e219423b238fc1384270f8341ffc7421954f3264


---
# <a name="azure-ad-connect-health-agent-installation"></a>Instalação do Agente do Azure AD Connect Health
Este documento descreve a instalação e a configuração dos Agentes do Azure AD Connect Health. Pode transferir os agentes de [aqui](active-directory-aadconnect-health.md#download-and-install-azure-ad-connect-health-agent).

## <a name="requirements"></a>Requisitos
A tabela seguinte é uma lista de requisitos para utilizar o Azure AD Connect Health.

| Requisito | Descrição |
| --- | --- |
| Azure AD Premium |O Azure AD Connect Health é uma funcionalidade do Azure AD Premium e requer o Azure AD Premium. </br></br>Para obter mais informações, veja [ Introdução ao Azure AD Premium](active-directory-get-started-premium.md) </br>Para iniciar uma versão de avaliação gratuita de 30 dias, veja [Iniciar uma versão de avaliação.](https://azure.microsoft.com/trial/get-started-active-directory/) |
| Tem de ser um administrador global do seu Azure AD para começar a utilizar o Azure AD Connect Health |Por predefinição, apenas os administradores globais podem instalar e configurar os agentes de estado de funcionamento para iniciar, aceder ao portal e executar operações no Azure AD Connect Health. Para obter mais informações, veja [Administrar o diretório do Azure AD](active-directory-administer.md). <br><br> Utilizando um Controlo de Acesso Baseado em Funções, pode permitir o acesso ao Azure AD Connect Health a outros utilizadores na sua organização. Para obter mais informações, veja [Role Based Access Control for Azure AD Connect Health (Controlo de Acesso Baseado em Funções para o Azure AD Connect Health).](active-directory-aadconnect-health-operations.md#manage-access-with-role-based-access-control) </br></br>**Importante:** a conta utilizada ao instalar os agentes tem de ser uma conta escolar ou profissional. Não pode ser uma conta Microsoft. Para obter mais informações, veja [Sign up for Azure as an organization (Inscrever-se no Azure como uma organização)](sign-up-organization.md) |
| O Agente do Azure AD Connect Health é instalado em cada servidor de destino |O Azure AD Connect Health requer a instalação de um agente nos servidores de destino, para fornecer os dados que são apresentados no portal. </br></br>Por exemplo, para obter dados da sua infraestrutura do AD FS no local, o agente tem de estar instalado nos servidores do AD FS, nos servidores Proxy do AD FS e nos servidores Proxy de Aplicações Web. Do mesmo modo, para obter os dados na sua infraestrutura local do AD DS, o agente tem de ser instalado nos controladores de domínio. </br></br>**Importante:** a conta utilizada ao instalar os agentes tem de ser uma conta escolar ou profissional. Não pode ser uma conta Microsoft. Para obter mais informações, veja [Sign up for Azure as an organization (Inscrever-se no Azure como uma organização)](sign-up-organization.md) |
| Conectividade de saída para os pontos finais de serviço do Azure |Durante a instalação e o tempo de execução, o agente requer conectividade aos pontos finais do serviço do Azure AD Connect Health. Se a conectividade de saída for bloqueada, certifique-se de que os pontos finais seguintes são adicionados à lista de permissões: </br></br><li>&#42;.blob.core.windows.net </li><li>&#42;.queue.core.windows.net</li><li>adhsprodwus.servicebus.windows.net - Port: 5671 </li><li>https://management.azure.com </li><li>https://s1.adhybridhealth.azure.com/</li><li>https://policykeyservice.dc.ad.msft.net/</li><li>https://login.windows.net</li><li>https://login.microsoftonline.com</li><li>https://secure.aadcdn.microsoftonline-p.com</li> |
| Portas da firewall do servidor onde o agente é executado. |O agente requer que as seguintes portas de firewall estejam abertas para que possa comunicar com os pontos finais de serviço do Azure AD Health.</br></br><li>TCP/UDP port 443</li><li>TCP/UDP port 5671</li> |
| Permitir os seguintes Web sites, caso esteja ativada a Segurança Avançada do IE |Se a Segurança Avançada do IE estiver ativada, os Web sites seguintes têm de ser permitidos no servidor no qual o agente vai ser instalado.</br></br><li>https://login.microsoftonline.com</li><li>https://secure.aadcdn.microsoftonline-p.com</li><li>https://login.windows.net</li><li>O servidor de federação para a sua organização considerado fidedigno pelo o Azure Active Directory. Por exemplo: https://sts.contoso.com</li> |

## <a name="installing-the-azure-ad-connect-health-agent-for-ad-fs"></a>Instalar o agente do Azure AD Connect Health para o AD FS
Para iniciar a instalação do agente, faça duplo clique no ficheiro .exe que transferiu. No primeiro ecrã, clique em Instalar.

![Verificar o Azure AD Connect Health](./media/active-directory-aadconnect-health-requirements/install1.png)

Uma vez concluída a instalação, clique em Configurar Agora.

![Verificar o Azure AD Connect Health](./media/active-directory-aadconnect-health-requirements/install2.png)

É iniciada uma linha de comandos, seguida de alguns comandos do PowerShell, que executam Register-AzureADConnectHealthADFSAgent. Quando lhe for pedido para iniciar sessão no Azure, continue e inicie-a.

![Verificar o Azure AD Connect Health](./media/active-directory-aadconnect-health-requirements/install3.png)

Depois de iniciar sessão, o PowerShell prosseguirá. Uma vez concluído, pode fechá-lo e a configuração estará concluída.

Nesta altura, os serviços deverão ser iniciados automaticamente, permitindo ao agente monitorizar e recolher dados. Se não tiver cumprido todos os pré-requisitos que foram descritos nas secções anteriores, são apresentados avisos na janela do PowerShell. Antes de instalar o agente, certifique-se de que concluiu os [requisitos](active-directory-aadconnect-health-agent-install.md#requirements). A captura de ecrã seguinte mostra um exemplo destes erros.

![Verificar o Azure AD Connect Health](./media/active-directory-aadconnect-health-requirements/install4.png)

Para verificar se o agente foi instalado, procure os serviços seguintes no servidor. Se concluiu a configuração, já devem estar a ser executados. Caso contrário, são parados até que a configuração esteja concluída.

* Serviço de Diagnóstico do Azure AD Connect Health AD FS
* Serviço de Informações do Azure AD Connect Health AD FS
* Serviço de Monitorização do Azure AD Connect Health AD FS

![Verificar o Azure AD Connect Health](./media/active-directory-aadconnect-health-requirements/install5.png)

### <a name="agent-installation-on-windows-server-2008-r2-servers"></a>Instalação do agente em servidores do Windows Server 2008 R2
Passos para servidores do Windows Server 2008 R2:

1. Certifique-se de que o servidor está a ser executado com o Service Pack 1 ou superior.
2. Desative o IE ESC para instalação de agentes:
3. Antes de instalar o agente do AD Health, instale o Windows PowerShell 4.0 em cada um dos servidores. Para instalar o Windows PowerShell 4.0:
   * Instale o [Microsoft .NET Framework 4.5](https://www.microsoft.com/download/details.aspx?id=40779) utilizando a seguinte ligação para transferir o instalador offline.
   * Instale o ISE do PowerShell (a partir de Funcionalidades do Windows)
   * Instale o [Windows Management Framework 4.0.](https://www.microsoft.com/download/details.aspx?id=40855)
   * Instale no servidor o Internet Explorer versão 10 ou posterior. (É um requisito do Serviço de Integridade para o autenticar com as suas credenciais de administrador do Azure.)
4. Para obter mais informações sobre como instalar o Windows PowerShell 4.0 no Windows Server 2008 R2, veja o artigo wiki [aqui](http://social.technet.microsoft.com/wiki/contents/articles/20623.step-by-step-upgrading-the-powershell-version-4-on-2008-r2.aspx).

### <a name="enable-auditing-for-ad-fs"></a>Ativar a auditoria para o AD FS
> [!NOTE]
> Esta secção aplica-se apenas aos servidores de federação do AD FS.
> 
> 

Para que a funcionalidade de Análise de Utilização possa recolher e analisar dados, o agente do Azure AD Connect Health precisa das informações nos Registos de Auditoria do AD FS. Estes registos não estão ativados por predefinição. Utilize os procedimentos seguintes para ativar a auditoria do AD FS e para localizar os registos de auditoria do AD FS nos servidores AD FS.

#### <a name="to-enable-auditing-for-ad-fs-20"></a>Para ativar a auditoria para o AD FS 2.0
1. Clique em **Iniciar**, aponte para **Programas**, aponte para **Ferramentas Administrativas** e, em seguida, clique em **Política de Segurança Local**.
2. Navegue até à pasta **Security Settings\Local Policies\User Rights Management** e, em seguida, faça duplo clique em Gerar auditorias de segurança.
3. No separador **Definição de Segurança Local**, certifique-se de que a conta de serviço do AD FS 2.0 está listada. Se não estiver presente, clique em **Adicionar Utilizador ou Grupo**, adicione-a à lista e, em seguida, clique em **OK**.
4. Para ativar a auditoria, abra uma linha de comandos com privilégios elevados e execute o comando seguinte: <code>auditpol.exe /set /subcategory:"Application Generated" /failure:enable /success:enable</code>
5. Feche a Política de Segurança Local e, em seguida, abra o snap-in Gestão. Para abrir o snap-in Gestão, clique em **Iniciar**, aponte para **Programas**, aponte para **Ferramentas Administrativas** e, em seguida, clique em AD FS 2.0 Gestão.
6. No painel Ações, clique em Editar Propriedades do Serviço de Federação.
7. Na caixa de diálogo **Propriedades do Serviço de Federação**, clique no separador **Eventos**.
8. Selecione as caixas de verificação **Auditorias de êxito** e **Auditorias de falha**.
9. Clique em **OK**.

#### <a name="to-enable-auditing-for-ad-fs-on-windows-server-2012-r2"></a>Para ativar a auditoria para o AD FS no Windows Server 2012 R2
1. Abra a **Política de Segurança Local** abrindo o **Gestor de Servidores** no ecrã Iniciar ou o Gestor de Servidores na barra de tarefas no ambiente de trabalho e clique em **Ferramentas/Política de Segurança Local**.
2. Navegue até à pasta **Security Settings\Local Policies\User Rights Assignment** e, em seguida, faça duplo clique em **Gerar auditorias de segurança**.
3. No separador **Definição de Segurança Local**, certifique-se de que a conta de serviço do AD FS está listada. Se não estiver presente, clique em **Adicionar Utilizador ou Grupo**, adicione-a à lista e, em seguida, clique em **OK**.
4. Para ativar a auditoria, abra uma linha de comandos com privilégios elevados e execute o comando seguinte: <code>auditpol.exe /set /subcategory:"Application Generated" /failure:enable /success:enable.</code>
5. Feche **Política de Segurança Local** e, em seguida, abra o snap-in **Gestão do AD FS** (no Gestor de Servidores, clique em Ferramentas e selecione Gestão do AD FS).
6. No painel Ações, clique em **Editar Propriedades do Serviço de Federação**.
7. Na caixa de diálogo Propriedades do Serviço de Federação, clique no separador **Eventos**.
8. Selecione as caixas de verificação **Auditorias de êxito e Auditorias de falha** e clique em **OK**.

#### <a name="to-locate-the-ad-fs-audit-logs"></a>Para localizar os registos de auditoria do AD FS
1. Abra o **Visualizador de Eventos**.
2. Aceda aos Registos do Windows e selecione **Segurança**.
3. À direita, clique em **Filtrar os Registos Atuais**.
4. Em Origem do evento, selecione **Auditoria do AD FS**.

![Registos de auditoria do AD FS](./media/active-directory-aadconnect-health-requirements/adfsaudit.png)

> [!WARNING]
> Se existir uma política de grupo que desative a auditoria do AD FS, o Agente do Azure AD Connect Health não conseguirá recolher informações. Certifique-se de que não tem uma política de grupo que possa estar a desativar a auditoria.
> 
> 

[//]: # (Start of Agent Proxy Configuration Section)

## <a name="installing-the-azure-ad-connect-health-agent-for-sync"></a>Instalar o agente Azure AD Connect Health para sincronização
O agente do Azure AD Connect Health para sincronização é instalado automaticamente na compilação mais recente do Azure AD Connect. Para utilizar o Azure AD Connect para sincronização, tem de transferir a versão mais recente do Azure AD Connect e instalá-la. Pode transferir a versão mais recente [aqui](http://www.microsoft.com/download/details.aspx?id=47594).

Para verificar se o agente foi instalado, procure os serviços seguintes no servidor. Se concluiu a configuração, já devem estar a ser executados. Caso contrário, são parados até que a configuração esteja concluída.

* Serviço de Informações do Azure AD Connect Health Sincronização
* Serviço de Monitorização do Azure AD Connect Health Sincronização

![Verificar o Azure AD Connect Health para sincronização](./media/active-directory-aadconnect-health-sync/services.png)

> [!NOTE]
> Lembre-se de que a utilização do Azure AD Connect Health requer o Azure AD Premium. Se não tiver o Azure AD Premium, não conseguirá concluir a configuração no portal do Azure. Para obter mais informações, veja a [página de requisitos](active-directory-aadconnect-health-agent-install.md#requirements).
> 
> 

## <a name="manual-azure-ad-connect-health-for-sync-registration"></a>Registo manual do Azure AD Connect Health para sincronização
Se o registo do agente Azure AD Connect Health para sincronização falhar após a instalação com êxito o Azure AD Connect, pode utilizar o seguinte comando do PowerShell para registar manualmente o agente.

> [!IMPORTANT]
> Só é necessário utilizar este comando PowerShell se falhar o registo do agente depois de instalar o Azure AD Connect.
> 
> 

O comando do PowerShell seguinte SÓ é necessário se o registo do agente de estado de funcionamento falhar, mesmo após a instalação e configuração com êxito do Azure AD Connect. Quando o agente for registado com êxito, os serviços do Azure AD Connect Health são iniciados.

Pode registar manualmente o agente do Azure AD Connect Health para sincronização com o seguinte comando do PowerShell:

`Register-AzureADConnectHealthSyncAgent -AttributeFiltering $false -StagingMode $false`

O comando recebe os seguintes parâmetros:

* AttributeFiltering: $true (predefinição) - se o Azure AD Connect não estiver a sincronizar o conjunto predefinido de atributos e tiver sido personalizado para utilizar um conjunto filtrado de atributos. $false, caso contrário.
* StagingMode: $false (predefinição) - se o servidor do Azure AD Connect NÃO estiver no modo de teste, $true se o servidor estiver configurado para estar no modo de teste.

Quando lhe for pedida a autenticação, deve utilizar a mesma conta de administrador global (por exemplo, admin@domain.onmicrosoft.com) que foi utilizada para configurar o Azure AD Connect.

## <a name="installing-the-azure-ad-connect-health-agent-for-ad-ds"></a>Instalar o Agente Azure AD Connect Health para o AD DS
Para iniciar a instalação do agente, faça duplo clique no ficheiro .exe que transferiu. No primeiro ecrã, clique em Instalar.

![Verificar o Azure AD Connect Health](./media/active-directory-aadconnect-health/aadconnect-health-adds-agent-install1.png)

Uma vez concluída a instalação, clique em Configurar Agora.

![Verificar o Azure AD Connect Health](./media/active-directory-aadconnect-health/aadconnect-health-adds-agent-install2.png)

É iniciada uma linha de comandos, seguida de alguns comandos do PowerShell, que executam Register-AzureADConnectHealthADDSAgent. Quando lhe for pedido para iniciar sessão no Azure, continue e inicie-a.

![Verificar o Azure AD Connect Health](./media/active-directory-aadconnect-health/aadconnect-health-adds-agent-install3.png)

Depois de iniciar sessão, o PowerShell prosseguirá. Uma vez concluído, pode fechá-lo e a configuração estará concluída.

Nesta altura, os serviços deverão ser iniciados automaticamente, permitindo ao agente monitorizar e recolher dados. Se não tiver cumprido todos os pré-requisitos que foram descritos nas secções anteriores, são apresentados avisos na janela do PowerShell. Antes de instalar o agente, certifique-se de que concluiu os [requisitos](active-directory-aadconnect-health-agent-install.md#requirements). A captura de ecrã seguinte mostra um exemplo destes erros.

![Verificar o Azure AD Connect Health para o AD DS](./media/active-directory-aadconnect-health/aadconnect-health-adds-agent-install4.png)

Para verificar se o agente foi instalado, procure os serviços seguintes no controlador de domínio.

* Serviço de Informações do Azure AD Connect Health AD DS
* Serviço de Monitorização do Azure AD Connect Health AD DS

Se concluiu a configuração, estes serviços já devem estar a ser executados. Caso contrário, são parados até que a configuração esteja concluída.

![Verificar o Azure AD Connect Health](./media/active-directory-aadconnect-health/aadconnect-health-adds-agent-install5.png)

## <a name="installing-the-azure-ad-connect-health-agent-for-ad-ds-on-server-core"></a>Instalar o Agente Azure AD Connect Health para o AD DS no Server Core
Depois de instalar o ficheiro .exe, pode concluir o processo de registo com o seguinte comando do PowerShell:

`Register-AzureADConnectHealthADDSAgent -Credential $cred`

## <a name="configure-azure-ad-connect-health-agents-to-use-http-proxy"></a>Configurar os Agentes do Azure AD Connect Health para utilizarem o Proxy de HTTP
Pode configurar os Agentes do Azure AD Connect Health para trabalharem com um Proxy de HTTP.

> [!NOTE]
> * A utilização de “Netsh WinHttp define ProxyServerAddress” não é suportada, uma vez que o agente utiliza System.Net para fazer pedidos Web em vez dos Serviços HTTP do Microsoft Windows.
> * O endereço Http Proxy configurado é utilizado para fazer o pass-through de mensagens Https encriptadas.
> * Proxies autenticados (utilizando HTTPBasic) não são suportados.
> 
> 

### <a name="change-health-agent-proxy-configuration"></a>Alterar a configuração de Proxy do Agente de Estado de Funcionamento
Tem as seguintes opções para configurar o Agente do Azure AD Connect Health para utilizar um Proxy de HTTP.

> [!NOTE]
> Para que as definições de proxy sejam atualizadas, têm de ser reiniciados todos os serviços do Agente do Azure AD Connect Health. Execute o seguinte comando:<br>
> Restart-Service AdHealth*
> 
> 

#### <a name="import-existing-proxy-settings"></a>Importar Definições de proxy existente
##### <a name="import-from-internet-explorer"></a>Importar do Internet Explorer
As definições de proxy de HTTP do Internet Explorer podem ser importadas para serem utilizadas pelos Agentes do Azure AD Connect Health. Em cada um dos servidores que executem o Agente de estado de funcionamento, execute o seguinte comando do PowerShell:

    Set-AzureAdConnectHealthProxySettings -ImportFromInternetSettings

##### <a name="import-from-winhttp"></a>Importar do WinHTTP
As definições de proxy de WinHTTP podem ser importadas para serem utilizadas pelos Agentes do Azure AD Connect Health. Em cada um dos servidores que executem o Agente de estado de funcionamento, execute o seguinte comando do PowerShell:

    Set-AzureAdConnectHealthProxySettings -ImportFromWinHttp

#### <a name="specify-proxy-addresses-manually"></a>Especificar manualmente endereços Proxy
Pode especificar manualmente um servidor proxy em cada servidor que executa o Agente de Estado de Funcionamento, através do seguinte comando do PowerShell:

    Set-AzureAdConnectHealthProxySettings -HttpsProxyAddress address:port

Exemplo: *Set-AzureAdConnectHealthProxySettings -HttpsProxyAddress myproxyserver: 443*

* “address” pode ser um nome de servidor DNS resolvível ou um endereço IPv4
* pode ser omitida a “porta”. Se for omitida, então 443 é escolhida como porta predefinida.

#### <a name="clear-existing-proxy-configuration"></a>Limpar a configuração de proxy existente
Pode limpar a configuração de proxy existente ao executar o seguinte comando:

    Set-AzureAdConnectHealthProxySettings -NoProxy


### <a name="read-current-proxy-settings"></a>Ler as definições de proxy atuais
Pode ler as definições de proxy atualmente configuradas ao executar o seguinte comando:

    Get-AzureAdConnectHealthProxySettings


## <a name="test-connectivity-to-azure-ad-connect-health-service"></a>Testar a conectividade ao Serviço Azure AD Connect Health
É possível que possam surgir problemas que levem o agente do Azure AD Connect Health a perder a conectividade ao serviço do Azure AD Connect Health. Incluem problemas de rede, problemas de permissão ou vários outros motivos.

Se o agente não conseguir enviar dados para o serviço do Azure AD Connect Health durante mais de duas horas, é apresentado o alerta no portal “Os dados do Serviço de Estado de Funcionamento não estão atualizados”. Pode confirmar se o agente do Azure AD Connect Health consegue carregar dados para este serviço ao executar o seguinte comando do PowerShell:

    Test-AzureADConnectHealthConnectivity -Role ADFS

O parâmetro de função toma atualmente os seguintes valores:

* ADFS
* Sync
* AD DS

Pode utilizar o sinalizador - ShowResults no comando para ver registos detalhados. Utilize o seguinte exemplo:

    Test-AzureADConnectHealthConnectivity -Role Sync -ShowResult

> [!NOTE]
> Para utilizar a ferramenta de conectividade, primeiro tem de concluir o registo do agente. Se não conseguir concluir o registo do agente, certifique-se de que cumpriu todos os [requisitos](active-directory-aadconnect-health-agent-install.md#requirements) do Azure AD Connect Health. Este teste de conectividade é efetuado por predefinição durante o registo do agente.
> 
> 

## <a name="related-links"></a>Ligações relacionadas
* [Azure AD Connect Health](active-directory-aadconnect-health.md)
* [Azure AD Connect Health Operations (Operações do Azure AD Connect Health)](active-directory-aadconnect-health-operations.md)
* [Utilizar o Azure AD Connect Health com o AD FS](active-directory-aadconnect-health-adfs.md)
* [Utilizar o Azure AD Connect Health para sincronização](active-directory-aadconnect-health-sync.md)
* [Utilizar o Azure AD Connect Health com o AD DS](active-directory-aadconnect-health-adds.md)
* [FAQ do Azure AD Connect Health](active-directory-aadconnect-health-faq.md)
* [Histórico das Versões do Azure AD Connect Health](active-directory-aadconnect-health-version-history.md)




<!--HONumber=Dec16_HO1-->


