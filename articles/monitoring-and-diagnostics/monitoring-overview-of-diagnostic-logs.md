---
title: Visão geral dos Logs de Diagnóstico do Azure | Microsoft Docs
description: Saiba quais são os logs de diagnóstico do Azure e como você pode usá-los para compreender os eventos que ocorrem dentro de um recurso do Azure.
author: johnkemnetz
manager: orenr
editor: ''
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: fe8887df-b0e6-46f8-b2c0-11994d28e44f
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2018
ms.author: johnkem; magoedte
ms.openlocfilehash: 00b990181e5bb96f122ff1ae530dd027a772b210
ms.sourcegitcommit: 1362e3d6961bdeaebed7fb342c7b0b34f6f6417a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
---
# <a name="collect-and-consume-log-data-from-your-azure-resources"></a>Coletar e consumir dados de log dos recursos do Azure

## <a name="what-are-azure-resource-diagnostic-logs"></a>O que são os logs de diagnóstico de recursos do Azure

**Os logs de diagnóstico no nível do recurso do Azure** são logs emitidos por um recurso que fornece dados avançados e frequentes sobre a operação do recurso. O conteúdo desses logs varia de acordo com o tipo de recurso. Por exemplo, os contadores de regra do Grupo de Segurança de Rede e as auditorias do Key Vault são duas categorias de logs de recursos.

Os logs de diagnóstico no nível do recurso são diferentes do [Log de Atividades](monitoring-overview-activity-logs.md). O Log de Atividades fornece informações sobre as operações executadas em recursos em sua assinatura usando o Gerenciador de Recursos, por exemplo, criar uma máquina virtual ou excluir um aplicativo lógico. O Log de Atividades é um log no nível da assinatura. Os logs de diagnóstico no nível do recurso fornecem informações sobre as operações executadas dentro do próprio recurso, por exemplo, obtenção de um segredo de um Key Vault.

Os logs de diagnóstico no nível do recurso também diferem dos logs de diagnóstico no nível do sistema operacional convidado. Os logs de diagnóstico do sistema operacional convidado são aqueles coletados por um agente em execução dentro de uma máquina virtual ou outro tipo de recurso com suporte. Os logs de diagnóstico no nível do recurso não exigem um agente e capturam dados específicos ao recurso da própria plataforma do Azure, enquanto os logs de diagnóstico no nível do sistema operacional convidado capturam dados do sistema operacional e de aplicativos em execução em uma máquina virtual.

Nem todos os recursos oferecem suporte ao novo tipo de logs de diagnóstico descritos aqui. Este artigo contém uma seção que lista os tipos de recursos que dão suporte aos novos logs de diagnóstico no nível do recurso.

![Logs de diagnóstico do recurso versus outros tipos de logs ](./media/monitoring-overview-of-diagnostic-logs/Diagnostics_Logs_vs_other_logs_v5.png)

## <a name="what-you-can-do-with-resource-level-diagnostic-logs"></a>O que você pode fazer com os logs de diagnóstico no nível do recurso
Aqui estão algumas coisas que você pode fazer com os logs de diagnóstico de recurso:

![Posicionamento lógico dos Logs de Diagnóstico de recurso](./media/monitoring-overview-of-diagnostic-logs/Diagnostics_Logs_Actions.png)

* Salve-os em uma [**Conta de Armazenamento**](monitoring-archive-diagnostic-logs.md) para auditoria ou inspeção manual. Você pode especificar o tempo de retenção (em dias) usando as **Configurações de Diagnóstico do Recurso**.
* [Transmita-os para os **Hubs de Eventos**](monitoring-stream-diagnostic-logs-to-event-hubs.md) para o consumo por um serviço de terceiros ou uma solução de análises personalizadas, como o PowerBI.
* Analise-os com o [Log Analytics](../log-analytics/log-analytics-azure-storage.md)

Você pode usar uma conta de armazenamento ou um namespace de Hubs de Evento que não esteja na mesma assinatura que os logs emissores. O usuário que define a configuração deve ter o devido acesso RBAC para ambas as assinaturas.

## <a name="resource-diagnostic-settings"></a>Configurações do Diagnóstico do recurso

Os logs de diagnóstico do recurso para os recursos que não são de computação são configurados usando as configurações de diagnóstico do recurso. **Configurações de Diagnóstico do Recurso** para um controle de recursos:

* Para onde os logs de diagnóstico e as métricas do recurso são enviados (Conta de Armazenamento, Hubs de Eventos e/ou Log Analytics).
* Quais categorias de log são enviadas e se os dados de métrica também são enviados.
* Quanto tempo cada categoria de log deve ser mantida em uma conta de armazenamento
    - Uma retenção de zero dias significa que os registros serão mantidos indefinidamente. O valor pode ser qualquer quantidade de dias, entre 1 e 2147483647.
    - Se as políticas de retenção estiverem definidas, mas o armazenamento de logs em uma Conta de Armazenamento estiver desabilitado (por exemplo, se apenas as opções Hubs de Eventos ou Log Analytics forem selecionadas), as políticas de retenção não terão efeito.
    - As políticas de retenção são aplicadas por dia, para que, ao final de um dia (UTC), os logs do dia após a política de retenção sejam excluídos. Por exemplo, se você tiver uma política de retenção de um dia, no início do dia de hoje, os logs de anteontem serão excluídos.

Essas configurações são facilmente definidas por meio das configurações de diagnóstico para um recurso no Portal do Azure, via Azure PowerShell e comandos da CLI ou via [API REST do Azure Monitor](https://msdn.microsoft.com/library/azure/dn931943.aspx).

> [!NOTE]
> Atualmente, não há suporte para o envio da métrica multidimensional por meio das configurações de diagnóstico. As métricas com dimensões são exportadas como métricas dimensionais simples, agregadas nos valores da dimensão.
>
> *Por exemplo*: a métrica “Mensagens de Entrada” em um Hub de Eventos pode ser explorada e mapeada por nível da fila. No entanto, quando exportada por meio das configurações de diagnóstico, a métrica será representada como todas as mensagens de entrada em todas as filas no Hub de Eventos.
>
>

> [!WARNING]
> Os logs de diagnóstico e as métricas da camada do sistema operacional convidado dos recursos de Computação (por exemplo, VMs ou Service Fabric) usam [um mecanismo separado para a configuração e a seleção de saídas](../azure-diagnostics.md).

## <a name="how-to-enable-collection-of-resource-diagnostic-logs"></a>Como habilitar a coleção de logs de diagnóstico do recurso

A coleção de logs de diagnóstico do recurso pode ser habilitada [como parte da criação de um recurso em um modelo do Resource Manager](./monitoring-enable-diagnostic-logs-using-template.md) ou depois de um recurso ser criado por meio da página do recurso no portal. Você também pode habilitar a coleção a qualquer momento usando os comandos do Azure PowerShell ou da CLI, ou usando a API REST do Azure Monitor.

> [!TIP]
> Essas instruções não podem ser aplicadas diretamente em cada recurso. Confira os links do esquema na parte inferior desta página para entender as etapas especiais que podem ser aplicadas em certos tipos de recursos.

### <a name="enable-collection-of-resource-diagnostic-logs-in-the-portal"></a>Como habilitar a coleção de logs de diagnóstico de recurso no Portal

Você poderá habilitar a coleta de logs de diagnóstico de recursos no portal do Azure depois que um recurso tiver sido criado, acessando um recurso específico ou navegando até o Azure Monitor. Para habilitar isso por meio do Azure Monitor:

1. No [portal do Azure](http://portal.azure.com), navegue até o Azure Monitor e clique em **Configurações de Diagnóstico**

    ![Seção de monitoramento do Azure Monitor](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-blade.png)

2. Se desejar filtrar a lista por tipo de recurso ou grupo de recursos, clique no recurso para o qual você deseja definir uma configuração de diagnóstica.

3. Se nenhuma configuração existir no recurso que você selecionou, será solicitada a criação de uma configuração. Clique em “Ativar diagnóstico”.

   ![Adicionar configuração de diagnóstico - nenhuma configuração existente](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-none.png)

   Se houver configurações existentes no recurso, você verá uma lista de configurações já definidas nesse recurso. Clique em "Adicionar configuração de diagnóstico".

   ![Adicionar configuração de diagnóstico - configurações existentes](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-multiple.png)

3. Dê um nome para sua configuração, marque as caixas para cada destino ao qual você gostaria de enviar dados e configure o recurso usado para cada destino. Opcionalmente, defina um número de dias para manter esses logs usando os controles deslizantes **Retenção (dias)** (aplicáveis somente ao destino da conta de armazenamento). Uma retenção de zero dias armazena os logs indefinidamente.

   ![Adicionar configuração de diagnóstico - configurações existentes](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-configure.png)

4. Clique em **Salvar**.

Após alguns instantes, a nova configuração aparece na lista de configurações para esse recurso e os logs de diagnóstico são enviados para os destinos especificados assim que os novos dados de evento são gerados.

### <a name="enable-collection-of-resource-diagnostic-logs-via-powershell"></a>Habilitar a coleção de logs de diagnóstico de recurso via PowerShell

Para habilitar a coleção de logs de diagnóstico de recurso via Azure PowerShell, use os comandos a seguir:

Para habilitar o armazenamento dos logs de diagnóstico em uma conta de armazenamento, use este comando:

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -StorageAccountId [your storage account id] -Enabled $true
```

A ID da conta de armazenamento é a ID de recurso da conta de armazenamento para a qual você deseja enviar os logs.

Para habilitar o streaming dos logs de diagnóstico para um hub de eventos, use este comando:

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -ServiceBusRuleId [your Service Bus rule id] -Enabled $true
```

A ID da regra do barramento de serviço é uma cadeia de caracteres com este formato: `{Service Bus resource ID}/authorizationrules/{key name}`.

Para habilitar o envio dos logs de diagnóstico para um espaço de trabalho do Log Analytics, use este comando:

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -WorkspaceId [resource id of the log analytics workspace] -Enabled $true
```

É possível obter a ID de recurso do seu espaço de trabalho do Log Analytics usando o seguinte comando:

```powershell
(Get-AzureRmOperationalInsightsWorkspace).ResourceId
```

Você pode combinar esses parâmetros para permitir várias opções de saída.

### <a name="enable-collection-of-resource-diagnostic-logs-via-azure-cli-20"></a>Habilitar a coleção de logs de diagnóstico de recursos por meio da CLI 2.0 do Azure

Para habilitar a coleção de logs de diagnóstico de recursos por meio da CLI 2.0 do Azure, use o comando [az monitor diagnostic-settings create](/cli/azure/monitor/diagnostic-settings#az-monitor-diagnostic-settings-create).

Para habilitar o armazenamento de logs de diagnóstico em uma Conta de Armazenamento:

```azurecli
az monitor diagnostic-settings create --name <diagnostic name> \
    --storage-account <name or ID of storage account> \
    --resource <target resource object ID> \
    --resource-group <storage account resource group> \
    --logs '[
    {
        "category": <category name>,
        "enabled": true,
        "retentionPolicy": {
            "days": <# days to retain>,
            "enabled": true
        }
    }]'
```

O argumento `--resource-group` somente será necessário se `--storage-account` não for uma ID de objeto.

Para habilitar o fluxo de logs de diagnóstico para um Hub de Eventos:

```azurecli
az monitor diagnostic-settings create --name <diagnostic name> \
    --event-hub <event hub name> \
    --event-hub-rule <event hub rule ID> \
    --resource <target resource object ID> \
    --logs '[
    {
        "category": <category name>,
        "enabled": true
    }
    ]'
```

A ID da regra é uma cadeia de caracteres com este formato: `{Service Bus resource ID}/authorizationrules/{key name}`.

Para habilitar o envio de logs de diagnóstico para um espaço de trabalho do Log Analytics:

```azurecli
az monitor diagnostic-settings create --name <diagnostic name> \
    --workspace <log analytics name or object ID> \
    --resource <target resource object ID> \
    --resource-group <log analytics workspace resource group> \
    --logs '[
    {
        "category": <category name>,
        "enabled": true
    }
    ]'
```

O argumento `--resource-group` somente será necessário se `--workspace` não for uma ID de objeto

Com qualquer comando, é possível adicionar categorias adicionais ao log de diagnóstico, adicionando dicionários à matriz JSON transmitida como o parâmetro `--logs`. Você pode combinar `--storage-account`, `--event-hub` e `--workspace` para habilitar várias opções de saída.

### <a name="enable-collection-of-resource-diagnostic-logs-via-rest-api"></a>Habilitar a coleção de logs de diagnóstico do recurso via API REST

Para alterar as configurações de diagnóstico usando a API REST do Azure Monitor, confira [este documento](https://msdn.microsoft.com/library/azure/dn931931.aspx).

## <a name="manage-resource-diagnostic-settings-in-the-portal"></a>Gerenciar configurações de diagnóstico de recurso no Portal

Verifique se todos os seus recursos estão definidos com as configurações de diagnóstico. Navegue até **Monitor** no portal e abra **Configurações de diagnóstico**.

![Folha Logs de Diagnóstico no portal](./media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-nav.png)

Você talvez tenha que clicar em "Todos os serviços" para localizar a seção Monitoramento.

Ali, você pode exibir e filtrar todos os recursos que dão suporte a configurações de diagnóstico para ver se eles têm o diagnóstico habilitado. Você também pode fazer uma busca detalhada para ver se várias configurações estão definidas em um recurso e verificar para qual conta de armazenamento, namespace de Hubs de Eventos e/ou espaço de trabalho do Log Analytics os dados estão fluindo.

![Resultados da folha Logs de Diagnóstico no portal](./media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-blade.png)

A adição de uma configuração de diagnóstico mostra a exibição Configurações de Diagnóstico, onde você pode habilitar, desabilitar ou modificar as configurações de diagnóstico para o recurso selecionado.

## <a name="supported-services-categories-and-schemas-for-resource-diagnostic-logs"></a>Serviços, categorias e esquemas com suporte para os logs de diagnóstico de recurso

[Consulte este artigo](monitoring-diagnostic-logs-schema.md) para obter uma lista de serviços com suporte e as categorias de log e os esquemas usados por esses serviços.

## <a name="next-steps"></a>Próximas etapas

* [Transmitir logs de diagnóstico de recurso os **Hubs de Eventos**](monitoring-stream-diagnostic-logs-to-event-hubs.md)
* [Alterar as configurações de diagnóstico do recurso usando a API REST do Azure Monitor](https://msdn.microsoft.com/library/azure/dn931931.aspx)
* [Analisar logs do Armazenamento do Azure com o Log Analytics](../log-analytics/log-analytics-azure-storage.md)
