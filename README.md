```c

#include <stdio.h>

// === PROTOTIPOS DE FUNCIÓN ===
float calcularPromedioUnidad(int u);
float calcularComponente(const char *nombreComponente, float peso);
float calcularES();
float calcularPromedioFinal(float pACD, float pAPE, float pAA, float pES);
void cualitativo(float x);

// === FUNCIÓN PRINCIPAL ===
int main() {
    const int NUMEROUNIDADES = 3;
    float acumu = 0;
    
    printf("======================================\n");
    printf("---------------- NOTAS ---------------\n");
    printf("======================================\n");

    for(int unidad = 1; unidad <= NUMEROUNIDADES; unidad++) {
        acumu += calcularPromedioUnidad(unidad);
    }
    
    acumu = acumu / NUMEROUNIDADES;
    printf("\n======================================\n");
    printf("Tu nota final de CICLO es: %.2f\n", acumu);
    cualitativo(acumu);
    printf("======================================\n");

    return 0;
}

// === DESARROLLO DE FUNCIONES ===

float calcularPromedioUnidad(int u) { 
    float notaFinalUnidad, acd, ape, aa, es;

    printf("\n======================================\n");
    printf("-------------- UNIDAD %i -------------- \n", u);
    printf("======================================\n");

    // Reutilizamos la función genérica con el nombre y su peso respectivo
    acd = calcularComponente("ACD", 0.20);
    ape = calcularComponente("APE", 0.25);
    aa  = calcularComponente("AA",  0.20);
    es  = calcularES();
    
    notaFinalUnidad = calcularPromedioFinal(acd, ape, aa, es);
    return notaFinalUnidad; 
}

// Función genérica optimizada para ACD, APE y AA
float calcularComponente(const char *nombreComponente, float peso) {
    float promedio = 0, total = 0, notaActividad;
    int nA;
    
    do {
        printf("Ingrese la cantidad de actividades (%s): \n", nombreComponente);
        if (scanf("%d", &nA) != 1 || nA <= 0) {
            printf("ERROR: Datos no Validos.\nIngrese otro valor.\n");
            while(getchar() != '\n'); // Limpia el buffer en caso de error de tipo de dato
            nA = 0;
        }
    } while(nA <= 0);

    for(int y = 1; y <= nA; y++) {
        do {
            printf("Ingrese la nota de la actividad %i:\n", y);
            scanf(" %f", &notaActividad);
            if(notaActividad < 0 || notaActividad > 10) {
                printf("//////////////////////////\n");
                printf("ERROR: Datos no Validos.\nIngrese otro valor.\n");
                printf("//////////////////////////\n");
            }
        } while(notaActividad < 0 || notaActividad > 10);
        
        total += notaActividad;
    }

    promedio = (total / nA) * peso;
    printf("El ponderado del %s es: %.2f\n\n", nombreComponente, promedio);
    return promedio;
}

float calcularES() {             
    float promedioES = 0, totalES = 0, portafolioD, evaluacionS, porcentajeABP, porcentajePD;
    
    do {
        printf("Ingrese un porcentaje para el ponderado ABP (Escala 1-100):\n");
        scanf(" %f", &porcentajeABP);

        if(porcentajeABP <= 0 || porcentajeABP > 100) {
            printf("ERROR: Datos no Validos.\nIngrese un valor entre 1 y 100.\n");
        }
    } while(porcentajeABP <= 0 || porcentajeABP > 100);

    porcentajePD = 100 - porcentajeABP;

    printf("SU PORCENTAJE ABP ES %.0f %%\n", porcentajeABP);
    printf("SU PORCENTAJE PD ES %.0f %%\n", porcentajePD);
        
    do {
        printf("Ingrese la nota de su EVALUACIÓN BASADO EN PROBLEMAS (ABP - %.0f %%):\n", porcentajeABP);
        scanf(" %f", &evaluacionS);
        if(evaluacionS < 0 || evaluaciónS > 10) {
            printf("ERROR: Datos no Validos.\n");
        }
    } while(evaluacionS < 0 || evaluacionS > 10);

    do {
        printf("Ingrese la nota de su PORTAFOLIO DIGITAL (PD - %.0f %%):\n", porcentajePD);
        scanf(" %f", &portafolioD);
        if(portafolioD < 0 || portafolioD > 10) {
            printf("ERROR: Datos no Validos.\n");
        }
    } while(portafolioD < 0 || portafolioD > 10);

    evaluacionS = evaluacionS * (porcentajeABP / 100.0);
    portafolioD = portafolioD * (porcentajePD / 100.0);
        
    totalES = evaluacionS + portafolioD;
    promedioES = totalES * 0.35;
    
    printf("El ponderado de su ES es: %.2f\n\n", promedioES);
    return promedioES;
}

float calcularPromedioFinal(float pACD, float pAPE, float pAA, float pES) { 
    float total = pACD + pAPE + pAA + pES;
    printf("--> Su NOTA FINAL DE UNIDAD es: %.2f\n", total);
    return total;    
}

void cualitativo(float x) {           
    if(x >= 7) {
        printf("Estado: === APROBADO ===\n");
    } else if(x >= 2.5) {
        printf("Estado: === ASISTIR A SUPLETORIOS ===\n"); 
    } else {
        printf("Estado: === REPROBADO / SUPLETORIO ===\n");
    }
}
```
