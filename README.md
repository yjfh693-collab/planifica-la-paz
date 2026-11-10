# Planifica La Paz — Simulador financiero con GCP

Aplicación web académica para simular la distribución de recursos municipales entre cuatro áreas: mantenimiento vial, alumbrado público, gestión de residuos y áreas verdes. El proyecto compara Gradientes Conjugados (GC) y Gradientes Conjugados Precondicionados (GCP) con precondicionador de Jacobi.

> **Aviso:** los valores son sintéticos y tienen finalidad educativa. No representan el presupuesto oficial ni datos publicados por el Gobierno Autónomo Municipal de La Paz.

## Abrir la aplicación

La entrada del proyecto es `index.html`. Al abrirla con conexión a internet, carga y reconstruye la aplicación a partir de los fragmentos comprimidos ubicados en `src/`. Para que funcione correctamente, conserva los tres archivos de esa carpeta.

## Ejecutar y usar

1. Abre el repositorio y entra a `index.html`.
2. Selecciona uno de los tres escenarios o modifica los coeficientes de la matriz `A` y el vector `b`.
3. Ejecuta el cálculo y revisa la solución de referencia, GC, GCP, residuos, errores y diagnósticos.

## Modelo matemático

Se resuelve un sistema `A x = b`, con cuatro incógnitas financieras. La matriz de cada escenario debe ser cuadrada, simétrica y definida positiva.

- **Ideal:** condiciones estables y matriz bien condicionada.
- **Bajo estrés:** representa perturbaciones financieras en los requerimientos del modelo.
- **Mal condicionado:** utiliza escalas diagonales muy diferentes para estudiar la sensibilidad numérica y el efecto del precondicionador Jacobi.

La solución de referencia se obtiene mediante eliminación de Gauss con pivoteo. Se comparan GC y GCP con tolerancia relativa `1e-6`. Se muestran errores absolutos, relativos y porcentuales por variable, residuo relativo y estimaciones de los números de condición.

## Estructura

- `index.html`: punto de entrada de la aplicación.
- `src/index.part1.b64`, `src/index.part2.b64`, `src/index.part3.b64`: fragmentos del código HTML comprimido que reconstruyen el simulador en el navegador.

La aplicación no utiliza backend ni paquetes externos. El navegador debe permitir `fetch` y `DecompressionStream` (disponible en navegadores modernos).

## Pruebas QA incluidas

1. Carga y ejecución de los tres escenarios.
2. Rechazo de matrices no válidas (no simétricas o no definidas positivas).
3. Recálculo tras editar los coeficientes.
4. Comparación de iteraciones de GC y GCP en el escenario mal condicionado.

## Referencias

- Suñagua S., P. (2020). *Método de Gradientes Conjugados Precondicionado*. Revista Boliviana de Matemática – UMSA, 04, 2–7.
- Golub, G. H., & Van Loan, C. F. (2013). *Matrix Computations* (4th ed.). Johns Hopkins University Press.
- Saad, Y. (2003). *Iterative Methods for Sparse Linear Systems* (2nd ed.). SIAM.
