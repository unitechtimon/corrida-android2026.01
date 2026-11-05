# Corrida

App Android simples para registrar corridas: botão START grande, cronômetro, distância em km pelo GPS e aviso por voz (distância e tempo) em intervalo configurável (30 s, 1 min, 2 min ou 5 min).

## Como gerar o APK

### Opção A: GitHub Actions (não precisa instalar nada)

1. Crie um repositório no GitHub e envie esta pasta inteira (inclusive a pasta `.github`).
2. Abra a aba **Actions**, escolha **Gerar APK** e clique em **Run workflow** (ou espere o build rodar sozinho após o envio).
3. Ao terminar, abra a execução e baixe o arquivo **corrida-apk** na seção *Artifacts*. Dentro do zip está o `app-debug.apk`.

### Opção B: Android Studio

1. Instale o Android Studio (gratuito) e use **File > Open** nesta pasta.
2. Aguarde a sincronização do Gradle.
3. Vá em **Build > Build Bundle(s) / APK(s) > Build APK(s)**. O arquivo fica em `app/build/outputs/apk/debug/app-debug.apk`.

## Instalar no celular

Copie o `app-debug.apk` para o aparelho e abra. Se o Android pedir, permita a instalação de apps de fontes desconhecidas para o navegador ou gerenciador de arquivos que você usou.

O APK é assinado com a chave de debug: serve para instalar e testar. Para publicar na Play Store é preciso assinar com uma chave própria e gerar o build *release*.

## Como o app funciona

- Ao tocar em **START**, o app pede permissão de localização, liga o cronômetro e começa a somar a distância pelo GPS.
- A tela mostra tempo, distância em km e **ritmo médio** (min/km; aparece depois dos primeiros 50 m).
- A cada intervalo escolhido, ele fala algo como "Distância: 2,45 quilômetros. Tempo: 12 minutos e 30 segundos. Ritmo médio: 5 minutos e 6 segundos por quilômetro."
- **PAUSAR / RETOMAR**: durante a corrida aparece um botão abaixo do PARAR. Na pausa o tempo e a distância param, e o deslocamento feito enquanto pausado não é somado.
- Ao tocar em **PARAR**, ele fala o resumo final, mantém os valores na tela e **salva a corrida no histórico**.
- **Histórico** (botão no canto superior direito): lista as corridas salvas no aparelho, da mais recente para a mais antiga, com data, distância, tempo e ritmo. Dá para apagar tudo pelo botão *Limpar histórico*.
- Funciona com a tela apagada (serviço em primeiro plano, com notificação fixa).
- A voz usa o português do Brasil. Se ela sair com sotaque ou idioma errado, instale a voz pt-BR em *Configurações > Saída de texto para voz*.

## Ajustes rápidos no código

- Intervalos de voz: `res/layout/activity_main.xml` (botões) e o mapa `intervalByButton` em `MainActivity.kt`.
- Filtros do GPS (precisão, tremedeira, saltos): constantes no topo de `RunService.kt`.
