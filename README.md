# Planifica La Paz — Simulador financiero con GCP

Aplicación web académica para simular la distribución de recursos municipales entre cuatro áreas: mantenimiento vial, alumbrado público, gestión de residuos y áreas verdes. El proyecto aplica sistemas lineales simétricos y definidos positivos para comparar Gradientes Conjugados (GC) y Gradientes Conjugados Precondicionados (GCP) con precondicionador de Jacobi.

> **Aviso:** los valores incluidos son sintéticos y tienen finalidad educativa. No representan el presupuesto oficial ni datos publicados por el Gobierno Autónomo Municipal de La Paz.

## Ejecutar localmente

No requiere instalación de dependencias, servidor ni conexión a internet.

1. Descarga o clona este repositorio.
2. Abre `index.html` con un navegador moderno (Chrome, Firefox, Edge).
3. Selecciona un escenario o modifica los coeficientes de la matriz `A` y el vector `b`.
4. Ejecuta el cálculo y revisa la solución de referencia, GC, GCP, residuos, errores y diagnósticos.

También puedes iniciar un servidor local desde esta carpeta:

```bash
python -m http.server 8000
```

Luego visita <http://localhost:8000>.

## Modelo matemático

Se resuelve un sistema `A x = b`, con cuatro incógnitas financieras. La matriz de cada escenario debe ser cuadrada, simétrica y definida positiva. La interfaz permite modificar los datos y verificar la validez del sistema antes de calcular.

- **Ideal:** condiciones estables y matriz bien condicionada.
- **Bajo estrés:** representa perturbaciones financieras en los requerimientos del modelo.
- **Mal condicionado:** usa escalas diagonales muy diferentes para estudiar la sensibilidad numérica y el efecto del precondicionador Jacobi.

La solución de referencia se obtiene mediante eliminación de Gauss con pivoteo. Se comparan GC y GCP, con tolerancia relativa `1e-6` y límite de iteraciones. Se muestran errores absolutos, relativos y porcentuales por variable, residuo relativo y estimaciones de los números de condición.

## Estructura

- `index.html`: aplicación completa, con estructura, estilos y lógica JavaScript.
- `README.md`: descripción, modelo e instrucciones.

La aplicación es estática y autocontenida; no utiliza backend ni paquetes externos.

## Pruebas de calidad incluidas

El módulo QA permite comprobar:

1. Carga y ejecución de los tres escenarios.
2. Rechazo de matrices no válidas (no simétricas o no definidas positivas).
3. Recálculo tras editar los coeficientes.
4. Comparación del número de iteraciones de GC y GCP en el escenario mal condicionado.

## Referencias

- Suñagua S., P. (2020). *Método de Gradientes Conjugados Precondicionado*. Revista Boliviana de Matemática – UMSA, 04, 2–7.
- Golub, G. H., & Van Loan, C. F. (2013). *Matrix Computations* (4th ed.). Johns Hopkins University Press.
- Saad, Y. (2003). *Iterative Methods for Sparse Linear Systems* (2nd ed.). SIAM.

## Publicación

Para publicar con GitHub Pages, abre `Settings → Pages`, selecciona la rama `main` y la carpeta raíz (`/`). La URL resultante será el enlace público de la aplicación.
