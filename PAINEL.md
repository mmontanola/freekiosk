# FreeKiosk — fork "painel"

Fork de [RushB-fr/freekiosk](https://github.com/RushB-fr/freekiosk) (MIT) mantido
para o painel de parede do projeto `moto-e22-wallpanel`: um Motorola moto e22
(Android 12, 32 bits, 1,86 GB de RAM) mostrando o Home Assistant 24 horas por
dia. O objetivo é substituir o Fully Kiosk por software aberto, sem perder o que
o painel usa hoje: modo quiosque, câmera, detecção de movimento, captura de tela,
controle remoto da tela e integração com o Home Assistant.

## Branches e versões

- `main` acompanha o upstream sem alterações.
- `painel` é o branch de trabalho: parte de uma tag do upstream e soma as nossas
  mudanças, cada uma num commit separado e explicado.
- Versão: `<versão do upstream>-painel.<n>` (ex.: `2.0.0-beta.5-painel.1`).
  A tag `painel-v<versão>` dispara o build e publica o APK.

## Build

`.github/workflows/painel-build.yml` compila o APK de release a partir do código
no GitHub Actions (as ferramentas do Android SDK não existem para ARM64, que é o
servidor do projeto) e o assina com a chave própria do painel. A chave fica nos
segredos do repositório e, a original, em `/etc/freekiosk/` no servidor, só para
root. O workflow confere que o APK saiu com essa assinatura e publica o SHA-256.

Por que uma chave própria: o Android só aceita atualizar um app com a mesma
assinatura. Instalando desde o começo a nossa build, as próximas versões do fork
entram por cima sem perder a configuração.

## Mudanças em relação ao upstream

| Versão | Mudança | Por quê |
| --- | --- | --- |
| painel.1 | build do fork no GitHub Actions, assinatura própria | APK reproduzível a partir do código |

Mudanças que servem a qualquer usuário (tradução, correções) devem voltar ao
upstream como pull request.
