# MultiEnv Browser

Navegador Android (Kotlin + Jetpack Compose) com perfis de navegação isolados.

## Build
- Local: abra no Android Studio (Ladybug+) e rode `app`, ou `gradle assembleDebug` (Gradle 8.9, JDK 17).
- CI: `.github/workflows/android.yml` gera o APK debug como artefato a cada push.

## Requisitos
- Android 8.0+ (minSdk 26) e Android System WebView 124+ (necessário para perfis isolados).

## Isolamento de sessão
`WebView.setDataDirectorySuffix()` só pode ser chamado uma vez por processo, antes do primeiro WebView,
então não permite alternar perfis em tempo de execução. O app usa a Profile API oficial do AndroidX
(`ProfileStore` + `WebViewCompat.setProfile`), que separa cookies, cache, localStorage e IndexedDB por perfil
no mesmo processo. Sem suporte, o app recusa criar WebViews (nunca navega sem isolamento).
