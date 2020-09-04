# Documentación de Become iOS SDK
Este es un espacio para conocer a cerca de la app Become para validación biométrica de identidad en el sistema iOS.

## Configuraciones de Xcode
### Instalación de Become

Instale Become (Su archivo de pod de aplicación)
  
    pod 'Become-YYYYY-ID-SDK'
    
Ejecutar el pod desde la terminal

    pod install

## BecomeDelegate - Inicialización de Become KYC

Realice los siguientes cambios en su archivo BecomeDelegate

### Swift
    
    import BecomeDigitalV 

         let becomeIdentity = BDIVVC(clientId: "acc_demo_555", //El valor de este parámetro debe ser solicitado al contratar el servicio
                                    clientSecret: "KMBR4CLX6APSZ865465EIFVY95HUT3DG1QNJ",//El valor de este parámetro debe ser solicitado al contratar el servicio
                                    contractId: "3",
                                    validationTypes: "PASSPORT|DNI|LICENSE|VIDEO",
                                    allowLibraryLoading: true,
                                    customerLogo: UIImage(named: "icon")!)
 ## Errores en parámetros
 
 **1. Error con parámetros vacíos**
  
Parámetro | Valor
------------ | -------------
clientId | ""
clientSecret | ""

Mostrará el siguiente error por consola:

    clientIdL or clientIdL parameters cannot be empty

**2. Video cómo único parámetro**
El atributo validationTypes no puede contener como único valor el parámetro VIDEO

    validationTypes: "VIDEO"

Mostrará el siguiente error por consola:

    the process cannot be initialized with video only
    
| WARNING: be careful to baz the quux before initializing the retro encabulator! |
| --- |
