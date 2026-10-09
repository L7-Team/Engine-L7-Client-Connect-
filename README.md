Engine L7 Aurora

Este não é um produto oficialmente suportado pelo Aurora Play ou Playside Studio.

Visão Geral do Projeto

A Engine L7 Aurora é uma solução nativa de alto desempenho desenvolvida de forma independente pela Equipe L7 / Stpremy para o ecossistema Aurora Play.

Esta arquitetura foi projetada para substituir completamente as implementações tradicionais em Java, transferindo toda a carga crítica de processamento, gestão de rede, validação de tokens e controle de sessão diretamente para a camada nativa em C++ (nível de sistema / baixo nível).

Com isso, o projeto elimina a necessidade de depender de códigos extensos em Java dentro da sua aplicação, garantindo máxima segurança contra análise reversa, zero persistência de dados em arquivos locais e estabilidade total em qualquer ambiente de rede.

Principais Recursos e Diferenciais

 Arquitetura 100% Nativa em C++: Toda a lógica de comunicação, controle de sessão, parsing e segurança roda diretamente através da biblioteca pré-compilada libL7API.so.
 
 Zero Código Java Exposto: Não é necessário implementar diversas classes Java nem expor fluxos de autenticação em código de alto nível. Toda a inteligência reside na biblioteca nativa.
 
 Sessão Volátil em Memória RAM: Credenciais, tokens e informações de usuário nunca são salvos no armazenamento interno (SharedPreferences ou arquivos locais). Os dados existem apenas na memória RAM enquanto o processo estiver em execução, blindando a aplicação contra leitura via Root ou extração local.
 
 Injeção Dinâmica de Recursos: O motor nativo gerencia a integração diretamente no processo do aplicativo, permitindo obter e manipular os dados de sessão com chamadas simples e minimalistas.
 
 Compatibilidade Multirrede Definitiva: Correção completa de falhas de conexão. Funciona perfeitamente em redes Wi-Fi, Dados Móveis (3G, 4G, 5G), conexões cabeadas (Ethernet) e redes privadas (VPN).
 
 Ofuscação de Endpoints: URLs e rotas de comunicação são codificadas em Base64 internamente na camada C++, impedindo inspeção simples de tráfego.
 
 Logs de Produção Desativados: Remoção automática de saídas de depuração em compilações finais, garantindo total privacidade e performance.
 
Estrutura do Pacote de Distribuição (.zip)

Ao realizar o download do pacote oficial da versão mais recente na seção de Releases do repositório, você receberá um arquivo .zip contendo os recursos necessários para a integração.

Conteúdo do Arquivo ZIP

 lib/arm64-v8a/libL7API.so: Biblioteca C++ pré-compilada contendo todo o motor de baixo nível.
 
 AndroidManifest_snippet.xml: Trecho de código do manifesto contendo as permissões de rede e a declaração da Activity/Deep Link necessária para o retorno da autenticação.
 
 TUTORIAL_IMPLEMENTACAO.txt: Guia oficial passo a passo explicando onde posicionar a biblioteca nativa no seu projeto, como configurar o manifesto e como realizar a chamada mínima para consumir as informações da Engine.
 
Como Funciona a Integração

A proposta da Engine L7 Aurora é oferecer uma integração ultrassimples e limpa para o desenvolvedor:

 Inclusão da Biblioteca Nativa: Basta copiar a biblioteca libL7API.so para a pasta de bibliotecas nativas (jniLibs ou diretório correspondente) do seu ambiente de desenvolvimento (Android Studio, Sketchware, etc.).
 
 Configuração do AndroidManifest: Adicione as permissões de rede e a tag do Deep Link no seu manifesto, conforme o modelo fornecido no arquivo AndroidManifest_snippet.xml.
 
 Execução em Baixo Nível: Ao inicializar o motor nativo, a libL7API.so assume o controle das chamadas. Toda a troca de dados, verificação de conectividade e validação de token é tratada diretamente pela linguagem de baixo nível.
 
 Consumo de Dados: Siga as orientações contidas dentro do arquivo TUTORIAL_IMPLEMENTACAO.txt para consultar o status da sessão, e-mail, token e estado de rede do usuário e vinculá-los à sua própria lógica comercial ou banco de dados.
 
Requisitos do Sistema

 Versão Mínima do Android: Android 7.0 (API Level 24) ou superior.
 
 Arquiteturas Suportadas: arm64-v8a.
 
 Permissões de Sistema Necessárias:
 
   android.permission.INTERNET
   
   android.permission.ACCESS_NETWORK_STATE
   
Política do Código e Distribuição

 Código Proprietário e Fechado: 
 
 A biblioteca nativa libL7API.so é distribuída em formato pré-compilado. Ela utiliza motores internos e rotinas proprietárias desenvolvidas pela Equipe L7 / Stpremy, não sendo de código aberto.
 
 Uso Livre para Desenvolvedores: O pacote foi projetado como uma ferramenta para a comunidade. Você pode utilizar a biblioteca compilada para criar suas próprias lógicas, validar acessos, integrar com seus servidores ou gerenciar usuários do seu aplicativo de forma totalmente livre.
 
Relatórios de Erros e Suporte

Para garantir a melhoria contínua da Engine, os relatórios de falhas devem ser enviados contendo os seguintes dados:
 * Erros de Compilação/Build: Envie o arquivo de log gerado pela sua IDE ou ambiente de compilação.
 
 Erros de Execução (Crash/Encerrado): Envie o logcat capturado no momento exato do encerramento da aplicação.
 
 Erros de Conectividade: Informe a versão do Android do dispositivo de teste e a interface de rede utilizada (Wi-Fi, Dados Móveis ou VPN).
 
Canais Oficiais e Apoio ao Projeto

Desenvolver, otimizar e manter uma infraestrutura em código nativo exige dedicação contínua. Se esta Engine contribui para o seu aplicativo ou projeto, considere apoiar a equipe de desenvolvimento:

 Chave PIX: 
 
 fd31af15-8a20-4e0b-9fdd-e0d8255d151a
 
 Grupo Oficial de Suporte no WhatsApp: 
 
 https://chat.whatsapp.com/H6r7dCiVzin4lIh3513LXk?s=cl&p=a&mlu=4&ilr=4
Aviso Legal e Licença

Este projeto é uma reimplementação nativa independente desenvolvida pela Equipe L7 / Stpremy com o intuito de resolver limitações técnicas de desempenho e segurança da API original do Aurora Play.

Caso os detentores dos direitos da plataforma Aurora Play ou Playside Studio solicitem adequações ou a remoção do repositório, as medidas necessárias serão tomadas prontamente.

 API Original: Playside Studio
 
 Reescrita e Engine Nativa (C++/JNI): Equipe L7 / Stpremy
 
 Copyright (C) 2026 Equipe L7 / Stpremy
 
