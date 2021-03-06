---
title: Adicionar novos utilizadores ao Azure Active Directory | Microsoft Docs
description: "Explica como adicionar novos utilizadores ou alterar as informações de utilizador no Azure Active Directory."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: e3673727-6bec-4fdc-87a4-d65b213c4c3c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 02/10/2017
ms.author: curtand
translationtype: Human Translation
ms.sourcegitcommit: 8f171456f74925eba16ebd6f56ced558a11f9d99
ms.openlocfilehash: 6c366a2b7e5017bbe67cf1dbefc0baec6cf1aed3


---
# <a name="add-new-users--or-users-with-microsoft-accounts-to-azure-active-directory"></a>Adicionar novos utilizadores ou utilizadores com contas Microsoft ao Azure Active Directory.
Adicione utilizadores para povoar o diretório. Este artigo explica como adicionar novos utilizadores à sua organização e como adicionar utilizadores com contas Microsoft. Para obter mais informações sobre como adicionar utilizadores a partir de outros diretórios do Azure Active Directory ou como adicionar utilizadores de empresas associadas, consulte [Adicionar utilizadores de outros diretórios ou empresas associadas no Azure Active Directory](active-directory-create-users-external.md). Por predefinição, os utilizadores adicionados não têm permissões de administrador. No entanto, pode atribuir-lhes funções em qualquer altura.

## <a name="add-a-user"></a>Adicionar um utilizador
1. Iniciar sessão no [Portal Clássico do Azure](https://manage.windowsazure.com) com uma conta que seja um administrador global do diretório.
2. Selecione **Active Directory** e, em seguida, selecione o nome do diretório da sua organização.
3. Selecione o separador **Utilizadores** e selecione **Adicionar Utilizador** na barra de comandos.
4. Na página **Forneça mais informações sobre este utilizador**, em **Tipo de utilizador**, selecione:

   * **Novo utilizador na organização** – adiciona uma nova conta de utilizador ao diretório.
   * **Utilizador com uma conta Microsoft existente** – adiciona uma conta de consumidor Microsoft existente ao diretório (por exemplo, uma conta do Outlook)
5. Dependendo do **tipo de utilizador**, introduza um nome de utilizador (para o novo utilizador) ou um endereço de e-mail (para um utilizador com uma conta Microsoft).
6. Na página **Perfil** do utilizador, introduza o nome e o apelido, um nome amigável de utilizador e uma função de utilizador na lista **Funções**. Para obter mais informações sobre as funções de utilizador e administrador, consulte [Atribuir funções de administrador no Azure AD](active-directory-assign-admin-roles.md). Especifique se pretende **Ativar o Multi-Factor Authentication** para o utilizador.
7. Na página **Obter palavra-passe temporária**, selecione **Criar**.

> [!IMPORTANT]
> Se a sua organização utilizar mais de um domínio, deverá ser informado dos seguintes problemas quando adicionar uma conta de utilizador:
>
> * Para adicionar contas de utilizar com o mesmo nome principal de utilizador (UPN) em vários domínios, **comece** por adicionar, por exemplo, geoffgrisso@contoso.onmicrosoft.com, **seguido de**geoffgrisso@contoso.com.
> * **Não** adicione geoffgrisso@contoso.com antes de adicionar geoffgrisso@contoso.onmicrosoft.com. É importante seguir esta ordem uma vez que qualquer anulação poderá ser complicada.
>
>

## <a name="change-user-information"></a>Alterar as informações do utilizador
Pode alterar qualquer atributo do utilizador, exceto o ID de objeto.

1. Abra o diretório.
2. Selecione o separador **Utilizadores** e, em seguida, selecione o nome a apresentar do utilizador que pretende alterar.
3. Termine as alterações e clique em **Guardar**.

Se o utilizador que está a alterar estiver sincronizado com o seu serviço do Active Directory no local, não poderá alterar as informações do utilizador utilizando este procedimento. Para alterar o utilizador, utilize as ferramentas de gestão do Active Directory no local.

## <a name="guest-user-management-and-limitations"></a>Gestão de utilizadores convidados e limitações
As contas de convidados referem-se a utilizadores de outros diretórios que foram convidados para o seu diretório para aceder a documentos do SharePoint, aplicações ou a outros recursos do Azure. Uma conta de convidado no diretório tem o atributo UserType subjacente definido para “Convidado”. Os utilizadores regulares (nomeadamente os membros do diretório) têm o atributo UserType “Membro”.

Os convidados têm um conjunto limitado de direitos no diretório. Estes direitos limitam a capacidade de os convidados detetarem informações sobre outros utilizadores no diretório. No entanto, os utilizadores convidados ainda podem interagir com os utilizadores e grupos associados aos recursos em que estão a trabalhar. Os utilizadores convidados podem:

* Ver outros utilizadores e grupos associados a uma subscrição do Azure à qual foram atribuídos
* Ver os membros de grupos aos quais pertencem
* Procurar outros utilizadores no diretório, caso saibam o endereço de e-mail completo do utilizador
* Ver apenas um conjunto limitado de atributos dos utilizadores que procuram – limitado ao nome a apresentar, endereço de e-mail, nome principal de utilizador (UPN) e fotografia em miniatura
* Obter uma lista de domínios verificados no diretório
* Autorizar aplicações, garantindo-lhes o mesmo acesso que os Membros no diretório

## <a name="set-guest-user-access-policies"></a>Definir políticas de acesso do utilizador convidado
O separador **Configurar** de um diretório inclui opções para controlar o acesso de utilizadores convidados. Estas opções apenas podem ser alteradas no Portal Clássico do Azure, por um administrador global do diretório. Não existe atualmente nenhum PowerShell ou método API.

Para abrir o separador **Configurar** no Portal Clássico do Azure, selecione **Active Directory** e, em seguida, selecione o nome do diretório.

![Separador Configurar no Azure Active Directory][1]

Em seguida, pode editar as opções para controlar o acesso dos utilizadores convidados.

![opções de controlo de acesso dos utilizadores convidados][2]

## <a name="whats-next"></a>Passos seguintes
* [Adicionar utilizadores de outros diretórios ou empresas associadas no Azure Active Directory](active-directory-create-users-external.md)
* [Administrar o Azure AD](active-directory-administer.md)
* [Gerir palavras-passe no Azure AD](active-directory-manage-passwords.md)
* [Gerir grupos no Azure AD](active-directory-manage-groups.md)

<!--Image references-->
[1]: ./media/active-directory-create-users/RBACDirConfigTab.png
[2]: ./media/active-directory-create-users/RBACGuestAccessControls.png



<!--HONumber=Feb17_HO2-->


