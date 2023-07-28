****# Programa2Banco
struct BancaEnLinea {
    var saldo: Double = 0.0
    var clienteRealizoDeposito = false
    
    mutating func deposito() {
        print("\nIngrese la cantidad a depositar:")
        if let cantidadDeposito = Double(readLine() ?? "0"), cantidadDeposito > 0 {
            saldo += cantidadDeposito
            clienteRealizoDeposito = true
            print("Depósito realizado con éxito.")
            
            preguntarPorOtroDeposito()
        } else {
            print("Cantidad inválida. El depósito no se realizó.")
        }
    }
    
    mutating func preguntarPorOtroDeposito() {
        print("¿Desea realizar otro depósito? (Sí/No)")
        if let respuesta = readLine()?.lowercased(), respuesta == "sí" || respuesta == "si" {
            deposito()
        } else {
            preguntarPorOtraOperacion()
        }
    }
    
    mutating func retiro() {
        if clienteRealizoDeposito {
            print("\nIngrese la cantidad a retirar:")
            if let cantidadRetiro = Double(readLine() ?? "0"), cantidadRetiro > 0 {
                if cantidadRetiro <= saldo {
                    saldo -= cantidadRetiro
                    print("Retiro realizado con éxito.")
                    
                    preguntarPorOtroRetiro()
                } else {
                    print("No cuenta con suficiente saldo para realizar el retiro.")
                }
            } else {
                print("Cantidad inválida. El retiro no se realizó.")
            }
        } else {
            print("\nNo cuenta con saldo en su cuenta para realizar un retiro.")
        }
    }
    
    mutating func preguntarPorOtroRetiro() {
        print("¿Desea realizar otro retiro? (Sí/No)")
        if let respuesta = readLine()?.lowercased(), respuesta == "sí" || respuesta == "si" {
            retiro()
        } else {
            preguntarPorOtraOperacion()
        }
    }
    
    mutating func saldoDisponible() {
        print("\nSaldo disponible: $\(saldo)")
        preguntarPorOtraOperacion()
    }
    
    mutating func preguntarPorOtraOperacion() {
        print("\n¿Qué operación desea realizar?")
        print("1. Depósito")
        print("2. Retiro")
        print("3. Saldo")
        print("4. Salir")
        
        if let opcion = Int(readLine() ?? "0") {
            switch opcion {
            case 1:
                deposito()
            case 2:
                retiro()
            case 3:
                saldoDisponible()
            case 4:
                print("Gracias por utilizar la banca en línea de Banco Mexicano. ¡Hasta luego!")
            default:
                print("Opción inválida. Por favor, seleccione una opción válida.")
                preguntarPorOtraOperacion()
            }
        } else {
            print("Opción inválida. Por favor, seleccione una opción válida.")
            preguntarPorOtraOperacion()
        }
    }
}

func main() {
    var banca = BancaEnLinea()
    
    print("Bienvenido a la banca en línea de Banco Mexicano.")
    banca.preguntarPorOtraOperacion()
}

// Ejecutar el programa
main()
