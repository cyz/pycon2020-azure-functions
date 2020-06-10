.. _deployfn:

<a name="cloud-computing-deploy-your-first-function"></a>|cloud-computing| Implantar sua primeira função
==============================================

A próxima etapa será implantar sua função no Azure. Usaremos a extensão do VS Code novamente.

1. Clique na extensão do Azure na barra lateral do VS Code (1 na imagem) e, em seguida, clique em implantar para o aplicativo de funções na seção de funções do Azure (2 na imagem).

    .. image:: _static/images/snaps/deploy1.png :align: center :alt: Preparar-se para implantar

2. Selecione a opção **Criar aplicativo** e forneça um nome para seu aplicativo.
3. Selecione a versão de runtime do Python correta.
4. Selecione um local para seus recursos (o data center onde todos os seus recursos estarão localizados, por exemplo, na Europa Ocidental).
5. Aguarde a conclusão da implantação. Você pode ver o progresso na janela pop-up ou no console de saída.

.. _portalinst:

<a name="using-the-azure-portal"></a>Usar o portal do Azure
--------------------------

Há várias maneiras de verificar o status da sua função. Faremos isso no portal do Azure.

#<a name="-head-to-azureportal"></a>. Vá para |azureportal|.
#<a name="-click-on-the-home-icon-on-the-sidebar-if-the-sidebar-is-hidden-you-need-to-click-on-the--icon-on-the-top-left-corner"></a>. Clique no ícone de início na barra lateral (se a barra lateral estiver oculta, você precisará clicar no ícone ``>>`` no canto superior esquerdo).
#<a name="-the-default-home-view-should-show-your-new-resources-for-me-it-shows-the-resource-group-called-pycon2020-as-this-is-the-name-i-gave-it"></a>. A exibição Início padrão deve mostrar os novos recursos. Para mim, ela mostra o grupo de recursos chamado ``pycon2020``, pois esse é o nome que eu forneci.

    .. image:: _static/images/snaps/portal_01.png
            :align: center
            :alt: Azure portal home

#<a name="-on-the-sidebar-find-the-function-app-section-and-click-on-it-1-in-image-and-the-on-your-function-name"></a>. Na barra lateral, localize a seção **Aplicativo de funções** e clique nela (1 na imagem) e no nome da função:

    .. image:: _static/images/snaps/portal_02.png
            :align: center
            :alt: Function app

#<a name="-click-on-monitor-in-the-new-sidebar"></a>. Clique em **Monitorar** na nova barra lateral.

    .. image:: _static/images/snaps/portal_03.png
            :align: center
            :alt: Monitor function

#<a name="-in-the-following-screen-you-should-be-able-to-see-the-status-of-your-function-the-runs-and-their-statuses-as-well-as-the-url-for-your-app-you-can-also-click-on-each-individual-run-to-check-the-logs-output"></a>. Na tela a seguir, você deve poder visualizar o status de sua função, as execuções e os status, bem como a URL para seu aplicativo. Você também poderá clicar em cada execução individual para verificar a saída dos logs.

    .. image:: _static/images/snaps/portal_04.png
            :align: center
            :alt: Resource group

🎉 Parabéns, você implantou sua primeira função sem servidor! 🥳


<a name="floppy-additional-resources-and-docs"></a>|floppy| Recursos e documentos adicionais
---------------------------------------

- `Monitoring Azure functions <https://docs.microsoft.com/azure/azure-functions/functions-monitoring?tabs=cmd&WT.mc_id=pycon_tutorial-github-taallard>`_ 
