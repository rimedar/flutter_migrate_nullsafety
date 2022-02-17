

# Migrar flutter de 1.22.6 a 2.8.1 y 2.10.0

## Flutter 2.8.1 Instalado

### Proyecto en flutter 1.22.6

* Verificar los paquetes que tienen compatibilidad con null safety 
> en la consola correr --> dart pub outdated --    mode=null-safety
* Aplicar flutter fix
 >en la consola correr --> dart fix --dry-run para ver los cambios disponibles
 en la consola correr --> dart fix --apply para aplicar todos los cambios

* Actualizar los paquetes a null safety
* > dart pub upgrade --null-safety

* Quitar todas las importaciones a paquetes que no se esten usando
* Migrar el proyecto
>En la consola Correr --> dart migrate 
  Si no se genera ningun error, verificar los cambios que se van a aplicar en el monitor web y aplicar los cambios.
  
* En android/build.gradle actualizar lo siguiente:
  >Actualizar la version del pugin de kotlin --> ext.kotlin_version = '1.6.10' 
  Actualizar la version del pugin de grade --> 'com.android.tools.build:gradle:4.1.0'

* En android/app/build.gradle actualizar lo siguiente
 > --compileSdkVersion 31
  --minSdkVersion 21
  -targetSdkVersion 31

* En android/gradle/gradle-wrapper.properties actualizar lo siguiente
 > distributionUrl=https\://services.gradle.org/distributions/gradle-6.5-all.zip

#### Con esto la app deberia correr en la version 2.8.1 de flutter, si ya has corregido todas las advertencias o errores de null safety en tu codigo.


# Actualizar a flutter 2.10.0

* Correr el comando Futter Upgrade
* Agragar la siguiente linea en el archivo android/app/src/main/AndroidManifest.xml
  >En todos los <activiti que contengan un <intent-filter
                                                          
  > --- <activity
            android:name=".MainActivity"
            android:launchMode="singleTop"
            android:theme="@style/LaunchTheme"
            **android:exported="true" --->>> Linea nueva**

  > --- Si aun no tenias habilitado el embedding 2, deberas poner estas lineas debajo del activity
   ---</activity>
        <meta-data
            android:name="flutterEmbedding"
            android:value="2" />
--Mofificar esta linea --> android:name="io.flutter.app.FlutterApplication" por esta android:name="${applicationName}"
-- Si sale algun error, seguir los pasos descritos en el **link 1**

* Para crear la carpeta windows en el proyecto migrado de flutter 2.8.1  corren el comando **flutter create .** estando en la version 2.10.0

* Actualiza la version minima del sdk en el archivo pubspec.yaml a 
   sdk: '>=2.16.0 <3.0.0'
* Agrega flutter_lints: ^1.0.0 en dev_dependencies para ver las correcciones de codigo mas recientres.
* Nuevamente Aplicar flutter fix
 >en la consola correr --> dart fix --dry-run para ver los cambios disponibles
 -en la consola correr --> dart fix --apply para aplicar todos los cambios

### Listo, puedes ejecutar tu proyecto.

##### Esos son todos los pasos que yo segui para poder migrar mis aplicaciones de flutter 1.22.6 a flutter 2.10.0

ref link 1
https://github.com/flutter/flutter/wiki/Upgrading-pre-1.12-Android-projects
