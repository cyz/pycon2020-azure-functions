<a name="3d-completing-the-scenario"></a>|3d| Conclusão do cenário
==============================

Para concluir o cenário, vamos fazer o seguinte:

- Criar uma nova função que terá como gatilho a criação do arquivo de Armazenamento de Blobs
- Enviar emails automatizados com as URLs das perguntas

Vamos lá.

.. tip:: O repositório que contém todos os scripts e soluções para este tutorial pode ser encontrado em `<https://github.com/trallard/pycon2020-azure-functions>`_.

    👉🏼 The code for this section is in `<https://github.com/trallard/pycon2020-azure-functions/tree/master/solutions/03-full-pipeline>`_ 


1. Criar sua nova função
------------------------------

A criação de uma nova função em um projeto de funções existente é muito semelhante ao processo que seguimos na seção :ref:`functions101`.

Dentro do mesmo workspace do VS Code que usamos até agora:

#<a name="-click-on-the-azure-extension-on-the-sidebar"></a>. Clique na extensão do Azure na barra lateral.
#<a name="-in-the-azure-functions-section-click-on-the-create-function-icon"></a>. Na seção de funções do Azure, clique no ícone **Criar função**.

    .. image:: _static/images/snaps/new_function.png
            :align: center
            :alt: Create function

#<a name="-select-the-azure-blob-storage-trigger-and-azurewebjobsstorage"></a>. Selecione **Gatilho Armazenamento de Blobs do Azure** e **AzureWebJobsStorage**.
#<a name="-finally-provide-the-blob-path-to-be-monitored-functionblobnamecsv"></a>. Por fim, forneça o caminho do blob a ser monitorado: ``functionblob/{name}.csv``.

Como antes, vou renomear o ``scriptFile`` como ``blob_manipulation.py`` para manter meu workspace organizado.

.. note:: Aqui estamos filtrando por extensão de arquivo e caminho ``functionblob/{name}.csv``. Para obter mais padrões, confira `Blob name patterns docs <https://docs.microsoft.com/en-us/azure/azure-functions/functions-bindings-storage-blob-trigger?tabs=python#blob-name-patterns>`_.

2. Adicionar associações
------------------------------
Precisamos criar mais duas associações de saída:

- SendGrid: para enviar um email com o relatório
- Armazenamento de Blobs do Azure: para salvar a saída das funções

Armazenamento de Blobs
******************************

#<a name="-attach-a-blob-storage-binding-we-are-going-to-follow-the-same-process-as-in-section-refattachblob-follow-this-similar-configuration"></a>. Anexe uma associação de armazenamento de Blobs. Vamos seguir o mesmo processo que na seção :ref:`attachblob`. Siga esta configuração semelhante:

    .. code-block:: json

        {
        "type": "blob",
        "direction": "out",
        "name": "outputBlob",
        "path": "functionblob/{name}_tag_plot.png",
        "connection": "AzureWebJobsStorage"
        }

SendGrid por Twilio
******************************

#<a name="-head-to-azureportal-on-the-left-sidebar-click-on--create-a-resource-then-on-the-search-bar-type-sendgrid"></a>. Vá para |azureportal|. Na barra lateral esquerda, clique em **+ Criar um recurso**. Em seguida, clique no Tipo de Barra de Pesquisa **SendGrid**.
#<a name="-click-on-the-create-button"></a>. Clique no botão **Criar**.

    .. image:: _static/images/snaps/sendgrid.png
        :align: center
        :alt: Create sendgrid

#<a name="-fill-the-details-in-the-create-form---make-sure-to-select-the-same-resource-group-we-have-been-using-as-an-azure-customer-you-get-25000-emails-free-per-month-once-completed-click-on-review--create--and-create"></a>. Preencha os detalhes no formulário de criação - não deixe de selecionar o mesmo grupo de recursos que temos usado. Como cliente do Azure, você recebe 25,000 emails gratuitos por mês. Quando terminar, clique em **Examinar + Criar** e **Criar**.

#<a name="-you-will-a-progress-bar-on-top-of-your-screen-click-on-it-and-wait-for-your-deployment-to-complete-once-completed-click-on-go-to-resource"></a>. Você verá uma barra de progresso na parte superior da tela. Clique nela e aguarde a conclusão da implantação. Quando terminar, clique em **Ir para o recurso**.


    .. image:: _static/images/snaps/sendgrid2.png
            :align: center
            :alt: Create sendgrid

#<a name="-click-on-the-manage-tab"></a>. Clique na guia **Gerenciar**.

    .. image:: _static/images/snaps/sendgrid3.png
        :align: center
        :alt: Sengrid manage

#<a name="-you-will-be-redirected-to-your-sendgrid-dashboard-httpsappsendgridcom_-once-there-click-on-settings---api-keys--create-api-key"></a>. Você será redirecionado para `SendGrid dashboard <https://app.sendgrid.com>`_. Lá, clique em **Configurações**  > **Chaves de API** > **Criar Chave de API**.

    .. image:: _static/images/snaps/sendgrid4.png
        :align: center
        :alt: Create API key

#<a name="-in-the-next-screen-give-your-key-a-name-select-full-access-and-then-create--view"></a>. Na próxima tela, dê um nome à sua chave, selecione **Acesso Completo** e, em seguida, **Criar e exibir**.

    .. image:: _static/images/snaps/sendgrid5.png
        :align: center
        :alt: Create API key

    Make sure to take note of your API key as we will need it to add the binding.

#<a name="-back-in-vs-code-lets-create-the-binding-click-on-the-azure-extensions-tab-in-the-sidebar-then-in-azure-functions-right-click-on-the-newly-created-function-oe-blob-manipulation-followed-by-add-binding"></a>. De volta ao **VS Code**: vamos criar a associação. Clique na guia **Extensões do Azure** na barra lateral. Em seguida, em Azure functions, **clique com o botão direito do mouse** na função recém-criada (por exemplo, blob-manipulation** seguida por **Adicionar associação...** .

    .. image:: _static/images/snaps/sendgridbind.png
        :align: center
        :alt: Create new binding

#<a name="-select-the-following-options"></a>. Selecione as seguintes opções:

    - **Direção da associação**: out
    - **Selecionar associação** SendGrid
    - **Nome para identificar a associação**: sendemail
    - **Selecionar configuração de "local.settings.json**: Clique em **+ Criar nova configuração de aplicativo local** e nomeie-a como SendGridAPIKeyAsAppSetting
    - **Para enviar por email, de email e assunto**: pressione Enter conforme especificaremos no código

#<a name="-update-your-sendgrid-api-key-in-your-localsettingjson-file"></a>. Atualize a chave de API de SendGrid no arquivo ``local.setting.json``.

.. tip:: Depois de concluir essas seções, seu arquivo ``function.json`` deve ter a seguinte aparência:

    .. literalinclude:: ../solutions/03-full-pipeline/blob-manipulation/function.json
        :language: json
        :caption: blob-manipulation/function.json

#<a name="-update-your-env-file-to-add-the-sender-and-receiver-email-note-the-sender-must-be-the-same-email-associated-with-your-sendgrid-app"></a>. Atualize seu arquivo ``.env`` para adicionar o remetente e o email do destinatário. (Observe que o remetente deve ser o mesmo email associado ao seu aplicativo SendGrid).

    .. code-block:: python
        :caption: .env 

        SE_client_id = "******"
        SE_client_secret = "******"
        MyStorageConnectionAppSetting = "******"
        receiver = "******"
        sender = "******"


3. Atualizar seu código e requisitos
---------------------------------------

Vamos atualizar o código para executar as seguintes tarefas:

- Obter o arquivo CSV adicionado (Armazenamento de Blobs)
- Executar algumas manipulações básicas com pandas 
- Criar uma plotagem com as 15 primeiras marcas usadas nas perguntas coletadas
- Enviar um email com as novas perguntas e a plotagem criada

#<a name="-similar-to-section-refblobfunction-we-will-create-a-utils-directory-with-a-processingpy-script-in"></a>. Semelhante à seção :ref:`blobfunction`, criaremos um diretório ``utils`` com um script ``processing.py`` em:

    .. literalinclude:: ../solutions/03-full-pipeline/blob-manipulation/utils/processing.py
            :language: python
            :caption: blob-manipulation/utils/processing.py

#<a name="-and-update-our-blob_manipulationpy-script"></a>. E atualizaremos nosso script ``blob_manipulation.py``:

    .. literalinclude:: ../solutions/03-full-pipeline/blob-manipulation/blob_manipulation.py
        :language: python
        :caption: blob-manipulation/blob_manipulation.py
        :emphasize-lines: 38-42


#<a name="-finally-make-sure-to-update-your-requirementstxt-file"></a>. Por fim, não deixe de atualizar seu arquivo ``requirements.txt``:

    .. literalinclude:: ../solutions/03-full-pipeline/requirements.txt
        :language: python
        :caption: requirements.txt

Agora estamos prontos para depurar as funções localmente 🎉!

4. Como executar e depurar localmente
---------------------------------------

#<a name="-press-kbdf5-you-should-see-the-function-being-started-in-the--output-terminal-in-vs-code"></a>. Pressione :kbd:`F5`. Você deve ver a função que está sendo iniciada no **terminal de saída** no VS Code. 
#<a name="-click-on-the--azure--extension-then-on-the-azure-functions-section-right-click-on-the-timer-function--execute-function-now"></a>. Clique na extensão do **Azure** e, em seguida, na seção de **funções do Azure**, clique com o botão direito do mouse em `timer-function` > **Executar a função agora**.

Isso irá disparar a execução de sua função de temporizador e a função de Blob assim que o arquivo `.csv.` for adicionado ao seu blob. 


5. Como implantar sua função
---------------------------------------

Se você se lembrar corretamente, primeiro criamos um projeto de funções e adicionamos a função de processamento. Isso nos permite implantar ambas as funções diretamente no mesmo projeto de aplicativo.

    .. image:: _static/images/snaps/project.png
            :align: center
            :alt: Deploy project

Seguiremos o mesmo processo de antes:

#<a name="-deploy-from-the-azure-functions-extension-in-vs-code"></a>. Implante desde a extensão de funções do Azure no VS Code.
#<a name="-head-to-azureportal--function-app--your-function-app--configuration-and-we-will-add-the-new-variables-we-added-to-this-function-receiver-sender-sendgridapikeyasappsetting"></a>. Vá para |azureportal| > **Aplicativo de Função** > <your function app> > **Configuração** e adicionaremos as novas variáveis que adicionamos a esta função: ``receiver, sender, SendGridAPIKeyAsAppSetting``.

    .. image:: _static/images/snaps/envs2.png
            :align: center
            :alt: Create variables

Agora você pode disparar sua função pelo portal!!!

<a name="you-have-completed-the-tutorial-"></a>Você concluiu o tutorial!!! 🎉
---------------------------------------

.. raw:: html

    <div style="width:100%;height:0;padding-bottom:100%;position:relative;"><iframe src="https://giphy.com/embed/l4HodBpDmoMA5p9bG" width="100%" height="100%" style="position:absolute" frameBorder="0" class="giphy-embed" allowFullScreen></iframe></div><p><a href="https://giphy.com/gifs/thisisgiphy-reaction-audience-l4HodBpDmoMA5p9bG">via GIPHY</a></p>

<a name="floppy-additional-resources-and-docs"></a>|floppy| Recursos e documentos adicionais
---------------------------------------

- `Azure Blob Storage trigger docs <https://docs.microsoft.com/en-us/azure/azure-functions/functions-bindings-storage-blob-trigger?tabs=python?WT.mc_id=pycon_tutorial-github-taallard>`_
- `Blob name patterns <https://docs.microsoft.com/en-us/azure/azure-functions/functions-bindings-storage-blob-trigger?tabs=python#blob-name-patterns?WT.mc_id=pycon_tutorial-github-taallard>`_
- `Azure Blob storage input binding <https://docs.microsoft.com/en-us/azure/azure-functions/functions-bindings-storage-blob-input?tabs=python?WT.mc_id=pycon_tutorial-github-taallard>`_
- `SendGrid by Twilio <https://sendgrid.com/docs/>`_
- `SenGrid Python API <https://github.com/sendgrid/sendgrid-python>`_
- `SendGrid API - POST email <https://github.com/sendgrid/sendgrid-python/blob/master/USAGE.md#post-mailsend>`_
