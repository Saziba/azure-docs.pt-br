---
title: Entrega e repetição da Grade de Eventos do Azure
description: Descreve como a Grade de Eventos do Azure entrega eventos e como ela trata mensagens não entregues.
services: event-grid
author: tfitzmac
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 04/17/2018
ms.author: tomfitz
ms.openlocfilehash: 017cb5850788bd230c4a4ba256997f2776c07bec
ms.sourcegitcommit: 59914a06e1f337399e4db3c6f3bc15c573079832
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/19/2018
---
# <a name="event-grid-message-delivery-and-retry"></a>Entrega e repetição de mensagens da Grade de Eventos 

Este artigo descreve como a Grade de Eventos do Azure trata os eventos quando a entrega não é confirmada.

A entrega proporcionada pela Grade de Eventos tem um tempo de duração. Cada mensagem é entregue pelo menos uma vez para cada assinatura. Os eventos são imediatamente enviados ao webhook registrado de cada assinatura. Se um webhook não confirmar o recebimento de um evento em até 60 segundos a contar da primeira tentativa de entrega, a Grade de Eventos repete a entrega do evento. 

Atualmente, a Grade de Eventos envia cada evento individualmente aos assinantes. O assinante recebe uma matriz com um único evento.

## <a name="message-delivery-status"></a>Status de entrega da mensagem

A Grade de Eventos usa códigos de resposta HTTP para confirmar o recebimento de eventos. 

### <a name="success-codes"></a>Códigos de êxito

Os códigos de resposta HTTP a seguir indicam que um evento foi entregue com êxito ao webhook. A Grade de Eventos considera entrega concluída.

- 200 OK
- 202 Aceito

### <a name="failure-codes"></a>Códigos de falha

Os códigos de resposta HTTP a seguir indicam que houve falha na tentativa de entrega do evento. A Grade de Eventos tenta enviar o evento novamente. 

- 400 Solicitação Inválida
- 401 Não Autorizado
- 404 Não Encontrado
- 408 Tempo limite da solicitação
- 414 URI muito longo
- 500 Erro Interno do Servidor
- 503 Serviço Indisponível
- 504 Tempo Limite do Gateway

Qualquer outro código de resposta ou à falta de uma resposta indica uma falha. A Grade de Eventos repete a entrega. 

## <a name="retry-intervals"></a>Intervalos de repetição

A Grade de Eventos usa uma política de repetição de retirada exponencial para a entrega de eventos. Se o seu webhook não responder ou retornar um código de falha, a Grade de Eventos repetirá a entrega nos seguintes intervalos:

1. 10 segundos
2. 30 segundos
3. 1 minuto
4. 5 minutos
5. 10 minutos
6. 30 minutos
7. 1 hora

A Grade de Eventos adiciona uma pequena aleatoriedade a todos os intervalos de repetição. Após uma hora, a entrega de eventos é repetida a cada uma hora.

## <a name="retry-duration"></a>Duração da repetição

A Grade de Eventos do Azure expira todos os eventos que não são entregues dentro de 24 horas.

## <a name="next-steps"></a>Próximas etapas

* Para exibir o status de entregas de evento, consulte [Entrega de mensagens da Grade de Eventos do Monitor](monitor-event-delivery.md).
* Para ver uma introdução à Grade de Eventos, confira [About Event Grid](overview.md) (Sobre a Grade de Eventos).
* Para começar a usar rapidamente a Grade de Eventos, confira [Create and route custom events with Azure Event Grid](custom-event-quickstart.md) (Criar e rotear eventos personalizados com a Grade de Eventos do Azure).