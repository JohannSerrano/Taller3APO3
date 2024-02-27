```
package umariana.taller3;
//Sergio Morillo y Johan Serrano
import java.text.SimpleDateFormat;
import java.util.ArrayList;
import java.util.Date;
import java.util.Scanner;
import mundo.Entrada;

public class Taller3 {
    private ArrayList<Entrada> misEntradas;
    private Scanner lector;

    public Taller3() {
        misEntradas = new ArrayList<>();
        lector = new Scanner(System.in);
    }

    public void mostrarMenu() {
        boolean activo = true;
        do {
            System.out.println("_____ MENU DE OPCIONES _____\n"
                    + "1.Agregar una Entrada\n"
                    + "2.Consultar Entrada\n"
                    + "3.Modificar una Descripcion\n"
                    + "4.Eliminar una Entrada\n"
                    + "5.Salir\n");

            System.out.print("Seleccione una opción: ");
            int opcion = lector.nextInt();
            lector.nextLine(); // Consumir el salto de línea restante

            switch (opcion) {
                case 1:
                    agregarEntrada();
                    break;

                case 2:
                    consultarEntrada();
                    break;

                case 3:
                    modificarEntrada();
                    break;

                case 4:
                    eliminarEntrada();
                    break;

                case 5:
                    activo = false;
                    System.out.println("Programa terminado");
                    break;

                default:
                    System.out.println("Opción no válida, inténtelo nuevamente");
            }
        } while (activo);
    }

    private void agregarEntrada() {
        System.out.print("Ingrese la Descripcion: ");
        String descripcion = lector.nextLine();
        System.out.println("===========================================");

           int nuevoIdEntrada = misEntradas.size() + 1;


        Date fechaActual = new Date();
        SimpleDateFormat formatoFecha = new SimpleDateFormat("dd-MM-yyyy");
        String fecha = formatoFecha.format(fechaActual);

        Entrada nuevaEntrada = new Entrada(nuevoIdEntrada, fecha, descripcion);
        misEntradas.add(nuevaEntrada);

        System.out.println("La Entrada ha sido agregada con éxito!");
    }

    private void consultarEntrada() {
    System.out.print("Ingrese la fecha de la Entrada que desea consultar (dd-MM-yyyy): ");
    String fechaBuscada = lector.nextLine(); // El usuario ingresa la fecha

    // Verificar si hay entradas en esa fecha

    for (Entrada entrada : misEntradas) {
        if (entrada.getFecha().equals(fechaBuscada)) {
            // Se encontró al menos una entrada con la fecha especificada

            System.out.println("ID: " + entrada.getIdEntrada() + " | Fecha: " + entrada.getFecha() + " | Descripción: " + entrada.getDescripcion());
            System.out.println("-------------------");
        }else{
            System.out.println("No se encontro la fecha de la Entrada");
        }
    }
    }



    private void modificarEntrada() {
        System.out.print("Ingrese el ID de la Entrada que desea modificar: ");
        int idEntradaModificar = lector.nextInt();
        lector.nextLine(); // Consumir el salto de línea

        for (Entrada entrada : misEntradas) {
            if (entrada.getIdEntrada() == idEntradaModificar) {
                System.out.print("Ingrese la nueva Descripcion: ");
                entrada.setDescripcion(lector.nextLine());
                System.out.println("La Descripcion ha sido modificada con éxito.");
                return;
            }
        }

        System.out.println("No se encontró ninguna Entrada con el ID ");
    }

    private void eliminarEntrada() {
       System.out.println("Ingre el id del producto a eliminar");
       int id =lector.nextInt();
       for(Entrada e: misEntradas){
           if(e.getIdEntrada()==id){
               System.out.println("Seguro que quieres eliminar?\n1 SI\n2 NO");
               int opcion = lector.nextInt();
               if(opcion==1){
               misEntradas.remove(e);
               System.out.println("Entrada removido satisfactoriamente");
               }else if(opcion==2){
                   System.out.println("Se cancelo eliminar Entrada");
               }else if(opcion!=1 && opcion!=2){
                   System.out.println("No se encontro la opcion vuelves al inicio");
               }
               break;
           }else {
               System.out.println("no se encontro ningun producto");
           }
           
       }
    }

    public static void main(String[] args) {
        Taller3 diario = new Taller3();
        diario.mostrarMenu();
    }
}

// Suposición de implementación de la clase Entrada en el paquete mundo

```
