---
title: Elemento de interface do usuário do Azure MultiStorageAccountCombo | Microsoft Docs
description: Descreve o elemento de interface do usuário Microsoft.Storage.MultiStorageAccountCombo para o Portal do Azure.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: reference
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/12/2017
ms.author: tomfitz
ms.openlocfilehash: c395c076a4910e124c1b93ebc61b5e491b2b53ff
ms.sourcegitcommit: 20d103fb8658b29b48115782fe01f76239b240aa
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/03/2018
---
# <a name="microsoftstoragemultistorageaccountcombo-ui-element"></a>Elemento de interface do usuário Microsoft.Storage.MultiStorageAccountCombo
Um grupo de controles para criar várias contas de armazenamento com nomes que começam com um prefixo comum.

## <a name="ui-sample"></a>Exemplo de interface do usuário
![Microsoft.Storage.MultiStorageAccountCombo](./media/managed-application-elements/microsoft.storage.multistorageaccountcombo.png)

## <a name="schema"></a>Esquema
```json
{
  "name": "element1",
  "type": "Microsoft.Storage.MultiStorageAccountCombo",
  "label": {
    "prefix": "Storage account prefix",
    "type": "Storage account type"
  },
  "toolTip": {
    "prefix": "",
    "type": ""
  },
  "defaultValue": {
    "prefix": "sa",
    "type": "Premium_LRS"
  },
  "constraints": {
    "allowedTypes": [],
    "excludedTypes": []
  },
  "count": 2,
  "visible": true
}
```

## <a name="remarks"></a>Comentários
- O valor de `defaultValue.prefix` é concatenado com um ou mais números inteiros para gerar a sequência de nomes de conta de armazenamento. Por exemplo, se `defaultValue.prefix` é **foobar** e `count` é **2**, os nomes de conta de armazenamento **foobar1** e **foobar2** são gerados. Os nomes de conta de armazenamento gerados são validados por exclusividade automaticamente.
- Os nomes de conta de armazenamento são gerados lexicograficamente com base em `count`. Por exemplo, se `count` for 10, os nomes de conta de armazenamento terminarão com números inteiros de 2 dígitos (01, 02, 03, etc.).
- O valor padrão de `defaultValue.prefix` é **null**e `defaultValue.type` é **Premium_LRS**.
- Os tipos não especificados em `constraints.allowedTypes` ficam ocultos e os tipos não especificados em `constraints.excludedTypes` são mostrados.
`constraints.allowedTypes` e `constraints.excludedTypes` são opcionais, mas não podem ser usados simultaneamente.
- Além de gerar nomes de conta de armazenamento, `count` é usado para definir o multiplicador apropriado para o elemento. Ele dá suporte a um valor estático, como **2**, ou a um valor dinâmico de outro elemento, como `[steps('step1').storageAccountCount]`. O valor padrão é **1**.

## <a name="sample-output"></a>Saída de exemplo
```json
{
  "prefix": "sa",
  "count": 2,
  "resourceGroup": "rg01",
  "type": "Premium_LRS"
}
```

## <a name="next-steps"></a>Próximas etapas
* Para obter uma introdução à criação de definições de interface do usuário, consulte [Introdução ao CreateUiDefinition](create-uidefinition-overview.md).
* Para obter uma descrição das propriedades comuns em elementos de interface do usuário, consulte [Elementos de CreateUiDefinition](create-uidefinition-elements.md).
