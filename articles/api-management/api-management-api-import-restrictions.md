---
title: Restrições e problemas conhecidos na importação de API do Gerenciamento de API do Azure | Microsoft Docs
description: Detalhes de problemas conhecidos e restrições na importação para o Gerenciamento de API do Azure usando os formatos Open API, WSDL ou WADL.
services: api-management
documentationcenter: ''
author: vladvino
manager: vlvinogr
editor: ''
ms.assetid: 7a5a63f0-3e72-49d3-a28c-1bb23ab495e2
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/29/2017
ms.author: apipm
ms.openlocfilehash: b33c95af94c436b1069658963692242d0f905554
ms.sourcegitcommit: 9cdd83256b82e664bd36991d78f87ea1e56827cd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="api-import-restrictions-and-known-issues"></a>Restrições de importação de API e problemas conhecidos
## <a name="about-this-list"></a>Sobre esta lista
Ao importar uma API, você pode se deparar com algumas restrições ou identificar problemas que precisam ser corrigidos antes de poder importar com êxito. Este artigo documenta essas informações, organizadas pelo formato de importação da API.

## <a name="open-api"> </a>Open API/Swagger
Caso esteja recebendo erros ao importar seu documento da Open API, verifique se você o validou usando o designer no portal do Azure (Design – Front-End – Editor de Especificação da Open API) ou com uma ferramenta de terceiros, como o <a href="http://www.swagger.io">Editor do Swagger</a>.

* Apenas o formato JSON para OpenAPI tem suporte.
* Os esquemas referenciados usando as propriedades **$ref** não podem conter outras propriedades **$ref**.
* Ponteiros **$ref** não podem referenciar a arquivos externos.
* **x-ms-paths** e **x-servers** são as únicas extensões com suporte.
* As extensões personalizadas são ignoradas na importação e não são salvas ou preservadas para exportação.

> [!IMPORTANT]
> Consulte este [documento](https://blogs.msdn.microsoft.com/apimanagement/2018/03/28/important-changes-to-openapi-import-and-export/) para obter dicas e informações importantes relacionadas à importação do OpenAPI.

## <a name="wsdl"> </a>WSDL
Arquivos WSDL são usados para gerar as APIs de passagem SOAP ou servir como o back-end de uma API de SOAP para REST.
* **Associações SOAP** - Apenas as associações SOAP de estilo "documento" e codificação "literal" têm suporte. Não há suporte para estilo "rpc" ou SOAP-Encoding.
* **WSDL:Import** - Não há suporte para esse atributo. Os clientes devem mesclar as importações em um documento.
* **Mensagens com várias partes** - Não há suporte para esses tipos de mensagens.
* **WCF wsHttpBinding** - Serviços SOAP criados com Windows Communication Foundation devem usar basicHttpBinding - não há suporte para wsHttpBinding.
* **MTOM** - Serviços usando MTOM <em>podem</em> funcionar. No momento, não oferecemos suporte oficial.
* **Recursão** - Tipos que são definidos recursivamente (por exemplo, referem-se a uma matriz deles) não têm suporte pelo APIM.

## <a name="wadl"> </a>WADL
Atualmente, não há problemas de importação de WADL conhecidos.
