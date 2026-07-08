```c

#include <stdio.h>

// === PROTOTIPOS DE FUNCIÓN ===
float calcularPromedioUnidad(int u);
float calcularACD();
float calcularAPE();
float calcularAA();
float calcularES();
float calcularPromedioFinal(float pACD, float pAPE, float pAA, float pES);
void cualitativo(float x);

// === FUNCIÓN PRINCIPAL ===
int main() {
    const int NUMEROUNIDADES = 3; // Define la cantidad total de unidades a evaluar en el ciclo
    float acumu = 0;             // Acumulador para sumar las notas finales de cada unidad
    
    printf("======================================\n");
    printf("---------------- NOTAS ---------------\n");
    printf("======================================\n");

    // Bucle para iterar y procesar cada una de las 3 unidades
    for(int unidad = 1; unidad <= NUMEROUNIDADES; unidad++) {
        acumu += calcularPromedioUnidad(unidad); // Suma el promedio retornado por la unidad actual
    }
    
    // Calcula la media aritmética del ciclo dividiendo para el número de unidades
    acumu = acumu / NUMEROUNIDADES; 
    
    printf("\n======================================\n");
    printf("Tu nota final de CICLO es: %.2f\n", acumu);
    
    // Evalúa el estado académico final del estudiante según su nota acumulada
    cualitativo(acumu); 
    printf("======================================\n");

    return 0;
}

// === DESARROLLO DE FUNCIONES ===

// MÓDULO: Control de la Unidad Académica
// Coordina secuencialmente la llamada a los componentes de evaluación de una unidad específica
float calcularPromedioUnidad(int u) { 
    float notaFinalUnidad, acd, ape, aa, es;

    printf("\n======================================\n");
    printf("-------------- UNIDAD %i -------------- \n", u);
    printf("======================================\n");

    // Llama a cada componente evaluativo para obtener su valor ponderado
    acd = calcularACD(); // Componente de Aprendizaje en Contacto con el Docente
    ape = calcularAPE(); // Componente de Aprendizaje Práctico-Experimental
    aa  = calcularAA();  // Componente de Aprendizaje Autónomo
    es  = calcularES();  // Componente de Evaluación de Fin de Unidad (Examen/Evaluación Sumativa)
    
    // Envía los ponderados calculados para consolidar la nota de la unidad
    notaFinalUnidad = calcularPromedioFinal(acd, ape, aa, es);
    return notaFinalUnidad; // Retorna la nota sobre 10 de la unidad evaluada
}

// MÓDULO: Componente ACD (20%)
// Calcula el promedio de las actividades de docencia y le aplica el peso correspondiente
float calcularACD() {   
    float promedioACD = 0, totalACD = 0, notaActividad;
    int nA;
    
    printf("Ingrese la cantidad de actividades (ACD): \n");
    scanf("%d", &nA);

    // Suma iterativa de las calificaciones de cada actividad ACD
    for(int y = 1; y <= nA; y++) {
        printf("Ingrese la nota de la actividad %i:\n", y);
        scanf("%f", &notaActividad);
        totalACD += notaActividad;
    }

    // Calcula el promedio del componente y aplica el factor de ponderación del 20% (* 0.2)
    promedioACD = (totalACD / nA) * 0.2;
    printf("El ponderado del ACD es: %.2f\n\n", promedioACD);
    return promedioACD; 
}

// MÓDULO: Componente APE (25%)
// Obtiene el promedio de las tareas prácticas o experimentales y aplica su ponderación
float calcularAPE() {    
    float promedioAPE = 0, totalAPE = 0, notaActividad;
    int nA;
    
    printf("Ingrese la cantidad de actividades (APE): \n");
    scanf("%d", &nA);
    
    // Recopila y acumula las notas de las actividades prácticas
    for(int y = 1; y <= nA; y++) {
        printf("Ingrese la nota de la actividad %i:\n", y);
        scanf("%f", &notaActividad);
        totalAPE += notaActividad;
    }

    // Calcula la media de los registros y aplica la ponderación del 25% (* 0.25)
    promedioAPE = (totalAPE / nA) * 0.25;
    printf("El ponderado del APE es: %.2f\n\n", promedioAPE);
    return promedioAPE;
}

// MÓDULO: Componente AA (20%)
// Procesa las lecturas o trabajos autónomos asignados en la unidad
float calcularAA() {           
    float promedioAA = 0, totalAA = 0, notaActividad;
    int nA;
    
    printf("Ingrese la cantidad de actividades (AA): \n");
    scanf("%d", &nA);
    
    // Captura individual de las notas de aprendizaje autónomo
    for(int y = 1; y <= nA; y++) {
        printf("Ingrese la nota de la actividad %i:\n", y);
        scanf("%f", &notaActividad);
        totalAA += notaActividad;
    }

    // Promedia las calificaciones obtenidas y calcula su peso equivalente al 20% (* 0.2)
    promedioAA = (totalAA / nA) * 0.2;
    printf("El ponderado del AA es: %.2f\n\n", promedioAA);
    return promedioAA;
}

// MÓDULO: Componente ES - Evaluación Sumativa (35%)
// Divide la nota del examen final en subcomponentes dinámicos (ABP y Portafolio) distribuidos bajo un porcentaje variable
float calcularES() {             
    float promedioES = 0, totalES = 0, portafolioD, evaluacionS, porcentajeABP, porcentajePD;
    
    // Configuración de la distribución interna del componente sumativo
    printf("Ingrese un porcentaje para el ponderado ABP (Escala 1-100):\n");
    scanf("%f", &porcentajeABP);

    // El porcentaje restante se asigna automáticamente al Portafolio Digital (PD) para completar el 100% de la subnota
    porcentajePD = 100 - porcentajeABP;

    printf("SU PORCENTAJE ABP ES %.0f %%\n", porcentajeABP);
    printf("SU PORCENTAJE PD ES %.0f %%\n", porcentajePD);
        
    // Entrada de calificaciones directas sobre la escala base de 10
    printf("Ingrese la nota de su EVALUACIÓN BASADO EN PROBLEMAS (ABP - %.0f %%):\n", porcentajeABP);
    scanf("%f", &evaluacionS);

    printf("Ingrese la nota de su PORTAFOLIO DIGITAL (PD - %.0f %%):\n", porcentajePD);
    scanf("%f", &portafolioD);

    // Ponderación interna: Ajusta las dos notas basándose en los porcentajes elegidos
    evaluacionS = evaluacionS * (porcentajeABP / 100.0);
    portafolioD = portafolioD * (porcentajePD / 100.0);
        
    // Consolidación de la nota sumativa total sobre la escala base de 10
    totalES = evaluacionS + portafolioD;

    // Aplica el peso del parámetro Evaluación Sumativa correspondiente al 35% del total de la unidad (* 0.35)
    promedioES = totalES * 0.35;
    printf("El ponderado de su ES es: %.2f\n\n", promedioES);
    return promedioES;
}

// MÓDULO: Consolidación de Unidad
// Recibe los cuatro subtotales ponderados y los unifica en la nota definitiva de la unidad
float calcularPromedioFinal(float pACD, float pAPE, float pAA, float pES) { 
    float total = pACD + pAPE + pAA + pES; // Sumatoria directa de los pesos proporcionales
    printf("--> Su NOTA FINAL DE UNIDAD es: %.2f\n", total);
    return total;    
}

// MÓDULO: Clasificación Cualitativa
// Determina la condición final basándose en el puntaje definitivo del ciclo (Escala de 0 a 10)
void cualitativo(float x) {           
    if(x >= 7) {
        // Mayor o igual a 7 aprueba directamente la asignatura
        printf("Estado: === APROBADO ===\n");
    } else if(x >= 2.5) {
        // Calificaciones entre 2.5 y 6.99 habilitan la opción de rendir exámenes supletorios
        printf("Estado: === ASISTIR A SUPLETORIOS ===\n"); 
    } else {
        // Notas inferiores a 2.5 representan reprobación automática del curso
        printf("Estado: === REPROBADO / SUPLETORIO ===\n");
    }
}
```
