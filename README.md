import java.util.ArrayList;
import java.util.Scanner;

public class GestionInventarioZapatos {
    public static void main(String[] args) {
        ArrayList<Producto> inventario = new ArrayList<>();
        Scanner scanner = new Scanner(System.in);

        while (true) {
            System.out.println("\n--- Gestión de Inventario de Zapatos ---");
            System.out.println("1. Agregar producto");
            System.out.println("2. Vender producto");
            System.out.println("3. Duplicar inventario");
            System.out.println("4. Mostrar inventario");
            System.out.println("5. Salir");
            System.out.print("Seleccione una opción: ");

            int opcion = scanner.nextInt();
            scanner.nextLine(); // Consumir la nueva línea

            switch (opcion) {
                case 1:
                    System.out.print("Nombre del producto: ");
                    String nombre = scanner.nextLine();
                    System.out.print("Cantidad inicial: ");
                    int cantidadInicial = scanner.nextInt();
                    inventario.add(new Producto(nombre, cantidadInicial));
                    System.out.println("Producto agregado al inventario.");
                    break;
                case 2:
                    System.out.print("Nombre del producto a vender: ");
                    String nombreVenta = scanner.nextLine();
                    Producto productoVenta = buscarProducto(inventario, nombreVenta);
                    if (productoVenta != null) {
                        System.out.print("Unidades a vender: ");
                        int unidadesVenta = scanner.nextInt();
                        productoVenta.vender(unidadesVenta);
                    } else {
                        System.out.println("Producto no encontrado.");
                    }
                    break;
                case 3:
                    System.out.print("Nombre del producto para duplicar inventario: ");
                    String nombreDuplicar = scanner.nextLine();
                    Producto productoDuplicar = buscarProducto(inventario, nombreDuplicar);
                    if (productoDuplicar != null) {
                        productoDuplicar.duplicarInventario();
                    } else {
                        System.out.println("Producto no encontrado.");
                    }
                    break;
                case 4:
                    System.out.println("\n--- Inventario Actual ---");
                    for (Producto producto : inventario) {
                        producto.mostrarInformacion();
                        System.out.println("---");
                    }
                    break;
                case 5:
                    System.out.println("Saliendo del programa...");
                    scanner.close();
                    System.exit(0);
                default:
                    System.out.println("Opción no válida.");
            }
        }
    }

    private static Producto buscarProducto(ArrayList<Producto> inventario, String nombre) {
        for (Producto producto : inventario) {
            if (producto.nombre.equalsIgnoreCase(nombre)) {
                return producto;
            }
        }
        return null;
    }
}

class Producto { // Corrected: class Producto (no longer public)
    String nombre;
    int cantidadInicial;
    int cantidadActual;

    public Producto(String nombre, int cantidadInicial) {
        this.nombre = nombre;
        this.cantidadInicial = cantidadInicial;
        this.cantidadActual = cantidadInicial;
    }

    public void vender(int unidadesVendidas) {
        if (cantidadActual >= unidadesVendidas) {
            cantidadActual -= unidadesVendidas;
            System.out.println("Venta realizada con éxito.");
        } else {
            System.out.println("No hay suficiente stock disponible.");
        }
    }

    public void duplicarInventario() {
        cantidadActual = cantidadInicial * 2;
        System.out.println("Inventario duplicado.");
    }

    public void mostrarInformacion() {
        System.out.println("Producto: " + nombre);
        System.out.println("Cantidad inicial: " + cantidadInicial);
        System.out.println("Cantidad actual: " + cantidadActual);
    }
}
