---
title: Guia do administrador para o plug-in de SSO do Microsoft Azure Active Directory | Microsoft Docs
description: Saiba como configurar o logon único entre o Microsoft Azure Active Directory e o Jira/Confluence.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 4b663047-7f88-443b-97bd-54224b232815
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2018
ms.author: jeedes
ms.openlocfilehash: d34ff6021816c73fb064a3ce73b7fcf3ae22dbd1
ms.sourcegitcommit: 6fcd9e220b9cd4cb2d4365de0299bf48fbb18c17
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/05/2018
---
# <a name="admin-guide-for-the-azure-active-directory-sso-plug-in"></a>Guia do administrador para o plug-in de SSO do Microsoft Azure Active Directory

## <a name="overview"></a>Visão geral

O plug-in de logon único (SSO) do Azure Active Directory (AD do Azure) permite que os clientes do Microsoft Azure Active Directory usem sua conta corporativa ou de estudante para entrar no Atlassian Jira e produtos com base em Confluence Server. Ele implementa SSO baseado em SAML 2.0.

## <a name="how-it-works"></a>Como ele funciona

Quando os usuários desejam entrar no aplicativo Atlassian Jira ou Confluence, eles veem o botão **Logon com Microsoft Azure AD** na página de entrada. Quando eles o selecionam, precisam entrar usando a página de entrada da organização do Microsoft Azure AD (ou seja, sua conta corporativa ou de estudante).

Depois que os usuários forem autenticados, eles poderão entrar no aplicativo. Se eles já estão autenticados com a ID e a senha de sua conta corporativa ou de estudante, então eles entram diretamente no aplicativo. 

A entrada funciona no Jira e no Confluence. Se os usuários entrarem no aplicativo JIRA e o Confluence também estiver aberto na mesma janela do navegador, eles não precisarão fornecer as credenciais novamente para outro aplicativo. 

Os usuários também podem obter o produto Atlassian em Meus aplicativos com a conta corporativa ou de estudante. Eles devem conseguir entrar sem terem que fornecer credenciais.

> [!NOTE]
> O provisionamento de usuários não é feito por meio do plug-in.

## <a name="audience"></a>Público-alvo

Administradores de Jira e Confluence podem usar o plug-in para habilitar o SSO usando o Microsoft Azure Active Directory.

## <a name="assumptions"></a>Suposições

* Instâncias de Jira e Confluence são habilitadas para HTTPS.
* Usuários já estão criados no Jira ou no Confluence.
* Usuários já têm funções no Jira ou no Confluence.
* Os administradores têm acesso às informações necessárias para configurar o plug-in.
* O Jira e o Confluence também estão disponíveis fora da rede da empresa.
* O plug-in funciona com a versão local do Jira e do Confluence.

## <a name="prerequisites"></a>pré-requisitos

Considere as seguintes informações antes de instalar o plug-in:

* O Jira e o Confluence estão instalados em uma versão do Windows de 64 bits.
* As versões do Jira e do Confluence estão habilitadas para HTTPS.
* O Jira e o Confluence estão disponíveis na Internet.
* Credenciais de administrador estão em vigor para o Jira e o Confluence.
* Credenciais de administrador estão em vigor para o Microsoft Azure Active Directory.
* O WebSudo está desabilitado no Jira e no Confluence.

## <a name="supported-versions-of-jira-and-confluence"></a>Versões do Jira e do Confluence com suporte

O plug-in é compartível com as versões a seguir do Jira e do Confluence:

* Jira Core e Software: 6.0 a 7.2.0
* Jira Service Desk: 3.0 a 3.2
* Confluence: 5.0 a 5.10

## <a name="installation"></a>Instalação

Para instalar o plug-in, siga estas etapas:

1. Entre em sua instância do Jira ou do Confluence como administrador.
    
2. Vá para o console de administração do Jira/Confluence e selecione **Complementos**.
    
3. No Atlassian Market Place, pesquise **Plug-in de SSO do SAML da Microsoft**.
 
   A versão apropriada do plug-in é exibida nos resultados da pesquisa.
 
5. Selecione o plug-in e o Gerenciador de plug-in Universal (UPM) o instalará.
 
Depois que o plug-in for instalado, ele será exibido na seção **Complementos Instalados pelo Usuário** da seção **Gerenciar Complementos**.
    
## <a name="plug-in-configuration"></a>Configuração de plug-in

Antes de começar a usar o plug-in, você deve configurá-lo. Selecione o plug-in, selecione o botão **Configurar** e, em seguida, forneça os detalhes de configuração.

A imagem a seguir mostra a tela de configuração no JIRA e no Confluence:
    
![Tela de configuração de plug-in](./media/ms-confluence-jira-plugin-adminguide/jira.png)

*   **URL de metadados**: a URL para obter metadados de federação do Microsoft Azure AD.
 
*   **Identificadores**: a URL utilizada pelo Microsoft Azure AD para validar a origem da solicitação. Ela mapeia para o elemento **Identificador** no Microsoft Azure AD. O plug-in deriva automaticamente esta URL como https://*<domínio:porta>*/.
 
*   **URL de resposta**: a URL de resposta no seu provedor de identidade (IdP) que inicia a entrada do SAML. Ela mapeia para o elemento **URL de Resposta** no Microsoft Azure AD. O plug-in deriva automaticamente esta URL como https://*<domínio:porta>*/plugins/servlet/saml/auth.
 
*   **URL de logon**: a URL de logon no seu IdP que inicia a entrada SAML. Ela mapeia para o elemento **Logon** no Microsoft Azure AD. O plug-in deriva automaticamente esta URL como https://*<domínio:porta>*/plugins/servlet/saml/auth.
 
*   **ID da Entidade do IdP**: a ID de entidade que o IdP usa. Essa caixa é preenchida quando a URL de metadados é resolvida.
 
*   **URL de Logon**: a URL de entrada do IdP. Essa caixa é preenchida no Microsoft Azure AD quando a URL de metadados é resolvida.
 
*   **URL de Logoff**: a URL de logoff do IdP. Essa caixa é preenchida no Microsoft Azure AD quando a URL de metadados é resolvida.
 
*   **Certificado X.509**: o certificado X.509 do IdP. Essa caixa é preenchida no Microsoft Azure AD quando a URL de metadados é resolvida.
 
*   **Nome do botão de logon**: o nome do botão de entrada que sua organização deseja que os usuários vejam na página de entrada.
 
*   **Locais de ID de usuário do SAML**: o local onde a ID de usuário Jira ou Confluence é esperada na resposta SAML. Ele pode estar em **NameID** ou em um nome de atributo personalizado.
 
*   **Nome do atributo**: nome do atributo em que a ID de usuário é esperada.
 
*   **Habilitar a descoberta de realm inicial**: a seleção a ser feita caso a empresa esteja usando entrada com base nos Serviços de Federação do Active Directory (AD FS).
 
*   **Nome de domínio**: o nome de domínio se a entrada for baseada em AD FS.
 
*   **Habilitar saída única**: a seleção a ser feita caso você deseje sair do Azure Active Directory quando um usuário sair do Jira ou do Confluence.

## <a name="troubleshooting"></a>solução de problemas

* **Você está obtendo vários erros de certificado**: entre no Azure Active Directory e remova os vários certificados que estão disponíveis com relação ao aplicativo. Certifique-se de que apenas um certificado esteja presente.

* **Um certificado está prestes a expirar no Azure Active Directory**: complementos cuidam da sobreposição automática do certificado. Quando um certificado estiver prestes a expirar, um novo certificado deverá ser marcado como ativo e os certificados não utilizados deverão ser excluídos. Quando um usuário tenta entrar no Jira nesse cenário, o plug-in efetua fetch e salva o novo certificado.

* **Você deseja desabilitar o WebSudo (desabilite a sessão de administrador segura)**:
    
  * Para Jira, sessões de administrador seguras (ou seja, confirmação de senha antes de acessar as funções de administração) são habilitadas por padrão. Se você deseja remover esse recurso em sua instância de Jira, especifique a seguinte linha no arquivo jira-config: `ira.websudo.is.disabled = true`
    
  * Para Confluence, siga as etapas no [site de suporte do Confluence](https://confluence.atlassian.com/doc/configuring-secure-administrator-sessions-218269595.html).

* **Campos que devem ser preenchidos pela URL de metadados não estão sendo preenchidos**:
    
  * Verifique se a URL está correta. Verifique se o locatário e a ID do aplicativo estão mapeados corretamente.
    
  * Insira a URL em um navegador e verifique se você está recebendo o XML de metadados de federação.

* **Há um erro de servidor interno**: revise os logs no diretório de logs da instalação. Se você estiver recebendo o erro quando o usuário estiver tentando entrar utilizando o SSO do Microsoft Azure AD, é possível compartilhar os logs com a equipe de suporte.

* **Há um erro de "ID de usuário não encontrado" quando o usuário tenta entrar**: crie a ID de usuário no Jira ou no Confluence.

* **Há um erro de "Aplicativo não encontrado" no Azure Active Directory**: veja se a URL apropriada está mapeada para o aplicativo no Azure Active Directory.

* **Você precisa de suporte**: contate a [Equipe de integração de SSP do Microsoft Azure Active Directory](<mailto:SaaSApplicationIntegrations@service.microsoft.com>). A equipe responde entre 24 e 48 horas dentro do horário comercial.
    
  Também é possível criar um ticket de suporte com a Microsoft por meio do canal do Portal do Azure.