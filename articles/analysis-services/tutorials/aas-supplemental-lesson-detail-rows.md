---
title: 'Lição suplementar de tutorial do Azure Analysis Services: linhas de detalhes | Microsoft Docs'
description: Descreve como criar uma expressão de linhas de detalhes no tutorial do Azure Analysis Services.
author: minewiskan
manager: kfile
ms.service: analysis-services
ms.topic: conceptual
ms.date: 04/12/2018
ms.author: owend
ms.reviewer: minewiskan
ms.openlocfilehash: 02e9edd966e64c0bfa32e2b80f4c26f797e58582
ms.sourcegitcommit: 9cdd83256b82e664bd36991d78f87ea1e56827cd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="supplemental-lesson---detail-rows"></a>Lição suplementar – Linhas de Detalhes

Nesta lição suplementar, você pode usar o Editor do DAX para definir uma expressão de linhas de detalhes personalizada. Uma expressão de linhas de detalhes é uma propriedade em uma medida, fornecendo aos usuários finais mais informações sobre os resultados agregados de uma medida. 
  
Tempo estimado para conclusão desta lição: **10 minutos**  
  
## <a name="prerequisites"></a>pré-requisitos  
Esta lição suplementar faz parte de um tutorial de modelagem tabular. Antes de executar as tarefas desta lição suplementar, você deve ter concluído todas as lições anteriores ou ter um projeto de modelo de amostra de Vendas pela Internet da Adventure Works concluído.  
  
## <a name="whats-the-issue"></a>Qual é o problema?
Veremos os detalhes da medida InternetTotalSales, antes de adicionar uma Expressão das Linhas de Detalhes.

1.  No SSDT, clique no menu **Modelo** > **Analisar no Excel** para abrir o Excel e criar uma tabela dinâmica em branco.
  
2.  Em **Campos de Tabela Dinâmica**, adicione a medida **InternetTotalSales** da tabela FactInternetSales a **Valores**, **CalendarYear** da tabela DimDate a **Colunas** e **EnglishCountryRegionName** a **Linhas**. A tabela Dinâmica agora fornece um resultado agregado da medida InternetTotalSales por regiões e ano. 

    ![aas-lesson-detail-rows-pivottable](../tutorials/media/aas-lesson-detail-rows-pivottable.png)

3. Na tabela dinâmica, clique duas vezes em um valor agregado para um ano e um nome de região. O valor para a Austrália e o ano de 2014. Uma nova planilha abre os dados contidos, mas não os dados úteis.

    ![aas-lesson-detail-rows-pivottable](../tutorials/media/aas-lesson-detail-rows-sheet.png)
  
O objetivo aqui é uma tabela contendo colunas e linhas de dados que contribuem para o resultado agregado da medida InternetTotalSales. Para fazer isso, adicione uma Expressão das Linhas de Detalhes como uma propriedade da medida.

## <a name="add-a-detail-rows-expression"></a>Adicionar uma expressão de linhas de detalhes

#### <a name="to-create-a-detail-rows-expression"></a>Para criar uma expressão de linhas de detalhes 
  
1. Na grade de medida da tabela FactInternetSales, clique na medida **InternetTotalSales**. 

2. Em **Propriedades** > **Expressão de Linhas de Detalhes**, clique no botão do editor para abrir o Editor do DAX.

    ![aas-lesson-detail-rows-ellipse](../tutorials/media/aas-lesson-detail-rows-ellipse.png)

3. No Editor do DAX, digite a expressão a seguir:

    ```
    SELECTCOLUMNS(
    FactInternetSales,
    "Sales Order Number", FactInternetSales[SalesOrderNumber],
    "Customer First Name", RELATED(DimCustomer[FirstName]),
    "Customer Last Name", RELATED(DimCustomer[LastName]),
    "City", RELATED(DimGeography[City]),
    "Order Date", FactInternetSales[OrderDate],
    "Internet Total Sales", [InternetTotalSales]
    )

    ```

    Essa expressão especifica nomes de colunas, sendo que os resultados de medidas da tabela FactInternetSales e tabelas relacionadas são retornados quando um usuário clica duas vezes em um resultado agregado em uma tabela dinâmica ou relatório.

4. No Excel, exclua a planilha criada na Etapa 3, clique duas vezes um valor agregado. Desta vez, com uma propriedade de expressão de linhas de detalhes definida para a medida, uma nova planilha será aberta contendo dados muito mais úteis.

    ![aas-lesson-detail-rows-detailsheet](../tutorials/media/aas-lesson-detail-rows-detailsheet.png)

5. Reimplante o modelo.

  
## <a name="see-also"></a>Consulte também  

[Função SELECTCOLUMNS (DAX)](https://msdn.microsoft.com/library/mt761759.aspx)   
[Lição suplementar - Segurança dinâmica](../tutorials/aas-supplemental-lesson-dynamic-security.md)   
[Lição suplementar - hierarquias desbalanceadas](../tutorials/aas-supplemental-lesson-ragged-hierarchies.md)   
 