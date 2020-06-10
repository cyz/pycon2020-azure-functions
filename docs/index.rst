.. Arquivo mestre de documentação Processamento de dados fácil no Azure com Funções sem servidor, criado no sphinx-quickstart em 15 de abril de 2020, quarta-feira, às 11:37:06.
Você pode adaptar este arquivo completamente como desejar, mas ele deve pelo menos conter a diretiva de `toctree` raiz.

<a name="cloud-computing-easy-data-processing-on-azure"></a>|computação em nuvem| Processamento de dados fácil no Azure
---------------------------------------------------------

<a name="with-serverless-functions"></a>com Funções sem servidor
---------------------------------------------------------

Bem-vindo ao workshop sobre processamento de dados com o Azure Functions!
Inicialmente, ele foi planejado para ser realizado na PyCon US 2020, mas agora está disponível online como parte dos esforços da incrível equipe da PyCon.

.. image:: _static/icons/MSFT_Logo_Color.png :class: inline-image :width: 80% :align: center :alt: Microsoft logo


<a name="description"></a>Description
--------------
A computação sem servidor (também chamada de função como serviço, FaaS) é um padrão de design em que os aplicativos são hospedados por um serviço de terceiros (ou seja, o Azure). Isso elimina a necessidade de gerenciamento de hardware e software do servidor por parte do desenvolvedor.

A computação sem servidor pode ser uma excelente alternativa para Pythonistas interessados no processamento de dados, pois permite que eles se concentrem no código, e não na infraestrutura de nuvem. Este workshop apresentará aos participantes o Azure Functions para cenários de processamento de dados (incluindo aquisição de dados, limpeza e transformação e armazenamento para uso posterior).

Após este tutorial, os participantes terão experiência prática com o Azure Functions para cenários de processamento de dados. Além disso, eles deixarão o workshop com uma função básica para processamento de dados que pode ser modificada/ampliada para atender às suas necessidades/requisitos.

Estrutura
*********

1. Introdução à computação sem servidor e às funções do Azure
2. Como criar sua primeira função do Azure:
   - Criar uma função agendada simples usando a extensão do VS Code
   - Familiarizar-se com a estrutura e os projetos de funções
   - Como executar e depurar localmente
3. Implantação de funções
   - Implantar sua função no Azure
   - Familiarizar-se com o portal do Azure
4. Caso de uso de processamento de dados
   - Como atualizar sua função para coletar dados
   - Limpeza de dados, agregação e armazenamento

Recursos
***********

#<a name="-there-is-a-video-version-of-the-tutorial-that-can-be-found-on-the-pycon-youtube-channel"></a>. Há uma versão em vídeo do tutorial que pode ser encontrada no canal do YouTube da PyCon:

   .. raw:: html

      <iframe width="560" height="315" src="https://www.youtube.com/embed/PV7iy6FPjAY" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

#<a name="-the-repository-with-all-the-solutions-to-the-tutorial-sections-is-located-at-httpsgithubcomtrallardpycon2020-azure-functions_"></a>. O repositório com todas as soluções para as seções do tutorial está localizado em `<https://github.com/trallard/pycon2020-azure-functions>`_. 

#<a name="-the-accompanying-slides-can-be-found-on-speakerdeck-you-can-read-or-download-them-there"></a>. Os slides associados podem ser encontrados no Speaker Deck, e você pode lê-los ou baixá-los:

   .. raw:: html

      <iframe id="talk_frame_634998" src="//speakerdeck.com/player/3cca413b0553419ba1194696f18384f9" width="710" height="399" style="border:0; padding:0; margin:0; background:transparent;" frameborder="0" allowtransparency="true" allowfullscreen="allowfullscreen" mozallowfullscreen="true" webkitallowfullscreen="true"></iframe>

Pré-requisitos
*********************

Este workshop destina-se a pessoas interessadas em processamento de dados, engenharia de dados ou ciência de dados. O objetivo é fornecer uma introdução prática à computação sem servidor para cenários de processamento de dados.


Supomos que você:

- Tenha conhecimento intermediário de Python:

   - Tenha uma boa compreensão de como escrever e chamar funções
   - Tenha um bom conhecimento de como funcionam os módulos e scripts do Python

- Tenha alguma experiência com estruturação de dados e/ou processamento de dados (não é necessária uma ampla experiência, mas ter usado, por exemplo, bibliotecas como Pandas e solicitações de estruturação de dados e acesso a API)

- Sinta-se confortável ao usar a linha de comando/terminal (não é necessário ser um especialista, mas se sentir confortável o suficiente para navegar pelos sistemas de arquivos e executar tarefas necessárias do Git)

As instruções de instalação e outras orientações para definir seu ambiente de desenvolvimento podem ser encontradas na seção :ref:`setup` deste tutorial.
Siga essas instruções antes de continuar com o restante do tutorial.


.. toctree:: :maxdepth: 2 :caption: Tutorial Table of Contents:

   self setup 01_introduction 02_functions_intro 03_functions_deploy 04_data_function 05_data_export 06_complete_scenario resources
