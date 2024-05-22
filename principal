package convertidor;

import org.json.JSONObject;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.net.HttpURLConnection;
import java.net.URL;
import java.util.Scanner;
import java.util.logging.Level;
import java.util.logging.Logger;

public class Principal {

    private static final Logger LOGGER = Logger.getLogger(Principal.class.getName());

    public static void main(String[] args) {
        System.out.println("1 - Dolar");
        System.out.println("2 - Peso Argentino");
        System.out.println("3 - Real Brasileño");
        System.out.println("4 - Peso Colombiano");
        System.out.println("5 - Peso Chileno");

        Scanner cv = new Scanner(System.in);

        int eleccion = cv.nextInt();
        System.out.println("Introduzca el valor a convertir");
        double cantidad = cv.nextDouble();

        // Obtener tasas de cambio
        JSONObject rates = obtenerTasasDeCambio();

        // Convertir monedas
        switch (eleccion) {
            case 1:
                convertirMoneda(cantidad, "USD", rates);
                break;
            case 2:
                convertirMoneda(cantidad, "ARS", rates);
                break;
            case 3:
                convertirMoneda(cantidad, "BRL", rates);
                break;
            case 4:
                convertirMoneda(cantidad, "COP", rates);
                break;
            case 5:
                convertirMoneda(cantidad, "CLP", rates);
                break;
            default:
                System.out.println("Elección inválida");
        }
    }

    private static JSONObject obtenerTasasDeCambio() {
        try {
            URL url = new URL("https://api.exchangerate-api.com/v4/latest/USD");
            HttpURLConnection con = (HttpURLConnection) url.openConnection();
            con.setRequestMethod("GET");

            BufferedReader in = new BufferedReader(new InputStreamReader(con.getInputStream()));
            StringBuilder response = new StringBuilder();
            String inputLine;

            while ((inputLine = in.readLine()) != null) {
                response.append(inputLine);
            }
            in.close();

            return parseJsonResponse(response.toString());
        } catch (IOException e) {
            LOGGER.log(Level.SEVERE, "Error al obtener las tasas de cambio", e);
            return null;
        }
    }

    private static JSONObject parseJsonResponse(String response) {
        return new JSONObject(response).getJSONObject("rates");
    }

    private static void convertirMoneda(double cantidad, String monedaDestino, JSONObject rates) {
        if (rates != null) {
            double tasa = rates.getDouble(monedaDestino);
            double resultado = cantidad * tasa;
            System.out.println(cantidad + " USD equivale a " + resultado + " " + monedaDestino);
        } else {
            System.out.println("No se pudo obtener la tasa de cambio.");
        }
    }
}





