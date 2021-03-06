---
title: Utilizar SSH com o HDInsight (Hadoop) a partir de Windows, Linux, Unix ou OS X | Microsoft Docs
description: " Pode aceder ao HDInsight através do Secure Shell (SSH). Este documento disponibiliza informações sobre a utilização do SSH para ligar ao HDInsight a partir de clientes Windows, Linux, Unix ou OS X."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: a6a16405-a4a7-4151-9bbf-ab26972216c5
ms.service: hdinsight
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/16/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
translationtype: Human Translation
ms.sourcegitcommit: 4f2230ea0cc5b3e258a1a26a39e99433b04ffe18
ms.openlocfilehash: 89d44476e9de8ac32195efaf66535cdd9fb4260e
ms.lasthandoff: 03/25/2017

---
# <a name="connect-to-hdinsight-hadoop-using-ssh"></a>Ligar ao HDInsight (Hadoop) através de SSH

Saiba como utilizar [Secure Shell (SSH)](https://en.wikipedia.org/wiki/Secure_Shell) para ligar de forma segura ao HDInsight. O HDInsight pode utilizar o Linux (Ubuntu) como o sistema operativo dos nós dentro do cluster. O SSH pode ser utilizado para ligar os nós principais e de extremidade de clusters baseados no Linux e executar comandos nesses nós.

A tabela seguinte contém as informações de portas e de endereços necessárias quando se liga ao HDInsight através do SSH:

| Endereço | Porta | Liga-se a... |
| ----- | ----- | ----- |
| `<edgenodename>.<clustername>-ssh.azurehdinsight.net` | 22 | Nó de extremidade (se existir) |
| `<clustername>-ssh.azurehdinsight.net` | 22 | Nó principal primário |
| `<clustername>-ssh.azurehdinsight.net` | 23 | Nó principal secundário |

> [!NOTE]
> Substitua `<edgenodename>` pelo nome do nó de extremidade. Para obter mais informações sobre a utilização de nós de extremidade, veja [Use edge nodes in HDInsight](hdinsight-apps-use-edge-node.md#access-an-edge-node) (Utilizar nós de extremidade no HDInsight).
>
> Substitua `<clustername>` pelo nome do seu cluster do HDInsight.
>
> Recomendamos __ligar sempre ao nó de extremidade__, se tiver um. Os nós principais alojam serviços que são fundamentais para o estado de funcionamento do cluster. O nó de extremidade executa apenas o que colocar no mesmo.

## <a name="ssh-clients"></a>Clientes SSH

A maioria dos sistemas operativos fornecem o cliente `ssh`. O Microsoft Windows não fornece um cliente SSH por predefinição. Está disponível um cliente SSG para Windows em cada um dos pacotes seguintes:

* [Bash no Ubuntu no Windows 10](https://msdn.microsoft.com/commandline/wsl/about): o comando `ssh` é fornecido na linha de comandos Bash no Windows.

* [Git (https://git-scm.com/)](https://git-scm.com/): o comando `ssh` é facultado através da linha de comandos GitBash.

* [GitHub Desktop (https://desktop.github.com/)](https://desktop.github.com/) o comando `ssh` é fornecido através da linha de comandos Git Shell. O GitHub Desktop pode ser configurado para utilizar Bash, a Linha de Comandos do Windows ou no PowerShell como a linha ed comandos para o Git Shell.

* [OpenSSH (https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)](https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH): a equipa do PowerShell está a migrar o OpenSSH para o Windows e disponibiliza versões de teste.

    > [!WARNING]
    > O pacote OpenSSH inclui o componente de servidor SSH, `sshd`. Este componente inicia um servidor SSH no seu sistema, permitindo que outras pessoas se liguem ao mesmo. Não configure este componente nem abra a porta 22, a não ser que queira alojar um servidor SSH no seu sistema. Não é necessário para comunicar com o HDInsight.

Também existem vários clientes SSH gráficos, tais como [PuTTY (http://www.chiark.greenend.org.uk/~sgtatham/putty/)](http://www.chiark.greenend.org.uk/~sgtatham/putty/) e [MobaXterm (http://mobaxterm.mobatek.net/)](http://mobaxterm.mobatek.net/). Embora estes clientes possam ser utilizados para ligar ao HDInsight, o processo de ligação a um servidor é diferente relativamente à utilização do utilitário `ssh`. Para obter mais informações, veja a documentação do cliente gráfico que está a utilizar.

## <a id="sshkey"></a>Autenticação: chaves SSH

As chaves SSH utilizam a [encriptação de chave pública](https://en.wikipedia.org/wiki/Public-key_cryptography) para proteger o cluster. As chaves SSH são mais seguras do que as palavras-passe e proporcionam uma forma fácil de proteger o seu cluster do HDInsight.

Se a sua conta SSH for protegida com uma chave, o cliente tem de fornecer a chave privada correspondente quando se ligar:

* A maioria dos clientes podem ser configurados para utilizar uma __chave predefinida__. Por exemplo, o cliente `ssh` procura uma chave privada em `~/.ssh/id_rsa` nos ambientes Linux e Unix.

* Pode especificar o __caminho para uma chave privada__. Com o cliente `ssh`, o parâmetro `-i` é utilizado para especificar o caminho para a chave privada. Por exemplo, `ssh -i ~/.ssh/hdinsight sshuser@myedge.mycluster-ssh.azurehdinsight.net`.

* Se tiver __várias chaves privadas__ para utilização com diferentes servidores, podem ser utilizados utilitários como [ssh-agente (https://en.wikipedia.org/wiki/Ssh-agent)](https://en.wikipedia.org/wiki/Ssh-agent) para selecionar automaticamente a chave a utilizar.

> [!IMPORTANT]
>
> Se proteger a chave privada com uma frase de acesso, tem de introduzi-la quando utilizar a chave. Utilitários como `ssh-agent` podem colocar em cache a palavra-passe, para sua comodidade.

### <a name="create-an-ssh-key-pair"></a>Criar um par de chaves SSH

Utilize o comando `ssh-keygen` para criar ficheiros de chaves públicas e privadas. O comando seguinte gera um par de chaves RSA de 2048 bits que pode ser utilizado com o HDInsight:

    ssh-keygen -t rsa -b 2048

São-lhe pedidas informações durante o processo de criação de chaves. Por exemplo, onde estão armazenadas as chaves ou se pretende utilizar uma frase de acesso. Após a conclusão do processo, são criados dois ficheiros: uma chave pública e uma chave privada.

* A __chave pública__ é utilizada para criar um cluster do HDInsight. A chave pública tem a extensão `.pub`.

* A __chave privada__ é utilizada para autenticar o cliente no cluster do HDInsight.

> [!IMPORTANT]
> Pode utilizar uma frase de acesso para proteger as chaves. Esta trata-se, efetivamente, de uma palavra-passe na sua chave privada. Mesmo se alguém obtiver a sua chave privada, essa pessoa tem de ter a frase de acesso para poder utilizá-la.

### <a name="create-hdinsight-using-the-public-key"></a>Utilizar a chave pública para criar o HDInsight

| Método de criação | Como utilizar a chave pública |
| ------- | ------- |
| **Portal do Azure** | Desmarque __Utilizar a mesma palavra-passe de início de sessão do cluster__ e selecione __Chave Pública__ como o tipo de autenticação SSH. Por fim, selecione o ficheiro de chave pública ou cole os conteúdos de texto do ficheiro no campo __Chave pública SSH__.</br>![Caixa de diálogo Chave pública SSH na criação do cluster do HDInsight](./media/hdinsight-hadoop-linux-use-ssh-unix/create-hdinsight-ssh-public-key.png) |
| **Azure PowerShell** | Utilize o parâmetro `-SshPublicKey` do cmdlet `New-AzureRmHdinsightCluster` e transmita os conteúdos da chave pública como uma cadeia.|
| **CLI do Azure 1.0** | Utilize o parâmetro `--sshPublicKey` do comando `azure hdinsight cluster create` e transmita os conteúdos da chave pública como uma cadeia. |
| **Modelo do Resource Manager** | Para obter um exemplo de como utilizar chaves SSH com um modelo, veja [Deploy HDInsight on Linux with SSH key](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-ssh-publickey/) (Implementar o HDInsight no Linux com uma chave SSH). O elemento `publicKeys` no ficheiro [azuredeploy.json](https://github.com/Azure/azure-quickstart-templates/blob/master/101-hdinsight-linux-ssh-publickey/azuredeploy.json) é utilizado para transmitir as chaves ao Azure ao criar o cluster. |

## <a id="sshpassword"></a>Autenticação: palavra-passe

As contas SSH podem ser protegidas através de palavra-passe. Quando utiliza SSH para se ligar ao HDInsight, é-lhe pedido que introduza a palavra-passe.

> [!WARNING]
> Não recomendamos utilizar a autenticação por palavra-passe para SSH. As palavras-passe podem ser descobertas e são vulneráveis a ataques de força bruta. Em vez disso, recomendamos que utilize [chaves SSH para a autenticação](#sshkey).

### <a name="create-hdinsight-using-a-password"></a>Utilizar uma palavra-passe para criar o HDInsight

| Método de criação | Como especificar a palavra-passe |
| --------------- | ---------------- |
| **Portal do Azure** | Por predefinição, a conta de utilizador SSH tem a mesma palavra-passe da conta de início de sessão do cluster. Para utilizar outra palavra-passe, desmarque __Utilizar a mesma palavra-passe de início de sessão do cluster__ e introduza a palavra-passe no campo __Palavra-passe SSH__.</br>![Caixa de diálogo Palavra-passe SSH na criação do cluster do HDInsight](./media/hdinsight-hadoop-linux-use-ssh-unix/create-hdinsight-ssh-password.png)|
| **Azure PowerShell** | Utilize o parâmetro `--SshCredential` do cmdlet `New-AzureRmHdinsightCluster` e transmita um objeto `PSCredential` que contenha o nome e a palavra-passe da conta de utilizador SSH. |
| **CLI do Azure 1.0** | Utilize o parâmetro `--sshPassword` do comando `azure hdinsight cluster create` e indique o valor da palavra-passe. |
| **Modelo do Resource Manager** | Para obter um exemplo de como utilizar a palavra-passe com um modelo, veja [Deploy HDInsight on Linux with SSH password](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-ssh-password/) (Implementar o HDInsight no Linux com uma palavra-passe SSH). O elemento `linuxOperatingSystemProfile` no ficheiro [azuredeploy.json](https://github.com/Azure/azure-quickstart-templates/blob/master/101-hdinsight-linux-ssh-password/azuredeploy.json) é utilizado para transmitir o nome e a palavra-passe da conta SSH ao Azure ao criar o cluster.|

### <a name="change-the-ssh-password"></a>Alterar a palavra-passe SSH

Para obter informações sobre como alterar a palavra-passe da conta do utilizador SSH, veja a secção __Change passwords__ (Alterar palavras-passe) do documento [Manage HDInsight](hdinsight-administer-use-portal-linux.md#change-passwords) (Gerir o HDInsight).

## <a id="domainjoined"></a>Autenticação: HDInsight associado a um domínio

Se estiver a utilizar um __cluster do HDInsight associado a um domínio__, tem de utilizar o comando `kinit` depois de se ligar com SSH. Este comando pede-lhe um utilizador e uma palavra-passe de domínio e autentica a sua sessão com o domínio do Azure Active Directory associado ao cluster.

Para obter mais informações, veja [Configure domain-joined HDInsight](hdinsight-domain-joined-configure.md) (Configurar o HDInsight associado a um domínio).

## <a name="connect-to-worker-and-zookeeper-nodes"></a>Ligar a nós de trabalho e Zookeeper

Os nós de trabalho e os nós Zookeeper não estão diretamente acessíveis a partir da Internet, mas é possível aceder-lhes a partir dos nós principais ou de extremidade do cluster. Seguem-se os passos gerais necessários para ligar a outros nós:

1. Utilizar o SSH para ligar a um nó principal ou de extremidade:

        ssh sshuser@myedge.mycluster-ssh.azurehdinsight.net

2. A partir da ligação SSH ao nó principal ou de extremidade, utilize o comando `ssh` para ligar a um nó de trabalho no cluster:

        ssh sshuser@wn0-myhdi

    Para obter uma lista dos nomes de domínio dos nós no cluster, veja os exemplos no documento [Manage HDInsight by using the Ambari REST API](hdinsight-hadoop-manage-ambari-rest-api.md#example-get-the-fqdn-of-cluster-nodes) (Gerir o HDInsight com a API REST Ambari).

Se a conta SSH estiver protegida por uma __palavra-passe__, é-lhe pedido que a introduza e a ligação é, então, estabelecida.

Se estiver protegida por __chaves SSH__, tem de confirmar que o seu ambiente local está configurado para o reencaminhamento de agentes SSH.

> [!NOTE]
> Outra forma de aceder diretamente a todos os nós do cluster é instalar HDInsight numa Rede Virtual do Azure. Depois, pode associar o computador remoto à mesma rede virtual e aceder diretamente a todos os nós no cluster.
>
> Para obter mais informações, veja [Use a virtual network with HDInsight](hdinsight-extend-hadoop-virtual-network.md) (Utilizar uma rede virtual com o HDInsight).

### <a name="configure-ssh-agent-forwarding"></a>Configurar o reencaminhamento de agentes SSH

> [!IMPORTANT]
> Os passos abaixo pressupõem uma sistema baseado em Linux/UNIX e funcionam com o Bash on Windows 10. Se não funcionarem no seu sistema, poderá ter de ver a documentação do seu cliente SSH.

1. Utilizando um editor de texto, abra `~/.ssh/config`. Se este ficheiro não existir, pode criá-lo ao introduzir `touch ~/.ssh/config` na linha de comandos.

2. Adicione o texto seguinte ao ficheiro `config`.

        Host <edgenodename>.<clustername>-ssh.azurehdinsight.net
          ForwardAgent yes

    Substitua as informações do __Anfitrião__ pelo endereço do nó ao qual se liga com SSH. O exemplo anterior utiliza o nó de extremidade. Esta entrada configura o reencaminhamento de agentes SSH para o nó especificado.

3. Teste o reencaminhamento de agente SSH ao utilizar o comando seguinte no terminal:

        echo "$SSH_AUTH_SOCK"

    Este comando devolve informações semelhantes ao texto seguinte:

        /tmp/ssh-rfSUL1ldCldQ/agent.1792

    Se não forem devolvidas informações, então, `ssh-agent` não está em execução. Veja as informações de script de arranque do agente em [Using ssh-agent with ssh (http://mah.everybody.org/docs/ssh)](http://mah.everybody.org/docs/ssh) ou consulte a documentação do seu cliente SSH para obter os passos específicos relativos à instalação e configuração de `ssh-agent`.

4. Depois de verificar que o **ssh-agent** está em execução, utilize o seguinte para adicionar a chave privada SSH ao agente:

        ssh-add ~/.ssh/id_rsa

    Se a chave privada estiver armazenada num ficheiro diferente, substitua `~/.ssh/id_rsa` pelo caminho para o ficheiro.

5. Utilize SSH para ligar aos nós de extremidade ou principais do cluster. Em seguida, utilize o comando SSH para ligar a um nó de trabalho ou zookeeper. A ligação é estabelecida com a chave reencaminhada.

## <a name="next-steps"></a>Passos seguintes

* [Use SSH tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) (Utilizar túnel SSH com o HDInsight)
* [Use a virtual network with HDInsight](hdinsight-extend-hadoop-virtual-network.md) (Utilizar uma rede virtual com o HDInsight)
* [Use edge nodes in HDInsight](hdinsight-apps-use-edge-node.md#access-an-edge-node) (Utilizar nós de extremidade no HDInsight)
