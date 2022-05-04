# configuracion dentro de nuestro proyecto de android

## generando las credenciales

nesecitamos decirle a nuestro proyecto de firebase las credenciales de la app para que nos de acceso a nuestra app

### configurando la app en firebase

1. en la consola de firebase picamos sobre nuestro proyecto respectivo , deberiamos estar en dashboard
2. en la pantalla inicial veras un icono de android, junto a una breve texto indicando `comienza por agreagar Firebase a tu app`, es posible que el dashboar cambie.
3. nos pedira los siguiente

- nombre del paquete android
- este se encuentra en el manifiesto de la app, la ruta es la siguiente `/android/app/src/main/AndroidManifest.xml`, justo en la primera etiqueta encontramos la proipiedad package donde estara el nombre

```xml
<manifest xmlns:android="http://schemas.android.com/apk/res/android"

package="com.firebasesteps">

  <uses-permission android:name="android.permission.INTERNET" />

...
</manifest>
```

- sobrenombre : opcional
- certificado SHA : opcional, recomendable
- para obtener este certificado debes hacer lo siguiente abrir un terminal en la ruta `/android` una vez hay ejecuta

```Shell
~$ ./gradlew signinReport
```

obtendras un informe como este

```filenames
  Variant: debug
  Config: debug
  Store: /home/adriel/Documentos/proyectos/react-native-firebase/firebasesteps/android/app/debug.keystore
  Alias: androiddebugkey
  MD5: 20:F4:61:48:B7:2D:8E:5E:5C:A2:3D:37:A4:F4:14:90
  SHA1: 5E:8F:16:06:2E:A3:CD:2C:4A:0D:54:78:76:BA:A6:F3:8C:AB:F6:25
  SHA-256: FA:C6:17:45:DC:09:03:78:6F:B9:ED:E6:2A:96:2B:39:9F:73:48:F0:BB:6F:89:9B:83:32:66:75:91:03:3B:9C
  Valid until: martes, 30 de abril de 2052
```

puedes incluir las claves SHA1 y256 a tu proyecto en firebase

4. si todo va bien en firebase el siguiente punto debe ser descarga una manifiesto en formato json de `google-services` descargalo y colocalo dentro de la siguiente ruta `android/app/src` , tienes una foto en la web
5. ahora tenemos que modificar los siguientes archivos

- `<project>/build.gradle`

```Gradle
buildscript {

 repositories {

   // Check that you have the following line (if not, add it):

   google()  // Google's Maven repository

 }

 dependencies {

   ...

   // Add this line

   classpath 'com.google.gms:google-services:4.3.10'

 }

}


allprojects {

 ...

 repositories {

   // Check that you have the following line (if not, add it):

   google()  // Google's Maven repository

   ...

 }

}
```

- el siguiente es `<project>/<app-module>/build.gradle`

```Gradle

apply plugin: 'com.android.application'

// Add this line

apply plugin: 'com.google.gms.google-services'


dependencies {

  // Import the Firebase BoM

  implementation platform('com.google.firebase:firebase-bom:29.3.1')


  // Add the dependency for the Firebase SDK for Google Analytics

  // When using the BoM, don't specify versions in Firebase dependencies

  implementation 'com.google.firebase:firebase-analytics'


  // Add the dependencies for any other desired Firebase products

  // https://firebase.google.com/docs/android/setup#available-libraries

}


```

6. una finalizada la configuracion debemos hacer un rebuild de la app

```Shell
npx react-native run-android
```

## seguimos con [Analitic](./analitics.md) o volvemos al [indice](./home.md)
