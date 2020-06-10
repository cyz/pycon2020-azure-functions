<a name="introduction-to-serverless-and-azure-functions"></a>Introdução à computação sem servidor e às funções do Azure
================================================

<a name="light-what-is-serverless-computing"></a>|light| O que é a computação sem servidor?
---------------------------------------

A computação sem servidor também é conhecida como FaaS (função como serviço).

Resumindo:

#<a name="-serverless-architecture-makes-use-of-third-party-services-they-might-for-example-run-your-code-on-managed-ephemeral-containers-in-a-faas-platform-azure-functions"></a>. A arquitetura sem servidor usa serviços de terceiros. Eles podem, por exemplo, executar seu código em contêineres gerenciados e efêmeros em uma plataforma FaaS (funções do Azure).
#<a name="-servers-are-still-used-to-run-your-applications-but-in-this-case-your-cloud-provider-takes-care-of-the-management-provisioning-and-scaling-microsoft-azure-in-this-case"></a>. Os servidores ainda são usados para executar seus aplicativos. Mas, nesse caso, seu provedor de nuvem cuida do gerenciamento, do provisionamento e do dimensionamento (neste caso, o Microsoft Azure).

Isso permite que você se concentre no código e implante-o quando estiver pronto, enquanto seu provedor cuida da infraestrutura.

Algumas das vantagens da computação sem servidor:

- Ela é dimensionável: ela não só é dimensionada automaticamente com base no aumento e na diminuição do uso, mas também tem alta disponibilidade.
- Ela pode economizar seu dinheiro: você paga apenas pelo uso (número de execuções) em vez de ter um servidor sendo executado em tempo integral.

O infográfico a seguir fornece mais detalhes sobre a computação sem servidor:

.. image:: _static/images/serverless.png :alt: serverless infographic

Bons casos de uso
****************

Alguns bons casos de uso para a computação sem servidor:

- **Processamento de imagem e vídeo**: você pode associar as funções do Azure ao Armazenamento de Blobs do Azure e usar um gatilho de armazenamento para sua função. Sua função poderá, então, realizar o processamento de forma assíncrona.
- **Internet das Coisas**: os aplicativos de IoT podem gerar muitos dados por meio dos sensores. Você pode usar funções para processar os dados de maneira dimensionável.
- **Pipelines de dados**: você pode integrar vários serviços para criar pipelines de dados dimensionáveis.

<a name="faas-azure-functions-and-serverless"></a>|faas| Funções do Azure e computação sem servidor
----------------------------------------

A FaaS permite que você execute trechos de código independentes chamados de **funções** na nuvem.
Suas funções ficam ociosas até que eventos específicos as disparem.
As funções são independentes, pequenas, de curta duração e de finalidade única.
Elas desaparecem após a execução e, por esse motivo, são chamadas de efêmeras.

As funções são muito versáteis – você pode usar uma variedade de gatilhos para chamar sua função e executar seu código.
Elas podem ser definidas para que sempre executem a mesma tarefa ou executem tarefas específicas com base em entradas.

A FaaS do Microsoft Azure é chamada de `Azure Functions <https://azure.microsoft.com/en-gb/services/functions?WT.mc_id=pycon_tutorial-github-taallard>`_.
Essa FaaS já dá suporte a várias linguagens de programação:

.. image:: https://azurecomcdn.azureedge.net/cvt-e918f8bc2be525756af58617c14443351ac83a8fd87a0b28d31919d627969098/images/page/services/functions/value-prop-5.svg :alt: Linguagens de funções

Portanto, vamos aproveitar o suporte do Python para este tutorial.

O Azure fornece três planos principais para funções, que determinarão o tipo de instâncias usadas, os tempos de execução e os preços.

Para obter mais detalhes, confira os documentos `Azure functions consumption plans <https://docs.microsoft.com/en-us/azure/azure-functions/functions-scale?WT.mc_id=pycon_tutorial-github-taallard>`_.

.. note:: Como as funções sem servidor devem ser sem estado, os recursos dentro da função desaparecerão depois que o código tiver terminado a execução (ou o tempo limite for atingido).


<a name="floppy-additional-resources-and-docs"></a>|floppy| Recursos e documentos adicionais
---------------------------------------


- `Introduction to Azure functions <https://docs.microsoft.com/azure/azure-functions/functions-overview?WT.mc_id=pycon_tutorial-github-taallard>`_
- `Azure functions consumption plans <https://docs.microsoft.com/en-us/azure/azure-functions/functions-scale?WT.mc_id=pycon_tutorial-github-taallard>`_
- `Functions app timeout <https://docs.microsoft.com/en-us/azure/azure-functions/functions-scale#timeout?WT.mc_id=pycon_tutorial-github-taallard>`_
- `Azure Storage docs <https://docs.microsoft.com/en-us/azure/storage/common/storage-introduction#core-storage-services?WT.mc_id=pycon_tutorial-github-taallard>`_
- `Infographic high-res pdf <https://github.com/trallard/tech-bites/tree/master/EN/serverless>`_  CC-BY
