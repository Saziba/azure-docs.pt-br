---
title: 'Kit de Desenvolvimento de IoT para nuvem: conectar Kit de Desenvolvimento MXChip de IoT para Hub IoT | Microsoft Docs'
description: Neste tutorial, saiba como enviar status de sensores em IoT DevKit AZ3166 ao Azure IoT Suite para monitoramento e visualização.
services: iot-hub
documentationcenter: ''
author: liydu
manager: timlt
tags: ''
keywords: ''
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2018
ms.author: liydu
ms.openlocfilehash: 17b24244180436c2d1f97433e13a530dae565a10
ms.sourcegitcommit: e2adef58c03b0a780173df2d988907b5cb809c82
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/28/2018
---
# <a name="connect-mxchip-iot-devkit-to-azure-iot-suite-for-remote-monitoring"></a>Conectar Kit de Desenvolvimento de IoT MXChip para Azure IoT Suite para monitoramento remoto

Neste tutorial, você aprenderá como executar um aplicativo de exemplo em DevKit para enviar os dados do sensor para o seu Azure IoT Suite.

O [MXChip IoT DevKit](https://aka.ms/iot-devkit) é uma placa compatível com Arduino all-in-one periféricos e sensores avançados. É possível desenvolvê-lo usando a [extensão do Visual Studio Code para Arduino](https://aka.ms/arduino). E vem com um [catálogo de projetos](https://microsoft.github.io/azure-iot-developer-kit/docs/projects/) crescente para guiá-lo no protótipo de soluções de IoT (Internet das Coisas) que aproveitam os serviços do Microsoft Azure.

## <a name="what-you-need"></a>O que você precisa

Siga o [Guia de Introdução](https://docs.microsoft.com/azure/iot-hub/iot-hub-arduino-iot-devkit-az3166-get-started) para:

* Ter seu DevKit conectado ao Wi-Fi
* Preparar o ambiente de desenvolvimento

Uma assinatura ativa do Azure. Se você não tiver uma, você pode registrar por meio de um desses dois métodos:

* Ative uma [conta do Microsoft Azure de avaliação por 30 dias](https://azure.microsoft.com/free/)
* Declare seu [crédito do Azure](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) se você for assinante do MSDN ou o Visual Studio

## <a name="create-an-azure-iot-suite"></a>Criar um Azure IoT Suite

1. Vá para o site [Azure IoT Suite](https://www.azureiotsuite.com/) e clique em **Criar uma nova solução**.
  ![Selecione o tipo de Azure IoT Suite](media/iot-hub-arduino-iot-devkit-az3166-devkit-remote-monitoring/azure-iot-suite-solution-types.png)
  > [!WARNING]
  > Por padrão, este exemplo cria um S2 IoT Hub depois que ele cria um conjunto de IoT Suite. Se este IoT hub não for usado com um grande número de dispositivos, é altamente recomendável fazer o downgrade do S2 para S1 e excluir o IoT Suite para que o Hub IoT relacionado também possa ser excluído quando você não precisa mais dele. 

2. Selecione **Monitoramento remoto**.

3. Insira um nome de solução, selecione uma assinatura e uma região e, em seguida, clique em **Criar solução**. A solução pode demorar um pouco para ser provisionada.
  ![Criar solução](media/iot-hub-arduino-iot-devkit-az3166-devkit-remote-monitoring/azure-iot-suite-new-solution.png)

4. Após o provisionamento ser concluído, clique em **Inicialização**. Alguns dispositivos simulados são criados para a solução durante o processo de provisionamento. Clique em **DISPOSITIVOS** para fazer check-out. ![Painel](media/iot-hub-arduino-iot-devkit-az3166-devkit-remote-monitoring/azure-iot-suite-new-solution-created.png)
  ![Console](media/iot-hub-arduino-iot-devkit-az3166-devkit-remote-monitoring/azure-iot-suite-console.png)

5. Clique em **ADICIONAR UM DISPOSITIVO**.

6. Clique em **Adicionar novo** para **Dispositivo Personalizado**.
  ![Adicionar novo dispositivo](media/iot-hub-arduino-iot-devkit-az3166-devkit-remote-monitoring/azure-iot-suite-add-new-device.png)

7. Clique em **Deixe-me definir minha própria ID de dispositivo**, digite `AZ3166`e, em seguida, clique em **Criar**.
  ![Criar dispositivo com ID](media/iot-hub-arduino-iot-devkit-az3166-devkit-remote-monitoring/azure-iot-suite-new-device-configuration.png)

8. Anote **Hub IoT Hostname**e clique em **Pronto**.

## <a name="open-the-remotemonitoring-sample"></a>Abra a amostra RemoteMonitoring

1. Desconecte o DevKit de seu computador, se ele estiver conectado.

2. Iniciar o VS Code.

3. Conecte o DevKit ao computador. O Código VS detecta automaticamente o DevKit e abre as seguintes páginas:
  * Página de introdução do DevKit.
  * Exemplos de Arduino: Exemplos práticos de como começar com DevKit.

4. Expanda a seção **EXEMPLOS DO ARDUINO** no canto esquerdo, vá até **Exemplos para MXCHIP AZ3166 > AzureIoT** e selecione **RemoteMonitoring**. Isso abrirá uma nova janela do VS Code com a pasta de projeto nela.
  > [!NOTE]
  > Se você fechar o painel, você poderá reabri-lo. Use `Ctrl+Shift+P` (macOS: `Cmd+Shift+P`) para abrir a paleta de comandos, digite **Arduino** e, em seguida, localize e selecione **Arduino: Exemplos**.

## <a name="provision-required-azure-services"></a>Provisionar serviços necessários do Azure

Na janela de solução, execute a tarefa por meio de `Ctrl+P` (macOS: `Cmd+P`) digitando `task cloud-provision` na caixa de texto fornecida:

No terminal do VS Code, uma linha de comando interativa orienta você durante o provisionamento dos serviços do Azure necessários:

![Provisionar recursos do Azure](media/iot-hub-arduino-iot-devkit-az3166-devkit-remote-monitoring/provision.png)

## <a name="build-and-upload-the-device-code"></a>Compilação e carregamento do código de dispositivo

1. Use `Ctrl+P` (macOS: `Cmd + P`) e o digite a **conexão dos dispositivos de configuração da tarefa**.

2. O terminal solicitará que você queira usar a cadeia de caracteres de conexão que recupera do `task cloud-provision` etapa. Você também pode inserir sua própria cadeia de caracteres de conexão do dispositivo clicando em 'Criar novo...'

3. O terminal solicita que você entre no modo de configuração. Para fazer isso, mantenha o botão A pressionado e, em seguida, solte o botão Reiniciar. A tela exibe a ID do Kit de Desenvolvimento e “Configuração”.
  ![Inserir cadeia de conexão](media/iot-hub-arduino-iot-devkit-az3166-devkit-remote-monitoring/config-device-connection.png)

4. Depois de `task config-device-connection` terminar, clique em `F1` para carregar os comandos de VS Code e selecione `Arduino: Upload`, o VS Code inicia verificando e carregando o sketch do Arduino: ![verificação e carregamento do esboço sketch Arduino](media/iot-hub-arduino-iot-devkit-az3166-devkit-remote-monitoring/arduino-upload.png)

O Kit de Desenvolvimento reinicia e começa a execução do código.

## <a name="test-the-project"></a>Teste do projeto

Quando o aplicativo de exemplo for executado, o DevKit envia dados de sensor por Wi-Fi para o Azure IoT Suite. Para ver o resultado, siga estas etapas:

1. Vá para o Azure IoT Suite e clique em **DASHBOARD**.

2. No console de solução do Azure IoT Suite, você verá o status do sensor de DevKit.

![Dados de sensor no Azure IoT Suite](media/iot-hub-arduino-iot-devkit-az3166-devkit-remote-monitoring/sensor-status.png)

## <a name="change-device-id"></a>Alterar ID do dispositivo

Você pode alterar a ID do dispositivo no Hub IoT seguindo [neste guia](https://microsoft.github.io/azure-iot-developer-kit/docs/customize-device-id/). E se você quiser alterar o **AZ3166** codificado para a ID de dispositivo personalizada no código. [Aqui](https://github.com/Microsoft/devkit-sdk/blob/master/AZ3166/src/libraries/AzureIoT/examples/RemoteMonitoring/RemoteMonitoring.ino#L23) está a linha de código que você pode modificar.

## <a name="problems-and-feedback"></a>Comentários e problemas

Se você encontrar problemas, consulte [Perguntas frequentes](https://microsoft.github.io/azure-iot-developer-kit/docs/faq/) ou entre em contato conosco pelos canais abaixo:

* [Gitter.im](http://gitter.im/Microsoft/azure-iot-developer-kit)
* [Stackoverflow](https://stackoverflow.com/questions/tagged/iot-devkit)

## <a name="next-steps"></a>Próximas etapas

Agora que você aprendeu como conectar a um dispositivo DevKit para o Azure IoT Suite e visualizar os dados de sensor, aqui estão as próximas etapas sugeridas:

* [Visão geral do Azure IoT Suite](https://docs.microsoft.com/azure/iot-suite/)
* [Conectar um dispositivo MXChip IoT DevKit ao aplicativo Microsoft IoT Central](https://docs.microsoft.com/microsoft-iot-central/howto-connect-devkit)
