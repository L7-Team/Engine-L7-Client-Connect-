# Engine-L7-Client-Connect-
Engine L7 Aurora é uma reimplementação nativa (C++/JNI) da API ClientConnect do ecossistema Aurora Play. Feita pela Equipe L7 / Stpremy como alternativa à versão Java original, com foco em segurança, performance e suporte completo a redes móveis.

Engine L7 Aurora

ClientConnect nativo em C++/JNI para o ecossistema Aurora Play.

Reimplementação independente feita pela Equipe L7 / Stpremy — com foco em segurança, performance e correção dos bugs de rede da versão original em Java.


O que é

Biblioteca de autenticação para apps do ecossistema Aurora Play. O usuário faz login pelo navegador, o site redireciona via deep link auroraplay e os dados ficam disponíveis na memória RAM do app.

Loja oficial: auroraplay.com.br


O que mudou em relação à API oficial

Recurso API oficial Engine L7 Aurora
Arquitetura 5 classes Java 1 classe ponte + C++ nativo
Cache SharedPreferences (arquivo) RAM (volátil)
URL de login Texto claro Base64 ofuscado
Rede Wi-Fi apenas (bug) Wi-Fi, dados móveis, Ethernet, VPN
Logs Sempre ligados Desligados em produção
Token Salvo em disco Só em memória

Motivos da reescrita: a versão Java original não funcionava bem com dados móveis nem com internet via cabo, e guardava o token em um arquivo que qualquer um com root podia editar. Corrigimos tudo isso em C++.


Como funciona

```
MainActivity.java → EngineL7Aurora.java (ponte) → libL7API.so (C++)
```

O Java é só um escutador de ~25 linhas. Toda a lógica (login, cache, rede, expiração) está na biblioteca nativa pré-compilada.

Fluxo de login:

1. App chama EngineL7Aurora.openLogin()
2. C++ abre o navegador no site da Aurora
3. Usuário loga → site redireciona para auroraplay://login-success?token
4. Android chama EngineL7Aurora.onUri(uri)
5. C++ faz parse, guarda tudo em RAM
6. App consulta com get("email"), get("token"), get("network"), etc.


Requisitos

· Android 7.0+
· ABI: arm64-v8a (por enquanto — ajuda pra compilar em 32 bits é bem-vinda)
· Permissões: INTERNET, ACCESS_NETWORK_STATE


O que abre e o que fecha

Aberto (MIT): EngineL7Aurora.java, documentação, exemplos
Fechado (EULA): libL7API.so — binário pré-compilado, sem código-fonte

A .so contém Engines internas da equipe L7 / Stpremy usadas em outros projetos. Não podemos liberar o código. O Java é aberto porque é só uma ponte — não tem lógica de negócio.


Apoie o projeto

Reescrever essa API em C++ não foi fácil. Se você quer ajudar a manter o projeto vivo:

PIX: fd31af15-8a20-4e0b-9fdd-e0d8255d151a

Comunidade Sketchware no WhatsApp: 

https://chat.whatsapp.com/H6r7dCiVzin4lIh3513LXk?s=cl&p=a&mlu=4&ilr=4

Aviso ao dono da loja

Se o proprietário do Aurora Play quiser que esse projeto seja removido, basta entrar em contato. Retiramos imediatamente. Nosso objetivo é só ajudar a comunidade — sem conflito, sem desrespeito à API original.

API original: Playside Studio
Reescrita C++: Equipe L7 / Stpremy

© 2026 Equipe L7 / Stpremy — Todos os direitos reservados.
