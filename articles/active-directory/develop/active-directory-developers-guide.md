---
title: Azure Active Directory para desenvolvedores | Microsoft Docs
description: Este artigo fornece uma visão geral sobre como conectar-se às contas corporativa e de estudante da Microsoft usando o Azure Active Directory.
services: active-directory
author: jmprieur
manager: mtillman
editor: ''
ms.assetid: 5c872c89-ef04-4f4c-98de-bc0c7460c7c2
ms.service: active-directory
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/24/2018
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: 02e182a090538588600f95c9be3fd57fc18ba532
ms.sourcegitcommit: e2adef58c03b0a780173df2d988907b5cb809c82
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/28/2018
---
# <a name="azure-active-directory-for-developers"></a>Azure Active Directory para desenvolvedores

O Azure Active Directory (Azure AD) é um serviço de identidade de nuvem que permite aos desenvolvedores criar aplicativos que conectam com segurança qualquer usuário com uma conta corporativa ou de estudante da Microsoft. O Azure Active Directory oferece tanto suporte a desenvolvedores que criam aplicativos de linha de negócios (LOB) com locatário único quanto a desenvolvedores que buscam desenvolver aplicativos de multilocação. Além da conexão básica, o Azure Active Directory também permite que aplicativos chamem as APIs Microsoft como [Microsoft Graph](https://developer.microsoft.com/en-us/graph/docs/concepts/overview) e as APIs personalizadas que são criadas na plataforma do Azure Active Directory.  A documentação mostra como adicionar suporte ao Azure Active Directory para o seu aplicativo usando protocolos padrão como OAuth2.0 e OpenID Connect.

> [!NOTE]
> A maioria do conteúdo nessa página se concentra no ponto de extremidade do Azure Active Directory v1, que oferece suporte somente a contas corporativas ou de estudante da Microsoft. Se deseja entrar em contas da Microsoft do tipo consumidor ou pessoal, consulte mais informações sobre o [ponto de extremidade do Azure Active Directory v2.0](active-directory-appmodel-v2-overview.md). O ponto de extremidade do Azure Active Directory v2.0 oferece uma experiência de desenvolvedor unificada para aplicativos que desejam conectar os usuários com contas do Azure Active Directory (corporativa e de estudante) e contas pessoais da Microsoft.

| | |
| --- | --- |
|[Noções básicas de autenticação](active-directory-authentication-scenarios.md) | Uma introdução à autenticação com o Azure AD. |
|[Tipos de aplicativos](active-directory-authentication-scenarios.md#application-types-and-scenarios) | Uma visão geral dos cenários de autenticação com suporte no Azure AD. |                                

## <a name="get-started"></a>Introdução
As configurações guiadas abaixo orientam você durante a criação de um aplicativo em sua plataforma preferida usando o SDK do Azure Active Directory Library (ADAL). Se estiver procurando informações sobre como usar a Biblioteca de Autenticação da Microsoft (MSAL), consulte nossa documentação sobre o [ponto de extremidade do Azure Active Directory v2.0](active-directory-appmodel-v2-overview.md).

|  |  |  |  |
| --- | --- | --- | --- |
| <center>![Aplicativos da área de trabalho e móveis](./media/active-directory-developers-guide/NativeApp_Icon.png)<br />Aplicativos da área de trabalho e móveis</center> | [Visão geral](active-directory-authentication-scenarios.md#native-application-to-web-api)<br /><br />[iOS](active-directory-devquickstarts-ios.md)<br /><br />[Android](active-directory-devquickstarts-android.md) | [.NET (WPF)](active-directory-devquickstarts-dotnet.md)<br /><br />[.NET (UWP)](active-directory-devquickstarts-windowsstore.md)<br /><br />[Xamarin](active-directory-devquickstarts-xamarin.md) | [Cordova](active-directory-devquickstarts-cordova.md) |
| <center>![Aplicativos Web](./media/active-directory-developers-guide/Web_app.png)<br />Aplicativos Web</center> | [Visão geral](active-directory-authentication-scenarios.md#web-browser-to-web-application)<br /><br />[ASP.NET](active-directory-devquickstarts-webapp-dotnet.md)<br /><br />[Java](active-directory-devquickstarts-webapp-java.md) | [Python](https://github.com/Azure-Samples/active-directory-python-webapp-graphapi)<br/><br/> [Node.js](active-directory-devquickstarts-openidconnect-nodejs.md) | |
| <center>![Aplicativos de página única](./media/active-directory-developers-guide/SPA.png)<br />Aplicativos de página única</center> | [Visão geral](active-directory-authentication-scenarios.md#single-page-application-spa)<br /><br />[AngularJS](active-directory-devquickstarts-angular.md)<br /><br />[JavaScript](https://github.com/Azure-Samples/active-directory-javascript-singlepageapp-dotnet-webapi) |  |  |
| <center>![APIs da Web](./media/active-directory-developers-guide/Web_API.png)<br />APIs da Web</center> | [Visão geral](active-directory-authentication-scenarios.md#web-application-to-web-api)<br /><br />[ASP.NET](active-directory-devquickstarts-webapi-dotnet.md)<br /><br />[Node.js](active-directory-devquickstarts-webapi-nodejs.md) | &nbsp; |
| <center>![De serviços](./media/active-directory-developers-guide/Service_App.png)<br />Serviço a serviço</center> | [Visão geral](active-directory-authentication-scenarios.md#daemon-or-server-application-to-web-api)<br /><br />[.NET](active-directory-code-samples.md#daemon-applications-accessing-web-apis-with-the-applications-identity)|  |

## <a name="how-to-guides"></a>Guias de instruções
Os guias a seguir guiam você entre algumas das tarefas mais comuns no Azure Active Directory.

|                                                                           |  |
|---------------------------------------------------------------------------| --- |
|[Registro de aplicativo](active-directory-integrating-applications.md)           | Como registrar um aplicativo no Azure AD. |
|[Aplicativos multilocatários](active-directory-devhowto-multi-tenant-overview.md)    | Como entrar em qualquer conta corporativa da Microsoft. |
|[Protocolos OAuth e OpenID Connect](active-directory-protocols-openid-connect-code.md)| Como conectar usuários e chamar APIs Web usando os protocolos de autenticação da Microsoft. |
|[Guias adicionais](active-directory-developers-guide-index.md#guides)        |  Uma lista de guias que estão disponíveis para o Azure AD.   |

## <a name="reference-topics"></a>Tópicos de referência
Os artigos a seguir fornecem informações detalhadas sobre as APIs, as mensagens de protocolo e os termos usados no Azure AD.

|                                                                                   | |
| ----------------------------------------------------------------------------------| --- |
| [Bibliotecas de autenticação (ADAL)](active-directory-authentication-libraries.md)   | Uma visão geral das bibliotecas e SDKs fornecidos pelo Azure AD. |
| [Exemplos de código](active-directory-code-samples.md)                                  | Uma lista de todos os exemplos de código do Azure AD. |
| [Glossário](active-directory-dev-glossary.md)                                      | Terminologia e definições de palavras usadas em toda esta documentação. |
| [Tópicos de referência adicionais](active-directory-developers-guide-index.md#reference)| Uma lista de tópicos de referência que estão disponíveis para o Azure AD.   |


[!INCLUDE [Help and support](../../../includes/active-directory-develop-help-support-include.md)]
