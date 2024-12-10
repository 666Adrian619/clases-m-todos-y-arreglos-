# clases-m-todos-y-arreglos-
clases, métodos, y arreglos  en java

public class Empleado {

    // Variables de instancia
    private int id_empleado;
    private String nombre_empleado;
    private String puesto;
    private double[] sueldo_quincenal;

    // Constructor de la clase
    public Empleado(int id_empleado, String nombre_empleado, String puesto) {
        // Validar datos antes de asignar
        if (validarDatos(id_empleado, nombre_empleado, puesto)) {
            this.id_empleado = id_empleado;
            this.nombre_empleado = nombre_empleado;
            this.puesto = puesto;
            this.sueldo_quincenal = new double[2];  // Asignamos tamaño 2 para almacenar los salarios quincenales
        } else {
            System.out.println("Datos incorrectos.");
        }
    }

    // Método para validar los datos de entrada
    private boolean validarDatos(int id_empleado, String nombre_empleado, String puesto) {
        if (id_empleado <= 0 || nombre_empleado == null || nombre_empleado.isEmpty()) {
            return false;
        }

        // Validamos si el puesto es "Empleado" o "Supervisor"
        return puesto.equals("Empleado") || puesto.equals("Supervisor");
    }

    // Método para calcular el sueldo
    public void calcularSueldo(double horasExtrasDiurnas, double horasExtrasNocturnas) {
        if (puesto.equals("Empleado")) {
            // Sueldo base del empleado
            double sueldoBase = 5000;

            // Cálculo de horas extras
            double pagoHorasExtras = (horasExtrasDiurnas * 50) + (horasExtrasNocturnas * 60);

            // Sueldo total del empleado
            sueldo_quincenal[0] = sueldoBase + pagoHorasExtras;
            System.out.println("Sueldo total de " + nombre_empleado + " (Empleado): $" + sueldo_quincenal[0]);
        } else if (puesto.equals("Supervisor")) {
            // Sueldo base del supervisor
            double sueldoBase = 8000;

            // Deducciones
            double infonavit = sueldoBase * 0.002;  // 0.2% de INFONAVIT
            double seguroMedico = sueldoBase * 0.001; // 0.1% de Seguro Médico
            double isr = sueldoBase * 0.0016;  // 0.16% de ISR

            // Sueldo total después de deducciones
            sueldo_quincenal[1] = sueldoBase - infonavit - seguroMedico - isr;
            System.out.println("Sueldo total de " + nombre_empleado + " (Supervisor): $" + sueldo_quincenal[1]);
        } else {
            System.out.println("Puesto no reconocido");
        }
    }

    // Métodos getter para obtener los salarios
    public double getSueldoEmpleado() {
        return sueldo_quincenal[0];
    }

    public double getSueldoSupervisor() {
        return sueldo_quincenal[1];
    }
    
    // Método para obtener información del empleado
    public void mostrarInfoEmpleado() {
        System.out.println("ID: " + id_empleado);
        System.out.println("Nombre: " + nombre_empleado);
        System.out.println("Puesto: " + puesto);
    }

    // Método principal para probar la clase
    public static void main(String[] args) {
        // Crear un objeto Empleado
        Empleado empleado1 = new Empleado(12345, "Juan Pérez", "Empleado");
        empleado1.calcularSueldo(10, 5); // 10 horas extras diurnas y 5 nocturnas

        // Crear un objeto Supervisor
        Empleado supervisor1 = new Empleado(67890, "Ana Gómez", "Supervisor");
        supervisor1.calcularSueldo(0, 0); // Sin horas extras para el supervisor
    }
}
