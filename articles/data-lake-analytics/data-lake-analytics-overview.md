---
title: "Descrição geral do Microsoft Azure Data Lake Analytics | Microsoft Docs"
description: "O Data Lake Analytics é um serviço do Azure Big Data que lhe permite utilizar dados para orientar a sua empresa com as informações obtidas a partir dos dados na cloud, independentemente do tamanho ou da localização."
services: data-lake-analytics
documentationcenter: 
author: edmacauley
manager: jhubbard
editor: cgronlun
ms.assetid: 1e1d443a-48a2-47fb-bc00-bf88274222de
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/28/2017
ms.author: edmaca
translationtype: Human Translation
ms.sourcegitcommit: 424d8654a047a28ef6e32b73952cf98d28547f4f
ms.openlocfilehash: 12d6fe834ed2b31a756123351288eec7ba2a72f7
ms.lasthandoff: 03/21/2017


---
# <a name="overview-of-microsoft-azure-data-lake-analytics"></a>Descrição geral do Microsoft Azure Data Lake Analytics
## <a name="what-is-azure-data-lake-analytics"></a>O que é o Azure Data Lake Analytics?
O Azure Data Lake Analytics é um serviço de tarefa de análise a pedido para simplificar a análise de macrodados. Concentre-se na escrita, execução e gestão de tarefas, em vez de na infraestrutura distribuída em funcionamento. Em vez de implementar, configurar e otimizar hardware, escreve consultas para transformar os dados e extrair informações valiosas. O serviço de análise pode processar tarefas de qualquer dimensionamento instantaneamente definindo a quantidade de potência necessária. Apenas paga a tarefa quando estiver a ser executada, tornando-a económica. O serviço de análise suporta o Azure Active Directory permitindo-lhe gerir o acesso e as funções e está integrado no sistema de identidades no local. Também inclui U-SQL, uma linguagem que unifica os benefícios do SQL com o poder expressivo do código de utilizador. O runtime escalável distribuído de U-SQL permite-lhe analisar eficazmente os dados no arquivo e nos SQL Servers no Azure, Base de Dados SQL do Azure e Azure SQL Data Warehouse.

## <a name="key-capabilities"></a>Principais capacidades
* **Dimensionamento dinâmico**
  
    O Data Lake Analytics é criado para dimensionamento e desempenho da cloud.  Aprovisiona dinamicamente os recursos e permite-lhe fazer análises sobre terabytes ou até mesmo exabytes de dados. Quando a tarefa é concluída, reduz os recursos automaticamente e paga apenas a potência de processamento utilizada. À medida que aumenta ou diminui o tamanho dos dados armazenados ou a quantidade de computação utilizada, não tem de reescrever o código. Pode concentrar-se apenas na lógica de negócio e não em como processar e armazenar grandes conjuntos de dados.
* **Desenvolver mais rapidamente, depurar e otimizar de forma mais inteligente com ferramentas familiares**
  
    O Data Lake Analytics tem uma profunda integração com o Visual Studio, pelo que pode utilizar ferramentas familiares para executar, depurar e otimizar o seu código. As visualizações das tarefas U-SQL permitem-lhe ver o modo de execução do código relativamente ao dimensionamento, para que possa identificar facilmente estrangulamentos de desempenho e otimizar os custos.
* **U-SQL: simples e familiar, poderoso e extensível**
  
    O Data Lake Analytics inclui U-SQL, uma linguagem de consulta que expande a natureza familiar, simples e declarativa do SQL Server com o poder expressivo do C#. A linguagem U-SQL foi criada com base no mesmo runtime distribuído que alimenta os sistemas de macrodados na Microsoft. Milhões de programadores SQL e .NET podem agora processar e analisar os seus dados com as capacidades que já têm.
* **Integração total com os seus investimentos de TI**
  
    O Data Lake Analytics pode utilizar os investimentos de TI existentes para identidade, gestão, segurança e armazenamento de dados. Isto simplifica a governação de dados e facilita a expansão das aplicações de dados atuais. O Data Lake Analytics está integrada no Active Directory para gestão de utilizadores e permissões e é fornecida com monitorização e auditoria incorporadas.
* **Económica e acessível**
  
    O Data Lake Analytics é uma solução económica para executar cargas de trabalho de macrodados. Paga por tarefa quando os dados são processados. Não é necessário nenhum hardware, licenças ou contratos de suporte específicos do serviço. O sistema é aumentado ou reduzido verticalmente de forma automática à medida que a tarefa é iniciada e concluída, o que significa que nunca paga mais do que aquilo que precisa.
* **Funciona com todos os Dados do Azure**
  
    O Data Lake Analytics está otimizado para funcionar com o Azure Data Lake - oferecendo o nível mais elevado de desempenho, débito e paralelização das cargas de trabalho de macrodados.  O Data Lake Analytics também pode trabalhar com o Armazenamento de Blobs do Azure e a base de dados SQL do Azure.

## <a name="see-also"></a>Consultar também
* Introdução
  
  * [Introdução ao Data Lake Analytics com o portal do Azure](data-lake-analytics-get-started-portal.md)
  * [Introdução ao Data Lake Analytics com o Azure PowerShell](data-lake-analytics-get-started-powershell.md)
  * [Introdução ao Data Lake Analytics com o SDK .NET do Azure](data-lake-analytics-get-started-net-sdk.md)
  * [Desenvolver scripts U-SQL com as Ferramentas do Data Lake para Visual Studio](data-lake-analytics-data-lake-tools-get-started.md)
  * [Introdução à linguagem U-SQL do Azure Data Lake Analytics](data-lake-analytics-u-sql-get-started.md)
* U-SQL e desenvolvimento
  
  * [Utilizar as funções de janela U-SQL para tarefas do Azure Data Lake Analytics](data-lake-analytics-use-window-functions.md)
  * [Desenvolver operadores U-SQL definidos pelo utilizador para tarefas do Data Lake Analytics](data-lake-analytics-u-sql-develop-user-defined-operators.md)
* Gestão
  
  * [Gerir o Azure Data Lake Analytics com o portal do Azure](data-lake-analytics-manage-use-portal.md)
  * [Gerir o Azure Data Lake Analytics com o Azure PowerShell](data-lake-analytics-manage-use-powershell.md)
  * [Monitorizar e resolver problemas das tarefas de Azure Data Lake Analytics com o portal do Azure](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)
  * [Accessing Diagnostics logs for Azure Data Lake Analytics (Aceder aos registos de diagnóstico do Azure Data Lake Analytics)](data-lake-analytics-diagnostic-logs.md)
* Tutorial ponto a ponto
  
  * [Utilizar tutoriais interativos do Azure Data Lake Analytics](data-lake-analytics-use-interactive-tutorials.md)
  * [Analyze Website logs using Azure Data Lake Analytics (Analisar registos de sites com o Azure Data Lake Analytics)](data-lake-analytics-analyze-weblogs.md)
* Dê-nos a sua opinião
  
  <!-- Fixing broken links for Azure content migration from ACOM to DOCS. I can't find a suitable substitute for what appears to be a link that is no longer available. I am commenting out for now. The author can investigate in the future. Hyperlink text: Comment on our documentation backlog. Referenced file: data-lake-analytics-documentation-backlog.md -->
  * [Submeter um pedido de funcionalidade](http://aka.ms/adlafeedback)
  * [Obter ajuda nos fóruns](http://aka.ms/adlaforums)


