---
title: Entender cotas e limitação do Hub IoT do Azure | Microsoft Docs
description: Guia do desenvolvedor ‑ Descrição das cotas que se aplicam ao Hub IoT e o comportamento de limitação esperado.
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: ''
ms.assetid: 425e1b08-8789-4377-85f7-c13131fae4ce
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/01/2018
ms.author: dobett
ms.openlocfilehash: ef86af61284bb208cc8c469e3fe75bd4f4bdc5bf
ms.sourcegitcommit: 20d103fb8658b29b48115782fe01f76239b240aa
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/03/2018
---
# <a name="reference---iot-hub-quotas-and-throttling"></a>Referência - Cotas e limitação do Hub IoT

## <a name="quotas-and-throttling"></a>Cotas e limitação
Cada assinatura do Azure pode ter no máximo 10 hubs IoT e pelo menos 1 hub Gratuito.

Cada Hub IoT é provisionado com um determinado número de unidades em uma camada específica. Para saber mais, confira [Preços do Hub IoT do Azure][lnk-pricing]. A camada e o número de unidades determinam a cota diária máxima de mensagens que você pode enviar.

A camada também determina os limites de limitação que o Hub IoT aplicam em todas as operações.

## <a name="operation-throttles"></a>Restrições de operação
As restrições de operação são limites de taxa aplicados em intervalos de minutos, e têm como objetivo evitar o abuso. O Hub IoT tenta evitar o retorno de erros sempre que possível, mas começará a retornar exceções se a restrição for violada por muito tempo.

A qualquer momento, você pode aumentar as cotas ou restrições aumentando o número de unidades provisionadas em um Hub IoT.

A tabela a seguir mostra as limitações impostas. Os valores referem-se a um hub individual.

| Restrição | Gratuito, B1 e S1 | B2 e S2 | B3 e S3 | 
| -------- | ------- | ------- | ------- |
| Operações de registro de identidade (criar, recuperar, listar, atualizar, excluir) | 1,67/s/unidade (100/min/unidade) | 1,67/s/unidade (100/min/unidade) | 83,33/s/unidade (5000/min/unidade) |
| Conexões do dispositivo | Máximo de 100/s ou 12/s/unidade <br/> Por exemplo, duas unidades de S1 são 2\*12 = 24/s, mas você tem pelo menos 100/s em suas unidades. Com nove unidades S1 você tem 108/s (9\*12) em suas unidades. | 120/s/unidade | 6000/s/unidade |
| Envios do dispositivo para a nuvem | Máximo de 100/s ou 12/s/unidade <br/> Por exemplo, duas unidades de S1 são 2\*12 = 24/s, mas você tem pelo menos 100/s em suas unidades. Com nove unidades S1 você tem 108/s (9\*12) em suas unidades. | 120/s/unidade | 6000/s/unidade |
| Envios de nuvem para dispositivo<sup>1</sup> | 1,67/s/unidade (100/min/unidade) | 1,67/s/unidade (100/min/unidade) | 83,33/s/unidade (5000/min/unidade) |
| Recebimentos de nuvem para dispositivo<sup>1</sup> <br/> (somente quando o dispositivo usar HTTPS)| 16,67/s/unidade (1000/min/unidade) | 16,67/s/unidade (1000/min/unidade) | 833,33/s/unidade (50000/min/unidade) |
| Upload de arquivos | 1,67 notificações de carregamento de arquivo/s/unidade (100/min/unidade) | 1,67 notificações de carregamento de arquivo/s/unidade (100/min/unidade) | 83,33 notificações de carregamento de arquivo/s/unidade (5000/min/unidade) |
| Métodos diretos<sup>1</sup> | 160KB/seg/unidade<sup>2</sup> | 480KB/seg/unidade<sup>2</sup> | 24MB/seg/unidade<sup>2</sup> | 
| Leituras de dispositivo gêmeo<sup>1</sup> | 10/s | Máximo de 10/s ou 1/s/unidade | 50/s/unidade |
| Atualizações de dispositivo gêmeo<sup>1</sup> | 10/s | Máximo de 10/s ou 1/s/unidade | 50/s/unidade |
| Operações de trabalhos<sup>1</sup> <br/> (criar, atualizar, listar, excluir) | 1,67/s/unidade (100/min/unidade) | 1,67/s/unidade (100/min/unidade) | 83,33/s/unidade (5000/min/unidade) |
| Taxa de transferência de operação de trabalhos por dispositivo<sup>1</sup> | 10/s | Máximo de 10/s ou 1/s/unidade | 50/s/unidade |

<sup>1</sup>Esse recurso não está disponível na camada básica do Hub IoT. Para obter mais informações, consulte [Como escolher o Hub IoT correto](iot-hub-scaling.md). <br/><sup>2</sup>O tamanho do medidor de limitação é 8 KB.

As *conexões de dispositivo* controla a taxa em que novas conexões de dispositivo podem ser estabelecidas com um Hub IoT. A restrição de *conexões de dispositivo* não controla o número máximo de dispositivos conectados simultaneamente. A restrição depende do número de unidades provisionadas para o hub IoT.

Por exemplo, se você comprar uma única unidade S1, obterá uma restrição de 100 conexões por segundo. Portanto, serão necessários pelo menos 1000 segundos (aproximadamente 16 minutos) para conectar 100.000 dispositivos. No entanto, você pode conectar ao mesmo tempo todos os seus dispositivos registrados no registro de identidade.

Para uma discussão aprofundada do comportamento de limitação do Hub IoT, veja a postagem do blog [A limitação do Hub IoT e você][lnk-throttle-blog].

> [!IMPORTANT]
> As operações de registro de identidade são destinadas ao uso no tempo de execução em cenários de provisionamento e gerenciamento de dispositivos. Há suporte para leitura ou atualização de grandes números de identidades de dispositivo por meio de [trabalhos de importação e exportação][lnk-importexport].
> 
> 

## <a name="other-limits"></a>Outros limites

IoT Hub impõe outros limites operacionais:

| Operação | Limite |
| --------- | ----- |
| URIs de upload de arquivos | 10000 URIs de SAS podem estar fora de uma conta de armazenamento ao mesmo tempo. <br/> 10 URIs de SAS/dispositivo podem estar fora ao mesmo tempo. |
| Trabalhos<sup>1</sup> | O histórico do trabalho é retido por até 30 dias <br/> O máximo de trabalhos simultâneos é 1 (para Gratuito) e S1, 5 (para S2), 10 (para S3). |
| Pontos de extremidade adicionais | Hubs SKU pagos podem ter 10 pontos de extremidade adicionais. Hubs SKU gratuitos podem ter um ponto de extremidade adicional. |
| Regras de roteamento de mensagem | Hubs SKU pagos podem ter 100 regras de roteamento. Hubs SKU gratuitos podem ter cinco regras de roteamento. |
| Mensagens do dispositivo para a nuvem | Tamanho máximo da mensagem 256 KB |
| Mensagens de nuvem para dispositivo<sup>1</sup> | Tamanho máximo da mensagem 64 KB. O máximo de mensagens pendentes para entrega é 50. |
| Método direto<sup>1</sup> | O tamanho de payload do método direto máximo é 128 KB. |

<sup>1</sup>Esse recurso não está disponível na camada básica do Hub IoT. Para obter mais informações, consulte [Como escolher o Hub IoT correto](iot-hub-scaling.md).

> [!NOTE]
> Atualmente, o número máximo de dispositivos que você pode conectar a um único hub IoT é de 500.000. Se você quiser aumentar esse limite, entre em contato com o [Suporte da Microsoft](https://azure.microsoft.com/support/options/).

## <a name="latency"></a>Latency
O Hub IoT busca oferecer baixa latência para todas as operações. No entanto, devido a condições da rede e outros fatores imprevisíveis ele não garante uma latência máxima. Ao projetar sua solução, você deve:

* Evitar fazer suposições sobre a latência máxima de qualquer operação de IoT Hub.
* Provisionar o hub IoT na região do Azure mais próxima de seus dispositivos.
* Considere usar o Azure IoT Edge para executar operações sensíveis à latência no dispositivo ou no gateway perto do dispositivo.

Várias unidades de Hub IoT afetam limitação, conforme descrito anteriormente, mas não oferecem nenhum benefício de latência nem garantia adicional.
No caso de aumentos inesperados na latência da operação, entre em contato com o [Suporte da Microsoft](https://azure.microsoft.com/support/options/).

## <a name="next-steps"></a>Próximas etapas
Outros tópicos de referência neste Guia do desenvolvedor do Hub IoT incluem:

* [Pontos de extremidade do Hub IoT][lnk-devguide-endpoints]
* [Linguagem de consulta do Hub IoT para dispositivos gêmeos, trabalhos e roteamento de mensagens][lnk-devguide-query]
* [Suporte ao MQTT do Hub IoT][lnk-devguide-mqtt]

[lnk-pricing]: https://azure.microsoft.com/pricing/details/iot-hub
[lnk-throttle-blog]: https://azure.microsoft.com/blog/iot-hub-throttling-and-you/
[lnk-importexport]: iot-hub-devguide-identity-registry.md#import-and-export-device-identities

[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
[lnk-devguide-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
