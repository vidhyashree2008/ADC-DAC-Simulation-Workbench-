# 
import java.util.Scanner;

public class ADCDACSimulation {

    static int adcConvert(double voltage, int bits, double vref) {
        int maxDigital = (1 << bits) - 1;

        if (voltage < 0 || voltage > vref) {
            throw new IllegalArgumentException(
                "Voltage must be between 0 and " + vref + " V."
            );
        }

        return (int) Math.round((voltage / vref) * maxDigital);
    }

    static double dacConvert(int digital, int bits, double vref) {
        int maxDigital = (1 << bits) - 1;

        if (digital < 0 || digital > maxDigital) {
            throw new IllegalArgumentException(
                "Digital value must be between 0 and " + maxDigital + "."
            );
        }

        return ((double) digital / maxDigital) * vref;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int bits = 8;
        double vref = 5.0;

        System.out.println("================================");
        System.out.println(" ADC & DAC SIMULATION WORKBENCH");
        System.out.println("================================");
        System.out.println("Resolution: " + bits + "-bit");
        System.out.println("Reference Voltage: " + vref + " V");

        System.out.print("\nEnter analog input voltage (0-5 V): ");
        double voltage = sc.nextDouble();

        try {
            int digital = adcConvert(voltage, bits, vref);
            double reconstructed = dacConvert(digital, bits, vref);

            System.out.println("\n--- ADC OUTPUT ---");
            System.out.println("Analog Input   : " + voltage + " V");
            System.out.println("Digital Output : " + digital);
            System.out.println("Binary Output  : "
                    + String.format("%8s",
                    Integer.toBinaryString(digital)).replace(' ', '0'));

            System.out.println("\n--- DAC OUTPUT ---");
            System.out.printf("Reconstructed Voltage: %.4f V%n",
                    reconstructed);
            System.out.printf("Conversion Error     : %.4f V%n",
                    Math.abs(voltage - reconstructed));

        } catch (IllegalArgumentException e) {
            System.out.println("Error: " + e.getMessage());
        }

        sc.close();
    }
}
ADC-DAC-Simulation-Workbench-
ADC &amp; DAC Simulation Workbench for understanding analog-to-digital and digital-to-analog conversion, sampling, quantization, and signal reconstruction.
