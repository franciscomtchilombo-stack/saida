# Teclado de Umbundu

Teclado QWERTY interativo com acesso direto às vogais nasais. Roda como PWA no navegador e como **APK Android** (Capacitor), gerado automaticamente pelo GitHub Actions.

## Gerar o APK pelo GitHub

1. Crie um repositório no GitHub e envie todos os arquivos deste projeto (inclusive `.github/` e `android-res/`).
2. Abra a aba **Actions → Build APK → Run workflow** (também roda sozinho a cada push em `main`).
3. Ao terminar (~5–8 min), abra a execução e baixe **Teclado-Umbundu-apk** em *Artifacts*. Dentro há `Teclado-Umbundu-debug.apk`.
4. Copie o APK para o celular e instale (permita "instalar apps desconhecidos").

**Release com link fixo:** crie uma tag (`git tag v1.0.0 && git push --tags`); o APK é anexado em *Releases*.

### APK assinado (opcional, para publicar na Play Store)
Gere uma chave: `keytool -genkey -v -keystore release.keystore -alias teclado -keyalg RSA -keysize 2048 -validity 10000`
Em *Settings → Secrets and variables → Actions* crie:
`ANDROID_KEYSTORE_BASE64` (`base64 -w0 release.keystore`), `ANDROID_KEYSTORE_PASSWORD`, `ANDROID_KEY_ALIAS` e, se diferente, `ANDROID_KEY_PASSWORD`.
Com os secrets, o workflow também gera `Teclado-Umbundu-release.apk`.

## Desenvolvimento local
```
npm install
npm run dev          # navegador
npm run build && npx cap add android && npx cap sync android   # projeto Android (requer Android Studio/JDK 21)
```

## O que muda no APK
- Sem service worker/botão "instalar" (o app já é nativo).
- "Copiar tudo" usa a área de transferência nativa; "Baixar .txt" abre o menu Compartilhar do Android.
- Nome/ID: `Teclado de Umbundu` / `app.tecladoumbundu.qwerty` (em `capacitor.config.json`).
