---
title: Isolando Sua Rede
author: v3nusss
date: 2023-06-23 20:42:00 -0300
categories: [Blogging]
tags: [blog]
---

# Como Isolar Minha Rede?

Primeiramente, clique com o botão direito na sua máquina virtual e selecione "Configurações". Em seguida, vá para a seção de rede. Caso a opção "Habilitar Placa de Rede" esteja desativada, ative-a. Em seguida, altere a configuração de "NAT" para "Rede Interna". Nomeie a rede interna da forma que preferir e clique em "OK". Agora, concluímos todas as configurações necessárias no VirtualBox e podemos prosseguir para o prompt de comando (CMD).

# CMD

Você deve abrir o prompt de comando (CMD) como administrador. Em seguida, digite o comando "cd" seguido do local de instalação do seu VirtualBox. Por padrão, ele é instalado em "C:\Program Files\Oracle\VirtualBox". ja dentro do direitorio rode o comando (vboxmanage dhcpserver add --network= (nome da sua rede interna) --server-ip=10.38.1.1 --lower-ip=10.38.1.110 --upper-ip=10.38.1.120 -netmask=255.255.255.0 --enable) e aperte enter

# Spoiler Proximo Post

No próximo post, exploraremos a realização de um teste de segurança em um alvo dentro da nossa própria rede. Fiquem atentos, pois há muito mais por vir!
