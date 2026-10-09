Engine L7 Aurora

Este não é um produto oficialmente suportado pelo Aurora Play ou Playside Studio.
Introdução

Engine L7 Aurora é uma reimplementação nativa de alto desempenho (C++/JNI) da API ClientConnect para o ecossistema Aurora Play, desenvolvida de forma independente pela Equipe L7TEAM / Stpremy.

Esta nova versão foi criada para substituir a implementação original em Java, com foco total em segurança avançada, eliminação de vazamentos de credenciais no armazenamento local e suporte completo a múltiplas interfaces de rede.

Recursos em Destaque

 Core Nativo em C++: Lógica de autenticação, parsing e gerenciamento de sessão isolados na biblioteca nativa libL7API.so.
 
 Sessão Volátil (In-Memory Cache): Tokens e credenciais ficam salvos apenas na memória RAM do dispositivo. Isso impede a leitura por Root ou a extração de dados salvos em arquivos locais.
 
 Suporte Completo a Redes: Correção definitiva dos problemas de conectividade. A biblioteca funciona nativamente em Wi-Fi, redes móveis (3G, 4G, 5G), Ethernet e conexões VPN.
 
 URLs Ofuscadas: Endpoints e rotas sensíveis são codificados em Base64 para evitar a inspeção simples de tráfego.
 * Logs de Produção Desativados: Os logs de depuração do sistema são desativados automaticamente em compilações finais de produção.
 
Downloads e Arquivos do Projeto

O GitHub é a única fonte oficial para obter informações, atualizações e downloads verificados da Engine L7 Aurora.

Na seção de Releases / Download Mais Recente, você encontrará o arquivo zipado com todo o pacote necessário para a integração no seu aplicativo.

Conteúdo do Pacote ZIP

Ao baixar o arquivo .zip da release mais recente e descompactá-lo, você encontrará a seguinte estrutura:

 lib/arm64-v8a/libL7API.so: Biblioteca C++ nativa pré-compilada.
 
 EngineL7Aurora.java: Classe ponte em Java pronta para ser adicionada ao seu projeto.
 
 AndroidManifest_snippet.xml: Trecho com as permissões e a tag da Activity com o Deep Link para colocar no manifesto do seu app.
 
 TUTORIAL_IMPLEMENTACAO.txt: Guia passo a passo em texto explicando como configurar tudo, importar as bibliotecas e realizar as chamadas do método dentro do seu projeto (compatível com Android Studio e Sketchware).
 
O que mudou no Projeto

Como funcionava antes

A versão oficial em Java dependia de 5 classes inteiras para realizar o fluxo de login. Ela salvava o token de autenticação em um arquivo SharedPreferences gravado diretamente no armazenamento do celular (o que permitia que usuários com acesso Root modificassem o token), mantinha URLs e rotas visíveis em texto claro, e apresentava falhas frequentes ao tentar autenticar usando redes móveis ou conexões via cabo. Além disso, gerava logs detalhados de sistema a todo momento.

Como funciona agora

Toda a lógica pesada de rede, processamento, validação e cache foi transferida para a biblioteca nativa libL7API.so em C++. O Java agora é apenas uma classe ouvinte (ponte) de poucas linhas que recebe o redirecionamento da Intent do Android. O token de sessão não é salvo no disco do aparelho, permanecendo exclusivamente na memória RAM enquanto a aplicação estiver em execução. As conexões funcionam sem quedas ou bugs em Wi-Fi, dados móveis e VPN, com URLs ofuscadas e logs desligados na versão final.

Estrutura e Fluxo de Execução

O seu aplicativo faz a chamada de login chamando a classe ponte Java.

 A camada nativa C++ abre o navegador no site do Aurora Play.
 
 O usuário realiza a autenticação e o site redireciona para a URL do Deep Link (auroraplay login-success?token=...).
 
 A Activity do seu app recebe a URI de retorno e repassa os dados para a ponte.
 
 A biblioteca libL7API.so faz o parse nativo, valida o token e armazena os dados de sessão na memória RAM.
 
 Seu aplicativo consulta as informações de usuário (como e-mail, token e estado da rede) diretamente na memória.
 
Requisitos do Sistema

 Versão Mínima do Android: Android 7.0 (API Level 24) ou superior.
 
 Arquiteturas Suportadas: arm64-v8a.
 Permissões Necessárias:
 
   android.permission.INTERNET
   android.permission.ACCESS_NETWORK_STATE
   
Como Implementar

Não é necessário escrever códigos complexos manualmente do zero. Basta baixar o arquivo .zip disponível na seção de Downloads do repositório, extrair o conteúdo e abrir o arquivo TUTORIAL_IMPLEMENTACAO.txt.

Dentro do arquivo .txt, você encontrará as instruções exatas de:

 Onde colar o arquivo EngineL7Aurora.java.
 
 Onde posicionar a pasta de bibliotecas nativas (libL7API.so).
 
 Como copiar o snippet do AndroidManifest.xml.
 
 Como fazer o tratamento do Deep Link no evento de carregamento da sua MainActivity.
 
Política do Código e Módulos

 Código Aberto: O arquivo ponte Java (EngineL7Aurora.java), arquivos de manifesto, documentação e tutoriais.
 
 Código Proprietário: A biblioteca nativa compilada libL7API.so.
 
> Nota: 

O arquivo .so contém bibliotecas e engines internas desenvolvidas pela Equipe L7 / Stpremy que são reaproveitadas em outros softwares da equipe, motivo pelo qual o código C++ é distribuído pré-compilado. 

A ponte Java permanece aberta para inspeção e fácil inclusão no seu projeto.

> 

Relatórios de Erros
Para manter a estabilidade do projeto, 

aceitamos relatórios de falhas com os seguintes requisitos:

 Erros de Instalação/Compilação: Envie o arquivo de log do Build do seu ambiente ou do Android Studio/Sketchware.
 
 Erros de Execução/Crash: Grave e envie o logcat capturado exatamente no momento do encerramento inesperado.
 
 Erros de Conexão: Informe o tipo de rede utilizada (Dados Móveis, Wi-Fi, VPN) e a versão do Android do aparelho testado.
 
Apoie o Projeto

Desenvolver e otimizar essa biblioteca nativa exige tempo, testes e manutenção contínua. Se este projeto ajuda na sua aplicação ou comunidade, considere apoiar o trabalho do desenvolvedor:

 Chave PIX: fd31af15-8a20-4e0b-9fdd-e0d8255d151a
 
 Comunidade no WhatsApp: Grupo de Suporte Sketchware e Desenvolvedores
 
 https://chat.whatsapp.com/H6r7dCiVzin4lIh3513LXk?s=cl&p=a&mlu=4&ilr=4
 
Aviso Legal

Este projeto é uma reimplementação independente feita com o objetivo de colaborar com a comunidade e resolver falhas de desempenho da versão Java anterior.

Se o proprietário dos direitos da plataforma Aurora Play ou Playside Studio desejar a alteração ou remoção deste repositório, basta entrar em contato para que a remoção ou adequação seja realizada imediatamente.

 API Original: Playside Studio
 
 Reescrita Nativa (C++/JNI): 
 
 Equipe L7 / Stpremy
 
Licença
A documentação, tutoriais e o código aberto da ponte Java deste projeto são software livre: 

você pode redistribuí-los e/ou modificá-los sob os termos da GNU General Public License (GPLv3) conforme publicada pela Free Software Foundation, seja a versão 3 da Licença ou (a seu critério) qualquer versão posterior.

Engine L7 Aurora - ClientConnect Nativo
Copyright (C) 2026 Equipe L7 / Stpremy

Este programa é distribuído na expectativa de que seja útil,

mas SEM QUALQUER GARANTIA; 

sem mesmo a garantia implícita de
COMERCIABILIDADE ou ADEQUAÇÃO A UM DETERMINADO PROPÓSITO. Veja a
GNU General Public License para obter mais detalhes.

Você deve ter recebido uma cópia da Licença Pública Geral GNU
junto com este programa. Se não, consulte <http://www.gnu.org/licenses/>.
