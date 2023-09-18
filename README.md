# produccion 
produccion y gestion de la empresa Ramo 
package proyectoingsoft1;
import java.util.Scanner;

public class Proyectoingsoft1 {

    // Arrays para almacenar nombres y precios de productos
    private static final String[] bebidas = {"Avena", "Yogurt", "Agua", "Gaseosas", "Orchata", "Masato", "Arroz de leche"};
    private static final double[] preciosBebidas = {2500, 3000, 2200, 2500, 4500, 2000, 3000};

    private static final String[] comidas = {"Pan coco", "Pastel de pollo", "Galleta de avena", "Galletas dulces", "Pan de yuca", "Pan de bono", "Almohabana", "Arepa de maiz", "Pan hojaldrado", "Pan rollito", "Corazones"};
    private static final double[] preciosComidas = {400, 2500, 1000, 1000, 2200, 2000, 2500, 2500, 3500, 400, 1500};

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int opcion;

        do {
            System.out.println("Bienvenido a la Panadería software");
            System.out.println("1. Bebidas y precios");
            System.out.println("2. Comidas y precios");
            System.out.println("3. Realizar pedido");
            System.out.println("4. Salir");
            System.out.print("Por favor, seleccione una opción: ");

            opcion = scanner.nextInt();

            switch (opcion) {
                case 1:
                    mostrarProductos(bebidas, preciosBebidas, "Bebidas personales disponibles:");
                    break;
                case 2:
                    mostrarProductos(comidas, preciosComidas, "Comidas disponibles:");
                    break;
                case 3:
                    realizarPedido(scanner);
                    break;
                case 4:
                    System.out.println("Gracias por visitar la Panadería. ¡Hasta luego!");
                    break;
                default:
                    System.out.println("Opción no válida. Por favor, seleccione una opción válida.");
                    break;
            }
        } while (opcion != 4);

        scanner.close();
    }

    public static void mostrarProductos(String[] productos, double[] precios, String mensaje) {
        System.out.println(mensaje);
        for (int i = 0; i < productos.length; i++) {
            System.out.println((i + 1) + ". " + productos[i] + " - $" + precios[i]);
        }
    }

    public static void realizarPedido(Scanner scanner) {
        // Crear variables para rastrear los productos seleccionados y el total del pedido
        double totalPedido = 0;
        StringBuilder resumenPedido = new StringBuilder();

        System.out.println("Realizar Pedido:");
        System.out.println("Seleccione el tipo de producto:");
        System.out.println("1. Bebidas");
        System.out.println("2. Comidas");
        System.out.println("3. Volver al menú principal");
        System.out.print("Por favor, seleccione una opción: ");

        int opcionProducto = scanner.nextInt();

        while (opcionProducto != 3) {
            String[] productos;
            double[] precios;
            String mensaje;

            if (opcionProducto == 1) {
                productos = bebidas;
                precios = preciosBebidas;
                mensaje = "Bebidas disponibles:";
            } else if (opcionProducto == 2) {
                productos = comidas;
                precios = preciosComidas;
                mensaje = "Comidas disponibles:";
            } else {
                System.out.println("Opción no válida. Por favor, seleccione una opción válida.");
                continue;
            }

            mostrarProductos(productos, precios, mensaje);

            System.out.print("Seleccione el número del producto que desea comprar (0 para volver atrás): ");
            int numeroProducto = scanner.nextInt();

            if (numeroProducto >= 1 && numeroProducto <= productos.length) {
                System.out.print("Ingrese la cantidad que desea comprar: ");
                int cantidad = scanner.nextInt();
                if (cantidad > 0) {
                    double precioUnitario = precios[numeroProducto - 1];
                    double costoProducto = precioUnitario * cantidad;
                    totalPedido += costoProducto;
                    resumenPedido.append(productos[numeroProducto - 1]).append(": ").append(cantidad).append(" x $").append(precioUnitario).append(" = $").append(costoProducto).append("\n");
                    System.out.println("Producto agregado al pedido.");
                } else {
                    System.out.println("Cantidad no válida. Debe ser mayor que cero.");
                }
            } else if (numeroProducto != 0) {
                System.out.println("Número de producto no válido. Intente nuevamente.");
            }

            System.out.println("Total del pedido: $" + totalPedido);

            System.out.println("Seleccione el tipo de producto:");
            System.out.println("1. Bebidas");
            System.out.println("2. Comidas");
            System.out.println("3. Volver al menú principal");
            System.out.print("Por favor, seleccione una opción: ");
            opcionProducto = scanner.nextInt();
        }

        if (resumenPedido.length() > 0) {
            System.out.println("Resumen del pedido:");
            System.out.println(resumenPedido.toString());
            System.out.println("Total a pagar: $" + totalPedido);
        } else {
            System.out.println("No se han agregado productos al pedido.");
        }
    }
}
