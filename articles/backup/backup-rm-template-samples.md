---
title: Modelos do Azure Resource Manager para o Backup do Azure | Microsoft Docs
description: Amostras do PowerShell do Backup do Azure
services: backup
documentationcenter: ''
author: markgalioto
manager: carmonm
editor: ''
tags: ''
ms.assetid: ''
ms.service: backup
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 04/18/2018
ms.author: markgal
ms.custom: mvc
ms.openlocfilehash: b8502e4e3934b36fb4c8ccac00f4fa14565780d9
ms.sourcegitcommit: fa493b66552af11260db48d89e3ddfcdcb5e3152
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2018
---
# <a name="azure-resource-manager-templates-for-azure-backup"></a>Modelos do Azure Resource Manager para o Backup do Azure

A tabela a seguir contém links para modelos do Azure Resource Manager para uso nos cofres dos Serviços de Recuperação e nos recursos do Backup do Azure.

|   |   |
|---|---|
|**Cofre dos Serviços de Recuperação** | |
| [Criar um cofre dos Serviços de Recuperação](https://github.com/Azure/azure-quickstart-templates/tree/master/101-recovery-services-vault-create)| Crie um cofre dos Serviços de Recuperação. O cofre pode ser usado no Backup do Azure e no Azure Site Recovery. |
|**Backup de máquinas virtuais**| |
| [Fazer back de VMs do Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/101-recovery-services-backup-vms) | Use o cofre dos Serviços de Recuperação e a política de backup existentes para fazer o backup de máquinas virtuais do Gerenciador de Recursos no mesmo grupo de recursos.|
| [Fazer backup de VMs IaaS no cofre dos Serviços de Recuperação](https://github.com/Azure/azure-quickstart-templates/tree/master/201-recovery-services-backup-classic-resource-manager-vms) | Modelo de backup clássico e máquinas virtuais do Gerenciador de Recursos. |
| [Criar política de backup semanal para VMs IaaS](https://github.com/Azure/azure-quickstart-templates/tree/master/101-recovery-services-weekly-backup-policy-create) | O modelo cria um cofre dos Serviços de Recuperação e uma política de backup semanal que são usados para fazer backup de máquinas virtuais do Gerenciador de Recursos e clássicas.|
| [Criar política de backup diário para VMs IaaS](https://github.com/Azure/azure-quickstart-templates/tree/master/101-recovery-services-daily-backup-policy-create) | O modelo cria um cofre dos Serviços de Recuperação e uma política de backup diário que são usados para fazer backup de máquinas virtuais do Gerenciador de Recursos e clássicas.|
| [Implantar VM do Windows Server com backup habilitado](https://github.com/Azure/azure-quickstart-templates/tree/master/101-recovery-services-create-vm-and-configure-backup) | O modelo cria uma VM do Windows Server e um cofre dos Serviços de Recuperação com a política de backup padrão habilitada.|
|**Monitorar trabalhos de backup** |  |
| [Usar o OMS Log Analytics para monitorar o Backup do Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/101-backup-oms-monitoring) | O modelo implanta o Monitoramento do OMS para o Backup do Azure, que permite monitorar o backup e restaurar trabalhos, fazer backup de alertas e do armazenamento em nuvem usado em seus cofres dos Serviços de Recuperação.|  
|   |   |

