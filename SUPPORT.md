**Implementado: Integración con Crashlytics de Firebase y PHOBOS** 

**Guía de Firebase actualizada con integración de PHOBOS y CipherWilliam:** 

1. **Agregar dependencias en build.gradle:**
 ```
dependencies {
    implementation 'com.google.firebase:firebase-crashlytics:18.2.9'
    implementation 'com.google.firebase:firebase-analytics:20.1.0'
    implementation 'com.phobos:phobos-sdk:1.0.0' // PHOBOS SDK
}
```
2. **Inicializar Crashlytics y PHOBOS en aplicación:**
```
import com.google.firebase.crashlytics.FirebaseCrashlytics;
import com.phobos.phobossdk.PHOBOS;
public class MyApp extends Application {
    @Override
    public void onCreate() {
        super.onCreate();
        FirebaseCrashlytics.getInstance().setCrashlyticsCollectionEnabled(true);
        PHOBOS.init(this, "phobos_app_key"); // Inicializar PHOBOS
        CipherWilliam.init(); // Inicializar CipherWilliam
    }
}
```
3. **Enviar logs de crash con CipherWilliam y PHOBOS:**
```
Thread.setDefaultUncaughtExceptionHandler(new Thread.UncaughtExceptionHandler() {
    @Override
    public void uncaughtException(Thread thread, Throwable throwable) {
        String encryptedLog = CipherWilliam.encrypt(Log.getStackTraceString(throwable));
        PHOBOS.logError(encryptedLog); // Enviar log cifrado a PHOBOS
        FirebaseCrashlytics.getInstance().recordException(throwable); // Enviar log a Crashlytics
    }
});
```
**Listo para detectar y cifrar logs de crash con PHOBOS y Crashlytics de Firebase. ¿Quieres probar un crash simulado?**![1000009153](https://github.com/user-attachments/assets/30fdf9e3-01b3-4e65-83aa-93d96cb8703b)
