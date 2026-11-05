# Directorio Dolorense (API Node + app Flutter)

## 1. API (la "cocina")
    cd api
    node server.js            # http://localhost:3000/negocios
    curl localhost:3000/salud

## 2. App Flutter
Este zip trae SOLO lib/, test/ y pubspec.yaml. Genera primero las carpetas de plataforma:

    flutter create app --project-name directorio_dolores     # en la carpeta directorio_dolores/
    # (si ya descomprimiste, haz el create en otra carpeta y copia android/ ios/ etc. a app/)
    cd app
    rm -f test/widget_test.dart
    flutter pub get
    flutter test             # 15 pruebas, sin red

Luego copia lib/, test/ y pubspec.yaml de este proyecto sobre los generados (reemplazando).

### Android: permitir HTTP (solo desarrollo)
En android/app/src/main/AndroidManifest.xml:
  - arriba de <application>:  <uses-permission android:name="android.permission.INTERNET"/>
  - en <application ...>:     android:usesCleartextTraffic="true"

### iOS (Mac): en ios/Runner/Info.plist
    <key>NSAppTransportSecurity</key>
    <dict><key>NSAllowsLocalNetworking</key><true/></dict>

## 3. Ejecutar
    Terminal 1 (api/):  node server.js
    Terminal 2 (app/):  flutter run                                   # emulador Android -> 10.0.2.2
                        flutter run --dart-define=API_URL=http://TU-IP:3000   # celular real
