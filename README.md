# Documentación de Become iOS SDK
Este es un espacio para conocer a cerca de la app Become para validación biométrica de identidad en el sistema iOS.

## Configuraciones de Xcode
### Instalación de Become

Instale Become (Su archivo de pod de aplicación)
  
    pod 'Become-YYYYY-ID-SDK'
    
Ejecutar el pod desde la terminal

    pod install

## Inicialización de Become KYC

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
Los siguientes parámetros son necesarios para la activación de la SDK por lo tanto su valor no debe ser vacío.
 
Parámetro | Valor
------------ | -------------
clientId | ""
clientSecret | ""

Mostrará el siguiente error por consola:

    clientIdL or clientIdL parameters cannot be empty

**2. Video cómo único parámetro**
El atributo ***validationTypes*** no puede contener como único valor el parámetro ***VIDEO***

    validationTypes: "VIDEO"

Mostrará el siguiente error por consola:

    the process cannot be initialized with video only

## Validación del proceso
En este apartado encontrará la respuesta a partir de la validación del proceso realizado por la SDK:

	present(becomeIdentity, animated: true, completion:{
		BDIVVC.onDoneBlock = { result in
		print(result) //La SDK responde a partir de la validación del proceso
		}
	})

A continuación, las estructuras internas que contienen los atributos encargados de capturar la información dada por el usuario:

** 1. Estructura encargada de la definición para los estados de validación realizados por la SDK:**

	public struct BecomeDIVResponse { // 
		public enum responseStatus {
		case succes // Estado de proceso finalizado exitosamente
		case cancelled // Estado de proceso cancelado
		case error // Error interno de la SDK 
	}
	
**2. Estructura para el retorno de la información **
Los siguientes son los parámetros que permiten el retorno de la información capturada por el sistema.

		public var created_at: String?
		public var transactionId: String?
		public var identityStatus: String?
		public var documentNumber: String?
		public var dateOfBirth: String? 
		public var fullName: String?
		public var comply_advantage_result: String?
		public var comply_advantage_url: String?
		public var company: String?
		public var document_type: String?
		public var responseStatus: BecomeDigitalV.BecomeDIVResponse.responseStatus? // Retorna el estado de la validación ( succes | canceled | error )
		public var message: String? // Retorna mensaje a partir del responseStatus
		public var face_match: Bool?
		public var template: Bool?
		public var alteration: Bool?
		public var watch_list: Bool?
		
### Adicional: ¿Que sucede cuándo un usuario cancela el proceso?
La respuesta a esta pregunta se encuentra en el siguiente bloque de código, el cuál representa representa el objeto  ***BecomeDIVResponse*** con todos sus atributos vacíos:

		BecomeDIVResponse
		- created_at : nil
		- transactionId : nil
		- identityStatus : nil
		- documentNumber : nil
		- dateOfBirth : nil
		- fullName : nil
		- comply_advantage_result : nil
		- comply_advantage_url : nil
		- company : nil
		- document_type : nil

## Implementación del proceso
Esta sección se encarga de proporcionar los pasos para la implementación final del proceso.

**1.** Llenar los parámetros ***clientId*** , ***clientSecret*** y ***validationTypes*** con los valores proporcionados en la compra del producto.

	Ejemplo:
		clientId: "gergregg",
		clientSecret: "KMBR4CLX6APSZ85EIFVY95HUT3DG1QNJ",
		contractId: "3",
		validationTypes: "PASSPORT|DNI|LICENSE|VIDEO"
		
**2.** Colocar el logo de su preferencia dando valor a la variable ***customerLogo***
	
	Ejemplo:
		customerLogo: UIImage(named: "icon")!)

**3.** Definir el tipo de visualización de la modal

	Ejemplo:
		becomeIdentity.modalPresentationStyle = .fullScreen	
	
**4.** Debe crear un objeto de nombre ***resultFinal*** e igualarlo a ***BecomeDIVResponse*** esto con el fin de codificar el acceso a todos los parámetros que retorna la SDK.

	let resultFinal = result as! BecomeDIVResponse

**5.** El siguiente bloque de código permite visualizar los pasos unificados para la implementación final:

	@IBAction func start(_ sender: Any) {
				let becomeIdentity = BDIVVC(
						clientId: "gergregg",
						clientSecret: "KMBR4CLX6APSZ85EIFVY95HUT3DG1QNJ",
						contractId: "3",
						validationTypes: "PASSPORT|DNI|LICENSE|VIDEO",
						allowLibraryLoading: true,
						customerLogo: UIImage(named: "icon")!) 
		becomeIdentity.modalPresentationStyle = .fullScreen
		  present(becomeIdentity, animated: true, completion:{
		        BDIVVC.onDoneBlock = { result in
					  //Objeto final de la respuesta para obter todos los parametros retornados por la SDK
            let resultFinal = result as! BecomeDIVResponse.
            print(result)
			}
		}) 
	}


## Requerimientos

* **Tecnologias**
	
	iOS 9.0
  
	Xcode 10.2
  
	Swift 5.0
	
* Requiere del uso de **Alamofire**, es importante construir la siguiente estructura de archivos como se muestra a continuación:

![](C:\Users\User\Desktop\Celular.png)


## Vídeo de integración del SDK Become para iOS
