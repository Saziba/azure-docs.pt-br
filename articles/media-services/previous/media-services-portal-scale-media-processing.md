---
title: Dimensionar o processamento de mídia usando o portal do Azure | Microsoft Docs
description: Este tutorial orienta você pelas etapas do dimensionamento do processamento de mídia usando o portal do Azure.
services: media-services
documentationcenter: ''
author: Juliako
manager: cfowler
editor: ''
ms.assetid: e500f733-68aa-450c-b212-cf717c0d15da
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/04/2017
ms.author: juliako
ms.openlocfilehash: 51973916c97282ac93032ab833402d9d1356647e
ms.sourcegitcommit: e221d1a2e0fb245610a6dd886e7e74c362f06467
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/07/2018
---
# <a name="change-the-reserved-unit-type"></a>Alterar o tipo de unidade reservada
> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-encoding-units.md)
> * [Portal](media-services-portal-scale-media-processing.md)
> * [REST](https://docs.microsoft.com/rest/api/media/operations/encodingreservedunittype)
> * [Java](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [PHP](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

> [!NOTE]
> Para obter a versão mais recente do SDK do Java e começar a desenvolver com Java, confira [Introdução ao SDK de cliente Java para Serviços de Mídia](https://docs.microsoft.com/azure/media-services/media-services-java-how-to-use). <br/>
> Para baixar o SDK mais recente do PHP para os Serviços de Mídia, procure a versão 0.5.7 do pacote do Microsoft/WindowAzure no [Repositório do Packagist](https://packagist.org/packages/microsoft/windowsazure#v0.5.7).  

## <a name="overview"></a>Visão geral

Uma conta dos Serviços de Mídia está associada a um Tipo de Unidade Reservada que determina a velocidade com que as suas tarefas de processamento de mídia são processadas. Você pode escolher entre os seguintes tipos de unidade reservada: **S1**, **S2** ou **S3**. Por exemplo, o mesmo trabalho de codificação é executado mais rapidamente quando você usa o tipo de unidade reservada **S2** em comparação ao tipo **S1**.

Além de especificar o tipo de unidade reservada, você pode especificar o provisionamento de sua conta com as **URs** (Unidades Reservadas). O número de URs provisionadas determina o número de tarefas de mídia que podem ser processadas simultaneamente em determinada conta.

>[!NOTE]
>As URs trabalham para paralelizar todo o processamento de mídia, incluindo os trabalhos de indexação, usando o Azure Media Indexer. No entanto, ao contrário da codificação, a indexação de trabalhos não será processada mais rapidamente com unidades reservadas mais rápidas.

> [!IMPORTANT]
> Lembre-se de examinar o tópico [Visão geral](media-services-scale-media-processing-overview.md) para obter mais informações sobre o tópico de dimensionamento de processamento de mídia.
> 
> 

## <a name="scale-media-processing"></a>Processamento de mídia de escala
Para alterar o tipo de unidade reservada e o número de unidades reservadas, faça o seguinte:

1. No [Portal do Azure](https://portal.azure.com/), selecione sua conta dos Serviços de Mídia do Azure.
2. Na janela **Configurações**, selecione **Unidades reservadas de mídia**.
   
    Para alterar o número de unidades reservadas para o tipo de unidade reservada selecionado, use o controle deslizante **Unidades Reservadas de Mídia** no canto superior da tela.
   
    Para alterar o **TIPO DE UNIDADE RESERVADA**, clique na barra **Velocidade das unidades reservadas de processamento**. Em seguida, selecione o tipo de preço de que precisa: S1, S2 ou S3.
   
3. Pressione o botão SALVAR para salvar as alterações.
   
    As novas unidades reservadas são alocadas quando você pressiona SALVAR.

## <a name="next-steps"></a>Próximas etapas
Examine os roteiros de aprendizagem dos Serviços de Mídia.

[!INCLUDE [media-services-learning-paths-include](../../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../../includes/media-services-user-voice-include.md)]

